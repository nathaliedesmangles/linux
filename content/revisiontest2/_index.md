+++
title = "TEST #2-Quelques notions à maitriser"
weight = 55
+++

{{% notice style="warning" title="Revenez me voir" %}}
D'ici le test #2 (**jeudi 20 mars**), revenez sur cette page fréquemment, pour prendre connaissance des ajouts et/ou modifications.

***Ne vous limitez pas à cette page pour vous préparer au test #2, car certaines notions du cours ne s'y trouvent pas***.
{{% /notice %}}


## 1. La commande *tree*  
La commande `tree` permet d’**afficher la structure des dossiers sous forme d’arbre**. Elle est utile pour visualiser rapidement l’organisation des fichiers.  
**Exemple :**  
```bash
tree mon_dossier/
```
Affiche tous les fichiers et sous-dossiers de `mon_dossier`.

## 2. La commande *grep* 
La commande `grep` est utilisée pour **rechercher un mot ou une expression dans un fichier ou une sortie de commande**.  
**Exemple :**  
```bash
grep "erreur" journal.log
```
Affiche toutes les lignes contenant "erreur" dans le fichier `journal.log`.

## 3. La commande *sed*
La commande `sed` permet de **modifier un fichier en remplaçant du texte** sans l’ouvrir manuellement.  
**Exemple :**  
```bash
sed 's/ancien/nouveau/g' fichier.txt
```
Remplace toutes les occurrences de "ancien" par "nouveau" dans `fichier.txt`.

## 4. La commande *cut* 
La commande `cut` est utilisée pour extraire des parties spécifiques d’une ligne de texte, généralement des colonnes dans un fichier CSV ou un tableau.  
**Exemple :**  
```bash
cut -d',' -f2 fichier.csv
```
Affiche la deuxième colonne du fichier `fichier.csv`, en supposant que les colonnes sont séparées par des virgules.

## 5. La commande *sort* 
La commande `sort` permet de **trier les lignes d’un fichier** dans un ordre spécifique.  
**Exemple :**  
```bash
sort noms.txt
```
Trie les lignes du fichier `noms.txt` par ordre alphabétique.

## 6. Redirection des résultats  
Les **résultats des commandes peuvent être redirigés vers un fichier ou enchaînés avec d'autres commandes**.

- `>` : Écrit dans un fichier (écrase le contenu existant)  
  ```bash
  ls > liste_fichiers.txt
  ```
- `>>` : Ajoute au fichier sans écraser le contenu existant  
  ```bash
  echo "Nouveau texte" >> liste_fichiers.txt
  ```
- `|` (pipe) : Enchaîne des commandes  
  ```bash
  ls | grep "txt"
  ```
  Affiche uniquement les fichiers contenant "txt" dans leur nom.
 

## 7. **La commande *find***  
`find` permet de **rechercher des fichiers** dans un répertoire selon divers critères :  
```bash
find /home -name "*.txt"
```
Ce code cherche et affiche tous les fichiers `.txt` qui se trouvent dans `/home`.  

Autre exemple :  
```bash
find . -type d     
```
Ce code cherche et affiche tous les répertoires qui se trouvent dans le répertoire actuel. 


## 8. **La commande *wc***  
`wc` (word count) permet de **compter le nombre** de **lignes**, **mots** et **caractères** dans un fichier :  
```bash
wc -l fichier.txt   # Compte les lignes  
wc -w fichier.txt   # Compte les mots  
wc -c fichier.txt   # Compte les caractères  
```

## 9. **Variables**  
Une variable **stocke une valeur**, comme du **texte** ou un **nombre** ou le **résultat d'un commande** (voir le point 10.):  
```bash
nom="Alice"
age=25
```
On accède à la **valeur d'une variable** avec `$` :  
```bash
echo "Bonjour, $nom !"
```


## 10. **Stocker le résultat d’une commande dans une variable**  
On peut stocker le résultat d’une commande dans une variable avec `$(...)` :  
```bash
date_actuelle=$(date)
echo "Nous sommes le $date_actuelle"
```


