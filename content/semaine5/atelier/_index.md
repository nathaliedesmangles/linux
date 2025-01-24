+++
title = "ATELIER #5: Gestion des processus Linux"
weight = 52
+++


## Objectifs de l'atelier

- Manipuler les processus sous Linux en utilisant des commandes de base.
- Comprendre et explorer les différents types de processus sous Linux.
- Apprendre à lister, gérer et contrôler les processus.
- Manipuler les processus en premier plan et en arrière-plan.


### Remise

Vous devez remettre sur Moodle :
- Vos deux fichiers `.sh`
- Deux captures d’écran illustrant le fonctionnement des scripts :

| Capture                     | Contenu                                      |
|-----------------------------|----------------------------------------------|
| 01_nombre_de_fichiers_seq.png | Appel au script séquentiel et résultats      |
| 02_nombre_de_fichiers_conc.png | Appel au script concurrent et résultats      |

---

# Atelier

Dans cet atelier, vous apprendrez à créer deux scripts Bash : 
1. l’un avec des commandes séquentielles et 
2. l’autre avec des commandes exécutées de manière asynchrone. 

Ces scripts vous permettront de mieux comprendre les différences entre l’exécution séquentielle et concurrente.

## Astuces et rappels

### Stocker une valeur dans une variable

Pour stocker le nombre de fichiers présents dans un répertoire :
```bash
nb=$(ls | wc -l)
```
Cette commande place le nombre de fichiers dans la variable `nb`.

### Tester la valeur d’une variable

Pour comparer une variable à un chiffre :
```bash
test $nb -eq 10
```
Cette commande vérifie si `nb` est égal à 10. Si c’est le cas, le code de retour sera `0`, sinon il sera différent de `0`.

Vous pouvez combiner cette commande avec des opérateurs logiques :
```bash
test $nb -eq 10 && echo "Les deux valeurs sont égales" || echo "Les deux valeurs sont différentes"
```

### Parcourir une variable avec une boucle `for`

Pour parcourir une liste de serveurs :
```bash
serveurs="google.com facebook.com youtube.com"
for i in $serveurs; do echo $i; done
```
Chaque élément de la variable `serveurs` sera affiché séparément.

### Conseils supplémentaires

- Pour mesurer les performances des scripts, utilisez la commande `time`.
- Comparez les temps d’exécution pour comprendre l’intérêt de la concurrence.

---

## Exercice 1 : Script séquentiel

- Créer un script Bash nommé **nombre_de_fichiers_seq.sh** pour compter le nombre de fichiers par type.

### Aide pour l'exercice

- Ce script doit compter et afficher le nombre de fichiers pour chaque type suivant : `java`, `conf`, `txt`, `png`, `tiff`.
- Structure de base

  Ajoutez cette ligne au début du script :
  ```bash
   types="java conf txt png tiff"
  ```
- Fonctionnalités à implémenter

   1. Compter le nombre de fichiers pour chaque type.
   2. Afficher un message si aucun fichier n’est trouvé.
   3. Ne pas afficher d’autres messages.

- Exemple de sortie

```plaintext
Décompte des fichiers java conf txt png tiff

Il y a 50718 fichiers .java
Il y a 1171 fichiers .conf
Il y a 6999 fichiers .txt
Il y a 67296 fichiers .png
Il n’y a aucun fichier .tiff
```


## Exercice 2 : Script concurrent

- Créer une version concurrente de ce script nommée **nombre_de_fichiers_conc.sh**, en utilisant des commandes asynchrones (&).

### Aide pour l'exercice

- Ce script doit être une version améliorée de **nombre_de_fichiers_seq.sh**, en exécutant les commandes de manière asynchrone.
- Fonctionnalités à implémenter

   1. Utiliser `&` pour exécuter les commandes `find` en arrière-plan.
   2. Regrouper les processus dans un sous-processus avec `(CMD1; CMD2; ...) &`.
   3. Utiliser la commande `wait` à la fin pour attendre la fin de tous les processus en arrière-plan.

- Exemple de sortie

```plaintext
Décompte des fichiers java conf txt png tiff

Il y a 1171 fichiers .conf
Il n’y a aucun fichier .tiff
Il y a 67296 fichiers .png
Il y a 50718 fichiers .java
Il y a 6999 fichiers .txt
```