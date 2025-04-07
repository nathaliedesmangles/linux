+++
title = "Atelier 9"
weight = 179
+++

# Solution des exercices

## Exercices 1 

### Solution 1: Paramètres entrés sur la ligne de commande

```bash
#!/bin/bash

# Vérification que trois paramètres sont fournis
if [ $# -ne 3 ]; then
    exit 1
fi

# Détermination du plus grand et du plus petit
if [ $1 -gt $2 ]; then
    paramPlusGrand=$1
    paramPlusPetit=$2
else
    paramPlusGrand=$2
    paramPlusPetit=$1
fi

# Division entière et calcul final
let "resultat = (paramPlusGrand / paramPlusPetit) * $3"

# Affichage du résultat
echo "L'expression ($paramPlusGrand / $paramPlusPetit) * $3 donne : $resultat"
```

#### Explications :
- `if [ $# -ne 3 ]`: Vérifie que trois paramètres sont fournis.
- `paramPlusGrand` et `paramPlusPetit` sont déterminés avec une simple condition.
- Le calcul est effectué à l'aide de `let`
   - La division entière est effectuée avec `/`.
   - L'opérateur `*` réalise la multiplication.

#### Exemple d'exécution :
```bash
$ bash param3.sh 5 10 3
L'expression (10 / 5) * 3 donne : 6
```


### Solution 2: Paramètres entrés par l'utilisateur

```bash
#!/bin/bash

# Saisie des paramètres par l'utilisateur
read -p "Entrez le premier nombre : " param1
read -p "Entrez le deuxième nombre : " param2
read -p "Entrez le troisième nombre : " param3

# Détermination du plus grand et du plus petit
if [ $param1 -gt $param2 ]; then
    paramPlusGrand=$param1
    paramPlusPetit=$param2
else
    paramPlusGrand=$param2
    paramPlusPetit=$param1
fi

# Division entière et calcul final
let "resultat = (paramPlusGrand / paramPlusPetit) * param3"

# Affichage du résultat
echo "L'expression ($paramPlusGrand / $paramPlusPetit) * $param3 donne : $resultat"
```

#### Explications :
- `read` permet la saisie interactive des valeurs.
L'option **`-p`** de la commande `read` dans les scripts Bash permet **d'afficher un message avant la saisie de l'utilisateur**. Elle sert à guider l'utilisateur en lui indiquant quoi entrer. 
   ```bash
   read -p "Message à afficher : " variable
   ``` 
   - **`-p`** : Affiche le message spécifié sans retour à la ligne.  
   - **`variable`** : Stocke la valeur saisie par l'utilisateur.  
- `paramPlusGrand` et `paramPlusPetit` sont déterminés avec une condition simple.
- Le calcul est effectué à l'aide de `let`
   - La division entière est effectuée avec `/` et l'opérateur `*` réalise la multiplication.

#### Exemple d'exécution :
```bash
$ bash param3.sh
Entrez le premier nombre : 5
Entrez le deuxième nombre : 10
Entrez le troisième nombre : 3
L'expression (10 / 5) * 3 donne : 6
```
---

## Exercice 2  

```bash
#!/bin/bash

# Demande à l'utilisateur d'entrer le chemin du fichier
read -p "Entrez le chemin du fichier à vérifier : " fichier

# Vérification si le fichier existe
if [ -e "$fichier" ]
then
   # Vérification si c'est un fichier standard
   if [ -f "$fichier" ]
   then
       echo "$fichier est un fichier standard."
   else
       echo "$fichier n'est pas un fichier standard."
   fi

   # Vérification des droits d'accès
   [ -r "$fichier" ] && echo "lecture : oui" || echo "lecture : non"
   [ -w "$fichier" ] && echo "écriture : oui" || echo "écriture : non"
   [ -x "$fichier" ] && echo "exécution : oui" || echo "exécution : non"
else
    echo "Le fichier $fichier n'existe pas."
    exit 1
fi
```

