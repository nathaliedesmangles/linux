+++
title = "Entrées/Sorties, redirection, filtres et Pipeline des commandes"
weight = 41
+++

---
### 7. Utilisation spécifique avec `find`
Pour éviter une expansion prématurée par Bash, protégez les motifs :  
```bash
find / -name "*.txt"
```


## Bonnes pratiques avec les variables
1. **Utilisez des guillemets** pour gérer les espaces :  
   ```bash
   ls "$fichiers"
   ```
2. **Protégez les motifs pour `find` :**  
   ```bash
   find / -name "*.txt"
   ```
3. **Utilisez des accolades pour automatiser :**  
   ```bash
   touch fichier{1..10}.txt
   ```
======
Les entrées et sorties des commandes, la redirection des commandes, les filtres et les pipelines de commandes permettent de manipuler et de traiter des données de manière puissante et flexible, en utilisant des commandes simples mais très efficaces.

## Les entrées et sorties des commandes

Dans le système d'exploitation Linux, les commandes interagissent avec trois flux de données principaux :

- **Entrée standard** (*stdin*) : Il s'agit du flux de données d'entrée par défaut pour les commandes. Par défaut, stdin est lié au clavier, ce qui signifie que les commandes lisent les données saisies par l'utilisateur. Cependant, `stdin` peut être redirigé pour lire des données à partir de fichiers ou d'autres commandes.

- **Sortie standard** (*stdout*, numérotée ***1***) : Il s'agit du flux de données de sortie par défaut pour les commandes. Par défaut, `stdout` est lié à l'écran, ce qui signifie que les commandes affichent leurs résultats à l'écran. Cependant, `stdout` peut être redirigé pour écrire des données dans des fichiers ou les transmettre à d'autres commandes.

- **Erreurs standard** (*stderr*, numérotée ***2***) : Il s'agit du flux de données de sortie pour les messages d'erreur. Par défaut, `stderr` est également lié à l'écran, ce qui signifie que les messages d'erreur sont affichés à l'écran. Comme `stdout`, `stderr` peut être redirigé pour écrire des messages d'erreur dans des fichiers ou les transmettre à d'autres commandes.

### La redirection des entrées et sorties

L'utilisation de `stdin`, `stdout` et `stderr` est essentielle pour manipuler les flux de données dans Linux.

#### Redirection de `stdin` (Entrée standard)

Par défaut, `stdin` (**<**) lit les données saisies par l'utilisateur via le clavier. 

> [!INFO]
Nous ne verrons pas la redirection à l’aide de `<`.

Cependant, vous pouvez rediriger `stdin` pour lire des données à partir d'un fichier ou d'une autre commande, en récupérant la sortie standard d’une autre commande grâce au pipeline (vu plus bas).


#### Redirection de `stdout` (Sortie standard)

Par défaut, `stdout` (**>** et **>>**) affiche les résultats des commandes à l'écran. Vous pouvez rediriger `stdout` pour écrire les résultats dans un fichier ou les transmettre à une autre commande.

```
commande > fichier.txt
```
Cette commande enregistre la sortie de `commande` dans `sortie.txt`, écrasant le contenu existant du fichier.

**Exemples** :

La commande `find / -name services` retourne à l'écran (`stdout`) les noms des fichiers ou des répertoires nommés "services" à partir de la racine du système de fichiers (/). 

Si on souhaite , on peut rediriger la sortie standard (`stdout`) vers un fichier (ex: resultat.txt):

```bash
find / -name services > resultat.txt
```
Ou
```bash
find / -name services 1> resultat.txt
```

Ces commandes envoient le résultat dans un fichier au lieu de l’envoyer à l’écran.

> [!Important]
Avec `>` ou `1>`, le contenu du fichier sera **écrasé**.

Pour ne pas écraser le contenu existant, il faut utiliser `>>` comme dans l'exemple ci-dessous:

```bash
find / -name services >> resultat.txt
```

Cette commande ajoute le résultat à la fin du fichier `resultat.txt` sans écraser le contenu existant.

> [!INFO]
La mention ***Permission denied*** est un message d'erreur indiquant qu'il faut avoir les droits d'accès sur les fichiers ou répertoires. 

#### Redirection de `stderr` (Erreurs standard)

Par défaut, `stderr` affiche les messages d'erreur à l'écran. Vous pouvez rediriger `stderr` pour écrire les messages d'erreur dans un fichier ou les transmettre à une autre commande.

```bash
find / -name services 2> erreurs.txt
```
Cette commande envoie les messages d'erreur dans le fichier `erreurs.txt`.

Il est possible de rediriger la sortie standard et la sortie d’erreur standard.

```bash
$ find / -name services > resultats.txt 2>/dev/null
```

Il est aussi possible de rediriger la sortie d’erreur standard vers la sortie standard (`&1`) et d’envoyer le tout dans un fichier:

