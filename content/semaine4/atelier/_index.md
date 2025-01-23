+++
title = "ATELIER #4: Redirection, E/S, pipeline, filtres et while"
weight = 42
+++

## Objectifs de l'atelier

- Se familiariser avec les entrées/sorties et la redirection des commandes.
- Combinaison de commandes.
- Filtrage de données.
- Utilisation de l'itération avec la boucle While.

---

# Atelier


{{% notice style="tip" title="Astuce" %}}
- Pour effectuer des opérations simple, vous pouvez utiliser la commande `bc` de cette façon: 
{{% /notice %}}

```bash
$ echo 7-3 | bc
```

## Exercice 1

1. Ouvrez une session avec l’utilisateur standard et reproduisez, dans le répertoire courant, l'arborescence suivante et ce en utilisant un maximum de trois commandes : 
 
```
├── H2025
│   ├── Linux
│   │   ├── Cours
│   │   └── Ateliers
│   └── Virtualisation
│       └── machines
└── Personnel
```

2. Changez de répertoire en allant dans le dossier Notes. 
3. En saisissant une seule commande, créez, à l’intérieur du répertoire courant, les dossiers semaine1, semaine2, …semaine15. Vous **ne devez pas** à entrer tous les noms de semaines dans la commande. 
4. En une seule commande, faites-en-sorte que dans chacun des dossiers précédents (semaine1..), un fichier est créé et qui contient la ligne suivante :
<mark>Ce cours concerne la semaineN</mark>

Où `N` correspond au numéro de la semaine. 

5. Toujours à partir du répertoire courant, utilisez le chemin relatif pour copier dans le dossier Travaux le fichier `passwd` qui est dans `/etc`. 
6. Toujours à partir du répertoire courant et en utilisant le chemin relatif, renommez le fichier copié en ajoutant « Copie » à son nom (`passwdCopie`)
7. Changez le caractère délimiteur du fichier `passwdCopie` par `;`
8. Triez le contenu du fichier `passwdCopie` en ordre croissant du numéro de groupe, soit le quatrième champ. On veut que le fichier soit trié et non uniquement le résultat retourné par la commande. 

---

## Exercice 2

- Écrire la ligne de commande qui permet d’afficher le nombre d’utilisateurs qui ont pour shell par défaut un des shells disponibles sur votre machine. 
À l’exécution de la commande, on aurait pour chacun des shells un résultat de la même forme que le suivant:

```
0 utilisateurs ont pour shell /bin/sh
11 utilisateurs ont pour shell /bin/bash
0 utilisateurs ont pour shell /usr/bin/sh
0 utilisateurs ont pour shell /usr/bin/bash
```

**Vous ne devez pas indiquer manuellement les noms des shells.**

--- 

## Exercice 3

1. On veut savoir combien de dossiers et de fichiers standards et combien d’éléments qui ne sont ni des dossiers ni des fichiers standards contient le répertoire courant. Le résultat doit être affiché comme suit :

```
Le répertoire nomdurépertoire contient   N dossiers
Le répertoire nomdurépertoire contient   N fichiers standards
Le répertoire nomdurépertoire contient   N fichiers qui ne sont ni standards ni des répertoires
```

- **nomdurépertoire** est affiché automatiquement. 
- **N** est le nombre trouvé. 

2. On veut afficher la liste de tous les fichiers standards (de toute l’arborescence) portant le nom du dernier utilisateur créé sur votre machine. Les messages d’erreurs sont redirigés vers `/dev/null`.

---

## Exercice 4

En une seule ligne de commande, trouvez tous les fichiers txt sur votre disque dur en tant qu’utilisateur standard et sans afficher les erreurs, afficher la taille de ces fichiers avec les unités  et classer les par ordre de taille croissante.

---

## Exercice 5: Caractères génériques et commande find

1. Aller dans le répertoire `/etc`. Ne vous déplacez pas pour le reste de cet exercice.
2. En utilisant la commande `find`, chercher les fichiers dont le nom commence par la lettre **r** à partir du répertoire courant.
3. Chercher tous les fichiers dont le nom contient la chaîne de caractères "rc" à partir du répertoire courant.
4. Afficher tous les fichiers dont le nom comporte trois caractères sur tout le système.
