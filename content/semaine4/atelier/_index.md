+++
title = "ATELIER #4: Commandes utiles, redirection, chainage, filtres et boucle while"
weight = 42
+++

## Objectifs de l'atelier

- Utiliser les commandes `tree`, `grep`, `sep`, `cut`, `more`, `less` et `sort`.
- Rediriger les résultats de commandes.
- Enchainer les commandes.
- Filtrer des données de fichiers ou répertoires.
- Itérer sur des résultats de commandes avec la boucle While.

---

# Atelier


{{% notice style="tip" title="Astuce" %}}
- Pour réaliser les exercices, vous aurez besoin de regarder les différentes commandes vues en cours (commandes et boucles). 
- Vous **devrez consulter les pages de manuel** (commande `man`) des différentes commandes pour trouver la façon de réaliser ce que vous souhaitez.
- Pour effectuer des opérations simple, vous pouvez utiliser la commande `bc` de cette façon: 
{{% /notice %}}

```bash
$ echo 7-3 | bc
```

## Exercice 1

1. Ouvrir une session avec l’utilisateur standard et reproduire, dans le répertoire courant, l'arborescence suivante et ce en utilisant un **maximum de trois commandes** : 
 
```
├── H2025
│   ├── Linux
│   │   ├── Cours
│   │   └── Ateliers
│   └── Virtualisation
│       └── machines
└── Icones
```

2. Changer de répertoire en allant dans le dossier **Cours**. Pour le reste des question de cet exercice, rester dans le répertoire **Cours**.

3. En saisissant une seule commande, créer, à l’intérieur du répertoire courant, les dossiers semaine1, semaine2, …, semaine15. Vous **ne devez pas** entrer tous les noms de semaines dans la commande (**hint**: expansion d'accolades). 

4. À l'aide d'une **boucle for**, à l'intérieur de chaque dossier **semaine**, créer un fichier .txt qui contient la phrase suivante :
<mark>Ce cours concerne la semaineN</mark>

Où `N` correspond au numéro de la semaine. 

5. Toujours à partir du répertoire courant, utiliser un **chemin relatif** pour copier dans le dossier **ateliers** le fichier **`passwd`** qui est dans **`/etc`**. 

6. Toujours à partir du répertoire courant et en utilisant le chemin relatif, renommer le fichier copié en ajoutant "Copie" à son nom (`passwdCopie`).

7. Changer toutes les occurrences du caractère délimiteur `:` (deux points) du fichier `passwdCopie` par `;` (point-virgule).

8. Trier le contenu du fichier `passwdCopie` en ordre croissant du numéro de groupe, soit le quatrième champ. On veut que le fichier soit trié et non uniquement le résultat retourné par la commande. 
{{% notice style="info" title="Hint" %}}
Utilisez la commande `man` pour trouver les options de la commande `sort` qui vous aideront à accomplir la tâche demandée.
{{% /notice %}}

---

## Exercice 2

{{% notice style="warning" title="Attention" %}}
Revenir dans votre dossier personnel.
{{% /notice %}}


1. Écrire la commande qui permet de compter le nombre d'utilisateurs qui ont pour shell le `/bin/bash`. Vous trouverez cette information dans le fichier `/etc/passwd`. À l'exécution de la commande, on veut un résultat comme ceci:
```bash
11 utilisateurs ont pour shell /bin/bash
```

{{% notice style="info" title="Notez que..." %}}
Le nombre d'utilisateurs pourrait être différent.
Utilisez la commande `man` pour trouver l' option de la commande `grep` qui vous aidera à accomplir la tâche demandée.
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

--- 

## Exercice 3

{{% notice style="warning" title="Attention" %}}
Revenir dans votre dossier personnel.
{{% /notice %}}

Pour cet exercice:
- **nomdurépertoire** est affiché automatiquement. 
- **N** est le nombre trouvé.

Référez-vous au cours de la semaine 2 sur [la commande ls -l](../../../semaine2/cours/#quelques-explications-du-résultat-de-ls--l)


1. En une seule ligne de commande, on veut savoir combien de **fichiers et dossiers** contient le répertoire courant. Le résultat doit être affiché comme suit :
```bash
Le répertoire `nomdurépertoire` contient N fichiers et dossiers
```

2. En une seule ligne de commande, on veut savoir combien de **fichiers standards** contient le répertoire courant. Le résultat doit être affiché comme suit :
```bash
Le répertoire `nomdurépertoire` contient N fichiers standards
```

3. En une seule ligne de commande, on veut savoir combien d’éléments ne sont **ni des dossiers ni des fichiers standards** dans le répertoire courant. Le résultat doit être affiché comme suit :
```bash
Le répertoire `nomdurépertoire` contient N fichiers qui ne sont ni standards ni des répertoires
```

4. Écrire une commande qui récupère le nom du **dernier utilisateur** qui a été créé sur votre machine (c'est celui qu'on retrouve à la **dernière ligne** du fichier `/etc/passwd`). Le résultat doit être stocké dans une variable nommée `nomUtilisateur`.

5. En utilisant la variable `nomdurépertoire` qui contient le nom du dernier utilisateur défini dans `/etc/passwd`, écrivez une commande permettant de :
    - Rechercher tous les fichiers à partir de `/home` (*find*)
    - Lister leurs détails avec `ls -l`
    - Filtrer uniquement les fichiers appartenant à cet utilisateur.
    - Filtrer uniquement les fichiers standards. 
    - La commande doit être une seule ligne en utilisant un pipe (`|`) et une boucle `while read`.

{{% notice style="info" title="Hint" %}}
Utilisez la commande `man` pour trouver les options des commandes `find` et `ls` qui vous aideront à accomplir la tâche demandée.
{{% /notice %}}

---

## Exercice 4

{{% notice style="info" title="Hint" %}}
Pour les #2 et #3, Utilisez la commande `man` pour trouver les options de la commande `sort` qui vous aideront à accomplir la tâche demandée.
{{% /notice %}}

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