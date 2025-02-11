+++
title = "Atelier 4"
weight = 164
draft = true
+++

# Solution des exercices

## Exercice 1

1. Ouvrir une session avec l’utilisateur standard et reproduire, dans le répertoire courant, l'arborescence suivante et ce en utilisant un **maximum de trois commandes** : 
 
```
├── H2025
│   ├── Linux
│   │   ├── Cours
│   │   └── Ateliers
│   └── Virtualisation
│       └── machines
└── Personnel
``` 

### Solution 1 : Une seule commande ***mkdir -p***

```bash
$ mkdir -p H2025/Linux/{Cours,Ateliers} H2025/Virtualisation/machines Personnel
```
**Avantages** : Très concise, une seule commande.  
**Inconvénients** : Moins lisible si l'arborescence est complexe.  

---

### Solution 2 : Trois commandes ***mkdir*** séparées
```bash
$ mkdir -p H2025/Linux H2025/Virtualisation Personnel
$ mkdir -p H2025/Linux/Cours H2025/Linux/Ateliers
$ mkdir -p H2025/Virtualisation/machines
```
**Avantages** : Plus lisible, chaque commande crée une partie logique de l'arborescence.  
**Inconvénients** : Utilise trois commandes, soit le maximum autorisé.   

---


2. Changer de répertoire en allant dans le dossier **Cours**. 
```bash
$ cd ~/H2025/Linux/Cours
```

