+++
title = "ATELIER #5: Gestion des processus Linux"
weight = 52
+++


## Objectifs de l'atelier

Dans cet atelier, vous allez créer deux versions d’un script Bash :  

1. Une version **séquentielle**, où les commandes s'exécutent les unes après les autres. 
	- `nombre_de_fichiers_seq.sh` : Affiche le nombre de fichiers par type. 
2. Une version **asynchrone**, où plusieurs commandes s'exécutent simultanément en arrière-plan.  
	- `nombre_de_fichiers_conc.sh` : Réécriture du script précédent avec des commandes asynchrones (`&`).

---

## Remise

Vous devez remettre sur Moodle :
- Vos deux fichiers `.sh`
- Deux captures d’écran illustrant le fonctionnement des scripts :

| Capture                            | Contenu                                      |
|------------------------------------|----------------------------------------------|
| **01_nombre_de_fichiers_seq.png**  | Exécution du script `nombre_de_fichiers_seq.sh` et résultats      |
| **02_nombre_de_fichiers_conc.png** | Exécution du script `nombre_de_fichiers_conc.sh` et son résultat      |


--- 


## **Rappels** 

### Stocker une valeur dans une variable
```bash
nb=$(ls | wc -l)
```
Cette commande stocke le nombre de fichiers du répertoire courant dans la variable `nb`.  

### Tester la valeur d’une variable
 
Pour comparer la valeur d’une variable à un chiffre :  
```bash
test $nb -eq 10
```
Cette commande compare `nb` à `10`. Si les deux valeurs sont égales, le code de retour sera `0`, sinon il sera différent de `0`.  

On peut alors utiliser cette comparaison dans une condition :  
```bash
test $nb -eq 10 && echo "Les deux valeurs sont égales" || echo "Les deux valeurs sont différentes"
```

### Parcourir une variable avec une boucle *for*
  
Si vous avez une liste de serveurs dans une variable et souhaitez les parcourir :  
```bash
serveurs="google.com facebook.com youtube.com"
for i in $serveurs; do echo $i; done
```

---

# Atelier

## Exercice 1 : Script séquentiel  

Créer un script `nombre_de_fichiers_seq.sh` contenant des commandes **séquentielles**.  

**Le script doit** :  
1. **Compter** le nombre de fichiers pour les extensions suivantes : `java`, `conf`, `txt`, `png`, `tiff`.  
2. **Afficher** le nombre de fichiers pour chaque type.  
3. **Si aucun fichier d'un type donné n'existe**, afficher :  
   ```bash
   Il n’y a aucun fichier .<extension>
   ```
4. **Ne pas afficher d’autres informations**.  

**À inclure au début du script**  
```bash
types="java conf txt png tiff"
```

**Exemple de résultat**  
```bash
Décompte des fichiers java conf txt png tiff

Il y a 50718 fichiers .java  
Il y a 1171 fichiers .conf  
Il y a 6999 fichiers .txt  
Il y a 67296 fichiers .png  
Il n’y a aucun fichier .tiff  
```

---

## Exercice 2 : Script concurrent 

Créer un script `nombre_de_fichiers_conc.sh`, qui est une version **asynchrone** du script précédent.  

**Spécifications du script**  
1. Effectuer **exactement** les mêmes opérations que le script séquentiel.  
2. Utiliser le symbole `&` pour exécuter les commandes **en arrière-plan**.  
3. Exécuter **toutes les commandes `find` simultanément**.  
4. Regrouper les commandes avec `(CMD1; CMD2; …) &` pour les exécuter en parallèle.  
5. Ajouter une commande `wait` à la fin du script pour s’assurer que tous les processus se terminent avant la fin du script.  

**Exemple de résultat**  
L’ordre des lignes peut être différent en raison de l’exécution parallèle.  
```bash
Décompte des fichiers java conf txt png tiff

Il y a 1171 fichiers .conf  
Il n’y a aucun fichier .tiff  
Il y a 67296 fichiers .png  
Il y a 50718 fichiers .java  
Il y a 6999 fichiers .txt  
```