### Explications :
- `-e` vérifie si le fichier existe.
- `-f` vérifie si c'est un fichier standard.
- `-r`, `-w`, `-x` vérifient respectivement les droits de lecture, écriture et exécution.

### Exemples d'exécution :

**#1**
```bash
$ bash testFichier.sh
Entrez le chemin du fichier à vérifier : /etc/passwd
/etc/passwd est un fichier standard.
lecture : oui
écriture : non
exécution : non
```

**#2**
```bash
$ bash testFichier.sh
Entrez le chemin du fichier à vérifier : /etc
/etc n'est pas un fichier standard.
lecture : oui
écriture : non
exécution : oui
```


**#3**
```bash
$ bash testFichier.sh
Entrez le chemin du fichier à vérifier : ./test.txt
./test.txt est un fichier standard.
lecture : oui
écriture : oui
exécution : non
```

**#4**
```bash
$ bash testFichier.sh
Entrez le chemin du fichier à vérifier : /etc/passssswd
Le fichier /etc/passssswd n'existe pas.
```

**#5**
```bash
$ bash testFichier.sh
Entrez le chemin du fichier à vérifier : 
Le fichier  n'existe pas.
```

---

## Exercice 3

### Partie 1: calcul.sh

```bash
#!/bin/bash

# Vérification qu'il y a 3 paramètres 
if [ $# -ne 3 ]
then
    exit 1
fi

# Vérification de l'opérateur et calcul
if [ "$1" = "+" ]; then
    let "resultat = $2 + $3"
elif [ "$1" = "-" ]; then
    let "resultat = $2 - $3"
elif [ "$1" = "^" ]; then
    let "resultat = $2 ** $3"
else
    echo "Opérateur invalide. Utilisez +, - ou ^."
    exit 1
fi

# Affichage du résultat
echo "$2 $1 $3 = $resultat"
```

### Exemple d'exécution :
```bash
$ bash calcul.sh + 4 6
4 + 6 = 10
$ bash calcul.sh - 4 6
4 - 6 = -2
$ bash calcul.sh ^ 4 6
4 ** 6 = 4096
```


### Partie 2: calculV2.sh

```bash
#!/bin/bash

# Vérification qu'il y a 3 paramètres 
if [ $# -ne 3 ]
then
    # Demande des paramètres à l'utilisateur
    read -p "Entrez un opérateur (+, -, ^) : " operateur
    read -p "Entrez le premier nombre : " nombre1
    read -p "Entrez le deuxième nombre : " nombre2

    # Affichage du résultat
    echo "$nombre1 $operateur $nombre2 = $resultat"

else
    # Vérification de l'opérateur et calcul
    if [ "$1" = "+" ]; then
       let "resultat = $2 + $3"
    elif [ "$1" = "-" ]; then
       let "resultat = $2 - $3"
    elif [ "$1" = "^" ]; then
       let "resultat = $2 ** $3"
    else
        echo "Opérateur invalide. Utilisez +, - ou ^."
        exit 1
    fi

    # Affichage du résultat
    echo "$2 $1 $3 = $resultat"
```

### Exemple d'exécution :
```bash
$ bash calculV2.sh + 4 6
4 + 6 = 10
$ bash calculV2.sh - 4 6
4 - 6 = -2
$ bash calculV2.sh ^ 4 6
4 ^ 6 = 4096

$ bash calculV2.sh
Entrez un opérateur (+, -, ^) : +
Entrez le premier nombre : 4
Entrez le deuxième nombre : 6
4 + 6 = 10

bash calculV2.sh
Entrez un opérateur (+, -, ^) : -
Entrez le premier nombre : 4
Entrez le deuxième nombre : 6
4 - 6 = -2

bash calculV2.sh
Entrez un opérateur (+, -, ^) : ^
Entrez le premier nombre : 4
Entrez le deuxième nombre : 6
4 ^ 6 = 4096
```