3. En saisissant une seule commande, créer, à l’intérieur du répertoire courant, les dossiers semaine1, semaine2, …, semaine15. Vous **ne devez pas** entrer tous les noms de semaines dans la commande (**hint**: expansion d'accolades). 
```bash
$ mkdir semaine{1..15}
```

4. À l'aide d'une **boucle for**, à l'intérieur de chaque dossier **semaine**, créer un fichier qui contient la phrase suivante :
<mark>Ce cours concerne la semaineN</mark>

Où `N` correspond au numéro de la semaine. 
```bash
$ for i in {1..15}; do echo "Ce cours concerne la semaine$i" > semaine$i/semaine$i.txt; done
```
**Explication** :
- ***for i in {1..15}*** : Crée une boucle qui itère de 1 à 15.
- ***echo "Ce cours concerne la semaine$i"*** : Génère la phrase avec le numéro de la semaine.
- ***> semaine$i/semaine$i.txt*** : Crée un fichier semaine$i.txt dans le dossier semaine$i et y écrit la phrase.

5. Toujours à partir du répertoire courant, utiliser un **chemin relatif** pour copier dans le dossier **Ateliers** le fichier **`passwd`** qui est dans **`/etc`**. 
```bash
$ cp /etc/passwd ./Ateliers/
```

6. Toujours à partir du répertoire courant et en utilisant le chemin relatif, renommer le fichier copié en ajoutant "Copie" à son nom (`passwdCopie`).
```bash
$ mv ./Ateliers/passwd ./Ateliers/passwdCopie
```

7. Changer le caractère délimiteur du fichier `passwdCopie` par `;` (point-virgule).
```bash
$ sed -i 's/:/;/g' ./Ateliers/passwdCopie
```

**Explication :**
- `sed` : Outil pour modifier un fichier en ligne.
- `-i` : Modifie le fichier en place (sans créer de fichier temporaire).
- `s/:/;/g` : Remplace tous les `:` par des `;` (g pour global, c'est-à-dire dans tout le fichier).
- `./Ateliers/passwdCopie` : Le fichier à modifier, situé dans le dossier **`Ateliers`**.

8. Trier le contenu du fichier `passwdCopie` en ordre croissant du numéro de groupe, soit le quatrième champ. On veut que le fichier soit trié et non uniquement le résultat retourné par la commande. 
```bash
$ sort -t ';' -k4,4 ./Ateliers/passwdCopie -o ./Ateliers/passwdCopie
```

**Explication :**
- `sort` : Outil pour trier le contenu d'un fichier.
- `-t ';'` : Définit le délimiteur comme étant le point-virgule (`;`).
- `-k4,4` : Trie les lignes en fonction du quatrième champ.
- `-o ./Ateliers/passwdCopie` : Sauvegarde directement le résultat trié dans le même fichier **`passwdCopie`**.

---

## Exercice 2

1. Écrire la commande qui permet de compter le nombre d'utilisateurs qui ont pour shell le `/bin/bash`. Vous trouverez cette information dans le fichier `/etc/passwd`. À l'exécution de la commande, on veut un résultat comme ceci:
```bash
11 utilisateurs ont pour shell /bin/bash
```

```bash
$ echo "$(grep -c '/bin/bash' /etc/passwd) utilisateurs ont pour shell /bin/bash"
```

**Explication :**
- `grep -c '/bin/bash' /etc/passwd` : Cherche toutes les lignes contenant **`/bin/bash`** dans le fichier **`/etc/passwd`** et renvoie le nombre de correspondances (l'option `-c` compte les lignes).
- `echo "$( ... )"` : Affiche le résultat avec le texte personnalisé. Le nombre d'utilisateurs est inséré dans le message.


{{% notice style="info" title="Notez que..." %}}
Le nombre d'utilisateurs pourrait être différent.
{{% /notice %}}

2. Maintenant on veut écrire la ligne de commande qui permet d’afficher le nombre d’utilisateurs qui ont pour shell par défaut un des shells disponibles sur votre machine. Pour cela, il faut parcourir le fichier `/etc/shells` **ligne par ligne** (**hint**: boucle). Vous y trouverez les shells disponibles. À l’exécution de la commande, on aurait pour chacun des shells un résultat de la même forme que le suivant:

```bash
0 utilisateurs ont pour shell /bin/sh
11 utilisateurs ont pour shell /bin/bash
0 utilisateurs ont pour shell /usr/bin/sh
0 utilisateurs ont pour shell /usr/bin/bash
```

{{% notice style="warning" title="Attention" %}}
Vous **ne devez pas** indiquer manuellement les noms des shells..
{{% /notice %}}

```bash
for shell in $(cat /etc/shells); do
    count=$(grep -c "^.*:$shell" /etc/passwd)
    echo "$count utilisateurs ont pour shell $shell"
done
```

**Explication :**
- `$(cat /etc/shells)` : Récupère tous les shells disponibles dans le fichier **`/etc/shells`**.
- `for shell in $(...)` : Parcourt chaque shell ligne par ligne.
- `grep -c "^.*:$shell" /etc/passwd` : Compte le nombre d'utilisateurs dont le shell correspond à l'élément `$shell` dans **`/etc/passwd`**. Le `^.*:` garantit que l'on regarde uniquement la partie correspondant au shell (après le `:` dans chaque ligne).
- `echo "$count utilisateurs ont pour shell $shell"` : Affiche le résultat pour chaque shell.

--- 

## Exercice 3

Pour cet exercice:
- **nomdurépertoire** est affiché automatiquement. 
- **N** est le nombre trouvé.

Référez-vous au cours de la semaine 2 sur [la commande ls -l](../../../semaine2/cours/#quelques-explications-du-résultat-de-ls--l)


1. En une seule ligne de commande, on veut savoir combien de dossiers contient le répertoire courant. Le résultat doit être affiché comme suit :
```bash
Le répertoire `nomdurépertoire` contient   N dossiers
```

```bash
echo "Le répertoire \`$(basename $PWD)\` contient $(find . -maxdepth 1 -type d | wc -l) dossiers"
```

**Explication :**
- `$(basename $PWD)` : Affiche le nom du répertoire courant (`$PWD` donne le chemin complet, et `basename` extrait uniquement le nom du répertoire).
- `find . -maxdepth 1 -type d` : Recherche tous les dossiers (`-type d`) dans le répertoire courant (`.`) sans descendre dans les sous-répertoires (`-maxdepth 1`).
- `wc -l` : Compte le nombre de lignes retournées par `find`, soit le nombre de dossiers.
- `echo` : Affiche le résultat avec le format spécifié.

2. En une seule ligne de commande, on veut savoir combien de fichiers standards contient le répertoire courant. Le résultat doit être affiché comme suit :
```bash
Le répertoire `nomdurépertoire` contient   N fichiers standards
```

3. En une seule ligne de commande, on veut savoir combien d’éléments ne sont ni des dossiers ni des fichiers standards dans le répertoire courant. Le résultat doit être affiché comme suit :
```bash
Le répertoire `nomdurépertoire` contient   N fichiers qui ne sont ni standards ni des répertoires
```

4. Écrire une commande qui récupère le nom du **dernier utilisateur** qui a été créé sur votre machine (c'est celui qu'on retrouve à la **dernière ligne** du fichier `/etc/passwd`). Le résultat doit être stocké dans une variable nommée `nomUtilisateur`.

5. En utilisant la variable `nomdurépertoire` qui contient le nom du dernier utilisateur défini dans `/etc/passwd`, écrivez une commande permettant de :
    - Rechercher tous les fichiers du système (*find*)
    - Lister leurs détails avec `ls -l`
    - Filtrer uniquement les fichiers appartenant à cet utilisateur.
    - Filtrer uniquement les fichiers standards. 
    - La commande doit être une seule ligne en utilisant un pipe (`|`) et une boucle `while read`.

---

## Exercice 4

1. En tant qu’utilisateur standard, On veut trouver tous les fichiers `.txt` sur votre disque dur (**ne pas utiliser `sudo`**). Écrire la commande qui permet de retrouver cette information **sans afficher les erreurs**.

2. Récupérer la sortie standard de la commande précédente et à partir de son résultat, **lire chaque ligne** et à l'aide de la commande `ls`, afficher la taille de ces fichiers suivi du chemin vers les fichiers.(**en une seule commande sans utiliser de variable**)
Résultat attendu:
```bash
0 /home/mot/dossier2/fichier4.txt
0 /home/mot/dossier3/fichier2.txt
0 /home/mot/dossier3/fichier3.txt
0 /home/mot/dossier3/fichier4.txt
79 /home/mot/prof.txt
```

3. Récupérer la sortie standard de la commande précédente et trier le résultat par **ordre croissant de taille**. (**en une seule commande sans utiliser de variable**)