```bash
$ find / -name services > resultats.txt 2>&1
```
- **`2>&1`** : Cette syntaxe redirige `stderr` vers la même destination que `stdout`.

Il est possible de se débarrasser des erreurs en redirigeant la sortie d’erreur standard.

```bash
$ find / -name services 2>/dev/null
```

`/dev/null` agit comme un trou noir dans lequel tout ce qu’on envoie disparait.

- **`&>`** : Ce symbole redirige à la fois `stdout` et `stderr` vers un fichier spécifié.

L'utilisation des symboles `&>` et `2>&1` permet de rediriger à la fois les sorties standard et les erreurs standard.

Vous pouvez rediriger à la fois `stdout` et `stderr` vers un fichier ou une autre commande.

*****

```
commande > sortie.txt 2> erreurs.txt
```
Cette commande enregistre la sortie de `commande` dans `sortie.txt` et les messages d'erreur dans `erreurs.txt`.

```
commande &> tout.txt
```
Cette commande enregistre à la fois la sortie et les messages d'erreur de `commande` dans `tout.txt`.

#### Redirection combinée

La redirection combinée permet de rediriger simultanément les sorties standard (`stdout`) et les erreurs standard (`stderr`) vers un fichier ou une autre commande. Cela est particulièrement utile pour capturer toutes les sorties d'une commande, y compris les messages d'erreur, dans un seul fichier.



**Exemple 1 : Utilisation de `&>`**
```
commande &> tout.txt
```
Cette commande redirige à la fois la sortie standard et les erreurs standard de `commande` vers le fichier `tout.txt`.

**Exemple 2 : Utilisation de `2>&1`**
```
commande > sortie.txt 2>&1
```
Cette commande redirige la sortie standard de `commande` vers le fichier `sortie.txt` et redirige les erreurs standard vers la même destination que la sortie standard.

**Exemple 3 : Redirection combinée avec append**
```
commande >> sortie.txt 2>&1
```
Cette commande ajoute la sortie standard et les erreurs standard de `commande` à la fin du fichier `sortie.txt` sans écraser le contenu existant.

#### Utilisation des Pipelines

Les pipelines permettent de rediriger la sortie d'une commande (`stdout`) comme entrée (`stdin`) d'une autre commande en utilisant le symbole `|` (se prononce pipe).

```
commande1 | commande2
```
Cette commande utilise la sortie de `commande1` comme entrée pour `commande2`.

**Exemple** :

```bash
ls -l | grep ".txt" | sort
```
Cette commande liste les fichiers du répertoire courant, filtre ceux qui ont l'extension `.txt`, puis trie les résultats.

#### Redirection combinée avec un pipeline
```
commande1 | commande2 > sortie.txt 2>&1
```
Cette commande utilise un pipeline pour rediriger la sortie de `commande1` vers `commande2`, puis redirige la sortie standard et les erreurs standard de `commande2` vers le fichier `sortie.txt`.

## Les filtres de commandes

Les filtres sont des commandes qui prennent des données en entrée, les transforment et produisent des données en sortie. Ils sont utilisés pour manipuler et traiter des données de manière précise et efficace. Les filtres sont souvent utilisés dans des pipelines pour créer des chaînes de traitement de données complexes.

Les filtres jouent un rôle crucial dans le traitement des données sous Linux. Ils permettent de :
- **Filtrer** : Sélectionner uniquement les données pertinentes en fonction de critères spécifiques.
- **Transformer** : Modifier les données pour les adapter à un format ou à une structure souhaitée.
- **Analyser** : Extraire des informations utiles à partir des données brutes.
- **Combiner** : Fusionner les données provenant de différentes sources pour obtenir un résultat cohérent.

### Les commandes de filtrage courantes AJOUTER FIND

