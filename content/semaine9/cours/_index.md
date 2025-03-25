+++
title = "Variables, paramètres et if_then_else_fi"
weight = 91
+++

## Effectuer des opérations mathématiques

En Bash, les variables stockent des **chaînes de caractères par défaut**, ce qui empêche la manipulation directe des nombres. Pour effectuer des calculs, nous utilisons la commande `let`.

### Opérations arithmétiques disponibles :

- Addition : `+`
- Soustraction : `-`
- Multiplication : `*`
- Division entière : `/`
- Puissance : `**`
- Modulo (reste de la division entière) : `%`

#### Exemples :
```bash
#!/bin/bash

a=5
b=2
let "c = a + b"
```

Autres exemples :
```bash
#!/bin/bash

let "a = 4 * 3"
let "a = 3 ** 2"
let "a = 12 / 2"
let "a = 10 / 3"
let "a = 10 % 3"
```
- `10 / 3` donne `3` car la division est entière.
- `10 % 3` donne `1` car 10 divisé par 3 laisse un reste de 1.

On peut aussi écrire des opérations sous forme abrégée :
```bash
#!/bin/bash

let "a = a * 3"  # Équivaut à :
let "a *= 3"
```

## Variables et paramètres

Les scripts Bash peuvent accepter des paramètres en ligne de commande :
```bash
./script.sh param1 param2 param3
```

Les variables associées :

- `$#` : Nombre de paramètres.
- `$0` : Nom du script exécuté.
- `$1, $2, ..., $9` : Paramètres de 1 à 9.
- `$?` : Code de retour de la dernière commande (0 = succès).
- `$*` : Liste des paramètres.

## Test de conditions

La commande `test` permet d’évaluer des conditions. Le résultat est stocké dans `$?` (0 = vrai, autre valeur = faux).

### Tests sur les chaînes de caractères

```bash
#!/bin/bash

test -z "$variable"  # Vrai si la variable est vide
test -n "$variable"  # Vrai si la variable n'est pas vide
test "$variable" = "chaine"  # Vrai si les valeurs sont identiques
test "$variable" != "chaine"  # Vrai si les valeurs sont différentes
```

### **Rappel**: Tests sur les valeurs numériques

Les comparaisons sont faites avec :

- `-eq` : Égal
- `-ne` : Différent
- `-lt` : Inférieur
- `-gt` : Supérieur
- `-le` : Inférieur ou égal
- `-ge` : Supérieur ou égal

Exemple :
```bash
#!/bin/bash

a=10
b=20
test "$a" -ne "$b"; echo $?
test "$a" -eq "$b"; echo $?
```

### Tests sur les fichiers

Syntaxe : `test option fichier`

- `-e` : Existence du fichier
- `-s` : Fichier non vide
- `-f` : Fichier normal
- `-d` : Répertoire
- `-r` : Lecture autorisée
- `-w` : Écriture autorisée
- `-x` : Exécution autorisée

## Structure conditionnelle *if ... then ... else ... fi*

Syntaxe :
```bash
#!/bin/bash

if [ condition ]
then
  commandes_si_vrai
else
  commandes_si_faux
fi
```

Exemple :
```bash
#!/bin/bash

if [ $# -ne 0 ]
then
  echo "Il y a des paramètres en ligne de commande"
  echo "Nombre de paramètres : $#"
  echo "Paramètres : 1=$1 2=$2 3=$3 4=$4"
  echo "Liste : $*"
else
  echo "Pas de paramètres"
fi
```

Autre exemple :
```bash
#!/bin/bash

if [ $1 -gt $2 ]
then
  echo "Le premier paramètre est supérieur au deuxième"
elif [ $1 -lt $2 ]
then
  echo "Le premier paramètre est inférieur au deuxième"
else
  echo "Les deux nombres sont égaux"
fi
```

### Tester l'existence d'un fichier

```bash
#!/bin/bash

if [ -e "$1" ]
then
  echo "Le fichier existe"
else
  echo "Le fichier n'existe pas"
fi
```

## Lire une entrée clavier

Pour stocker une entrée utilisateur dans une variable :
```bash
read nombre
```

Modification du script précédent pour lire les nombres au clavier :
```bash
#!/bin/bash

echo "Entrez un nombre"
read nb1
echo "Entrez un autre nombre"
read nb2

if [ "$nb1" -gt "$nb2" ]
then
  echo "Le premier nombre est supérieur au deuxième"
elif [ "$nb1" -lt "$nb2" ]
then
  echo "Le premier nombre est inférieur au deuxième"
else
  echo "Les deux nombres sont égaux"
fi
```