## 11. **Pipe-line (|)**  
Le pipe (`|`) permet de **transmettre la sortie d'une commande à la commande suivante** :  
```bash
ls -l | grep "linux"
```
Voici ce que ce code fait:
1. `ls -l`: liste les fichiers du répertoire courant
2. `grep "linux"`: prends le résultat de la première commande, dans ce résultat, cherche les fichiers qui contiennent le mot "linux" et affiche uniquement ces fichiers.  

Autre exemple :  
```bash
cat fichier.txt | wc -l
```
Ce code compte le nombre de lignes dans fichier.txt. `cat fichier.txt` retourne le contenu du fichier à la commande `wc -l` pour compter les lignes.


### 12. **Opérateurs de comparaison et logiques**  
Les opérateurs de comparaison permettent de comparer des valeurs :  
 
En bash, **Il ne faut pas utiliser** les opérateurs `=`, `!=`, `<`, `<=`, `>`, `>=`. Il faut plutôt utiliser les opérateurs ci-dessous :

| Opérateur | Signification   |
|-----------|:---------------:|
| `-eq`     | égal à          |
| `-ne`     | différent de    |
| `-lt`     | inférieur à     |
| `-le`     | inférieur ou égal à |
| `-gt`     | supérieur à     |
| `-ge`     | supérieur ou égal à |  

Les opérateurs logiques permettent de combiner des conditions :  
- commande1 `&&` commande2 : ET (exécute la commande suivante **si la première commande réussit**)  
- commande1 `||` commadne2 : OU (exécute la commande suivante **si la première commande échoue**)  

Exemples :  
```bash
test $age -ge 18 && echo "Majeur" || echo "Mineur"
```
**Cas 1**: si age=20, `test $age -ge 18` réussit, donc c'est "Majeur" qui s'affiche <br>
**Cas 2**: si age=17, `test $age -ge 18` échoue, donc c'est "Mineur" qui s'affiche


## 13. La commande `test`  
`test` permet d’évaluer des **conditions** sur des **fichiers** et des **valeurs numériques** :  
```bash
test -e "fichier.txt" && cat fichier.txt || touch fichier.txt
test $note ge 60 && echo "Cours réussit" || echo "Cours échoué"
```
**Explication du premier test** :
- `test -e "fichier.txt"` vérifie si le fichier existe. S'il existe on affiche son contenu avec `cat fichier.txt`, sinon, on crée le fichier a l'aide de la commande `touch fichier.txt`.

## 14. Boucles *for* et *while*  
Les boucles permettent d’**exécuter des commandes plusieurs fois**.  

**Boucle for** :  
```bash
for variable in éléments_sur_lesquels_boucler
do
    commande1
    commande2
    commande3
    ...
done
```


**Boucle `while`** :  
```bash
while condition
do
    commande1
    commande2
    commande3
    ...
done
```

**NB**: Dans un fichier .sh, que ce soit pour la boucle `for` ou la boucle `while`, **on ne mets pas les point-virgule, on les remplace par un saut de ligne.**

## 15. Processus séquentiels vs concurrents  

**Processus séquentiels** :  
Les commandes **s’exécutent l’une après l’autre dans l'ordre qu'elles sont écrites** :  
```bash
echo "S'affiche en premier"
echo "S'affiche en deuxième"
echo "S'affiche en premier"
```

**Processus concurrents** :  
On peut exécuter des commandes en parallèle (simultanément) avec `&` :  
```bash
commande1 &  # s'exécute en arrière-plan
commande2 &  # s'exécute en arrière-plan
commande3 &  # s'exécute en arrière-plan
wait # s'assure que les 3 commandes sont terminées avant d'executer le `echo` suivant
echo "Autre tâche en cours"
```
On peut utiliser les parenthèses `( )` pour grouper des commandes à executer en parallèle. Exemples:
```bash
for i in une_liste_d'éléments
do
  (commande1
   commande2
   commande3) &
done
```

OU

```bash
for i in une_liste_d'éléments
do
  (commande1) &
  (commande2) &
  (commande3) &
done
```

**Rappel** : La variable `i` aura comme valeur un élément à la fois de la liste à parcourir, à chaque tour de la boucle. Pour utiliser cette valeur, on devra utiliser `$i`.