| Commande |      Description      | Option |      Description de l'option      | Exemple |
|----------|-----------------------|--------|-----------------------------------|---------|
| `grep`   | Recherche de motifs dans les fichiers. | `-i`   | Ignore la casse (majuscule/minuscule) | `grep -i "motif" fichier.txt` |
|          |             | `-r`   | Recherche récursive dans les répertoires | `grep -r "motif" /chemin/du/repertoire` |
|          |             | `-v`   | Inverse la recherche, affichant les lignes qui ne correspondent pas au motif | `grep -v "motif" fichier.txt` |
|          |             | `-n`   | Affiche les numéros de ligne des correspondances | `grep -n "motif" fichier.txt` |
| `sed`    | Édition de flux de texte. | `-e`   | Permet de spécifier plusieurs commandes | `sed -e 's/ancien/nouveau/' -e 's/vieux/neuf/' fichier.txt` |
|          |             | `-i`   | Modifie les fichiers en place | `sed -i 's/ancien/nouveau/g' fichier.txt` |
| `cut`    | Extraction de sections de lignes. | `-d`   | Spécifie le délimiteur | `cut -d ',' -f 1,3 fichier.csv` |
|          |             | `-f`   | Spécifie les champs à extraire | `cut -f 1,3 fichier.txt` |
| `sort`   | Tri des lignes. | `-r`   | Trie dans l'ordre inverse | `sort -r fichier.txt` |
|          |             | `-n`   | Trie numériquement | `sort -n fichier.txt` |
|          |             | `-k`   | Trie selon une clé spécifique | `sort -k 2 fichier.txt` |
| `uniq`   | Suppression des doublons. | `-c`   | Affiche le nombre de fois que chaque ligne apparaît | `uniq -c fichier.txt` |
|          |             | `-d`   | Affiche uniquement les lignes en double | `uniq -d fichier.txt` |
| `wc`     | Comptage des lignes, mots et caractères. | `-l`   | Compte les lignes | `wc -l fichier.txt` |
|          |             | `-w`   | Compte les mots | `wc -w fichier.txt` |
|          |             | `-c`   | Compte les caractères | `wc -c fichier.txt` |
| `tr`     | Traduction ou suppression de caractères. | `-d`   | Supprime les caractères spécifiés | `echo "texte" | tr -d 'aeiou'` |
|          |             | `-s`   | Remplace les séquences de caractères répétés par un seul caractère | `echo "aaabbbccc" | tr -s 'a-c'` |

#### Commande `grep`

- `grep` (*Global Regular Expression Print*) est utilisée pour rechercher des motifs dans des fichiers.

```bash
grep "motif" fichier.txt
```
Cette commande recherche le mot "motif" dans `fichier.txt`.

#### Commande `sed`

- `sed` (*Stream Editor*) est un éditeur de texte en ligne de commande qui permet de modifier des fichiers de manière non interactive.

```bash
sed 's/ancien/nouveau/g' fichier.txt
```
Cette commande remplace toutes les occurrences de "ancien" par "nouveau" dans `fichier.txt`.


#### Commande `cut`

- `cut` est utilisée pour extraire des sections de chaque ligne d'un fichier.

```bash
cut -d ',' -f 1,3 fichier.csv
```
Cette commande extrait les champs 1 et 3 des lignes du fichier `fichier.csv`, en utilisant la virgule comme délimiteur.

#### Commande `sort`

- `sort` est utilisée pour trier les lignes d'un fichier texte ou d'une entrée standard.

```bash
sort fichier.txt
```
Cette commande trie les lignes de `fichier.txt`.

#### Commande `uniq`

- `uniq` est utilisée pour supprimer les lignes en double dans un fichier trié.

```bash
sort fichier.txt | uniq
```
Cette commande trie les lignes de `fichier.txt` et supprime les doublons.

#### Commande `wc`

**Rappel de la semaine 2** : `wc` (Word Count) est utilisée pour compter les lignes, les mots et les caractères dans un fichier.

```bash
wc -l fichier.txt
```
Cette commande affiche le nombre de lignes dans `fichier.txt`.

#### Commande `tr`

- `tr` (Translate) est utilisée pour traduire ou supprimer des caractères.

```bash
echo "texte" | tr 'a-z' 'A-Z'
```
Cette commande convertit les lettres minuscules en majuscules dans le texte "texte".

### Combinaison de plusieurs filtres à l'aide de `|`

**Exemple 1 : Compter les lignes contenant un motif spécifique**
```bash
grep "motif" fichier.txt | wc -l
```
Cette commande recherche "motif" dans `fichier.txt` et compte le nombre de lignes correspondantes.

**Exemple 2 : Afficher les 10 plus grands fichiers**
```bash
ls -l | sort -k 5 -n | tail -n 10
```
Cette commande liste les fichiers du répertoire courant, trie les résultats par taille (colonne 5) et affiche les 10 plus grands fichiers.

**Exemple 3 : Trouver les fichiers modifiés récemment**
```bash
find . -type f -mtime -7 | xargs ls -l
```
Cette commande trouve les fichiers modifiés au cours des 7 derniers jours et affiche leurs détails.

**Exemple 4 : Extraire et trier des champs spécifiques d'un fichier CSV**
```bash
cut -d ',' -f 2 fichier.csv | sort | uniq
```
Cette commande extrait le deuxième champ de chaque ligne de `fichier.csv`, trie les résultats et affiche les lignes uniques.

**Exemple 5 : Remplacer un mot dans plusieurs fichiers**
```bash
grep -rl "ancien" . | xargs sed -i 's/ancien/nouveau/g'
```
Cette commande recherche tous les fichiers contenant "ancien" dans le répertoire courant et remplace "ancien" par "nouveau" dans ces fichiers.


