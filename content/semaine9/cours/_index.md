+++
title = "Variables, paramètres et if_then_else_fi"
weight = 91
+++


## Les opérations mathématiques en Bash

Bash, le shell de commande sous Linux, ne traite pas les nombres de manière native. Toutes les variables sont considérées comme des chaînes de caractères. Pour effectuer des opérations mathématiques, on utilise des commandes spécifiques comme `let`.

La commande `let` permet d'exécuter des opérations arithmétiques simples.

**Exemple :**
```bash
$ a=5
$ b=2
$ let "c = a + b"
$ echo $c
7
```

### Opérations et opérateurs disponibles

- Addition : `+`
- Soustraction : `-`
- Multiplication : `*`
- Division entière : `/` (les décimales sont ignorées)
- Puissance : `**`
- Modulo : `%` (renvoie le reste de la division)

**Exemples :**
```bash
let "a = 4 * 3"  # Multiplication
let "a = 3 ** 2" # Puissance
let "a = 12 / 2" # Division entière
let "a = 10 / 3" # Division entière, résultat : 3
let "a = 10 % 3" # Modulo, résultat : 1
```

On peut aussi utiliser la notation raccourcie :
```bash
let "a *= 3" # Équivaut à : let "a = a * 3"
```

## Variables de paramètres dans les scripts

Les scripts Bash acceptent des paramètres passés en ligne de commande, **lors de l'exécution du script**

```bash
bash script.sh param1 param2 param3
```

Une fois le script lancé, Linux crée **automatiquement** des variables.

### Variables créées automatiquement

- `$#` : Nombre de paramètres
- `$0` : Nom du script exécuté
- `$1` à `$9` : Valeurs des paramètres 1 à 9
- `$?` : Code de retour de la dernière commande (0 si succès)
- `$*` : Liste de tous les paramètres

## Tester des conditions avec la commande *test*

La commande `test` permet de vérifier des conditions, et le résultat est stocké dans `$?` (0 si la condition est vraie).

### Tests sur les chaînes de caractères

| **Commande**                     | **Description**                               |
|----------------------------------|-----------------------------------------------|
| `test -z $variable`              | Vrai si `$variable` est **vide**.                 |
| `test -n $variable`              | Vrai si `$variable` n'est **pas vide**.           |
| `test $variable = "chaine"`      | Vrai si `$variable` est **identique à** "chaine". |
| `test $variable != "chaine"`     | Vrai si `$variable` est **différent de** "chaine".|

**Exemples**
```bash
$ test -z "$a"
$ echo $?
0            # car la variable "a" n'a pas été initialisée
$ a="abcd"
$ test -n "$a"
$ echo $?
0
$ test a = "abcd"
$ echo $?
0		# Vrai
$ test a != "dcba"
$ echo $?
0		# Vrai
```


{{% notice style="note" title="Note" %}}
Contrairement aux nombres, avec les chaînes de caractères les symboles `=` (égal) et `!=` (différent) sont utilisés comme opérateur d'égalité et d'inégalité.
{{% /notice %}}

### Tests sur les nombres

Les options disponibles sont :
- `-eq` : Égalité
- `-ne` : Différent
- `-lt` : Inférieur
- `-gt` : Supérieur
- `-le` : Inférieur ou égal
- `-ge` : Supérieur ou égal

**Exemple :**
```bash
a=10
b=20
test "$a" -ne "$b"; echo $? # Affiche 0 (vrai)
test "$a" -eq "$b"; echo $? # Affiche 1 (faux)
```

### Tests sur les fichiers

La syntaxe est test option `nom_fichier`

Les options:

- `-e` : Existe
- `-s` : Non vide
- `-f` : Fichier standard
- `-d` : Répertoire
- `-r` : Lecture autorisée
- `-w` : Écriture autorisée
- `-x` : Exécution autorisée

## Structure conditionnelle if...then...else

En Bash, la syntaxe correcte est :

```bash
if [ condition ]; then
    # commandes
fi
```

Il est aussi possible d’écrire sur deux lignes, dans ce cas on ne met pas le point-virgule (`;`) après la condition.
Ajout de "then" après les conditions :

```bash
if [ condition ]
then
  # Commandes à exécuter si la condition est vraie
else
  # Commandes à exécuter si la condition est fausse
fi
```

{{% notice style="note" title="Note" %}}
Les crochets remplacent la commande **`test`**. Vous pouvez utiliser l'un ou l'autre. 
Voici l'équivalent avec la commande `test` au lieu des crochets:
```bash
if test condition
then
  # Commandes à exécuter si la condition est vraie
else
  # Commandes à exécuter si la condition est fausse
fi
```
{{% /notice %}}

### Exemple 1: Nombre de paramètres

```bash
#!/bin/bash

if [ $# -ne 0 ]
then
  echo "il y paramètres en ligne de commande";
  echo "Nombre de paramètres:$#";
  echo "Paramètres: 1=$1 2=$2 3=$3 4=$4";
  echo "Liste : $*";
else
  echo "Pas de paramètres ";
fi
```

**Exécution du script** : sans paramètres 

![Exemple 1 if](./exemple1_if.png?width=45vw)

### Exemple 2: avec comparaisons

```bash
#!/bin/bash

if [ $1 -gt $2 ]
then
  echo "Le premier paramètre est supérieur au deuxième paramètre"
elif [ $1 -lt $2 ]
then
  echo "Le premier paramètre est inférieur au deuxième paramètre"
else
  echo "Les deux sont égaux"
fi
```

{{% notice style="note" title="Note" %}}
En bash, vous pouvez avoir autant de `elif` que vous voulez, tout comme en Java avec le `else if`.
{{% /notice  %}}

**Exécution du script** : en passant les paramètres 

![Exemple 2 if](./exemple2_if.png?width=45vw)

### Exemple 3: Tester si un fichier existe

```bash
#!/bin/bash

if [ -e $1 ]
then
  echo "Le fichier existe"
else
  echo "Le fichier n'existe pas"
fi
```

**Exécution du script** : avec le fichier /etc/passwd en paramètre 

![Exemple 3 if](./exemple3_if.png?width=45vw)


## Lire des entrées clavier (commande *read*)

### Exemple 4: Attendre la saisie au clavier de l'utilisateur

Pour lire une information saisie au clavier par l'utilisateur on utilise la commande `read`:

![Exemple 4 read](./exemple4_read.png?width=45vw)

### Exemple 5: Demander à l'utilisateur de saisir 2 nombres au clavier

```bash
#!/bin/bash

echo "Entrez un nombre"
read nb1
echo "Entrez un autre nombre"
read nb2

if [ $nb1 -gt $nb2 ]
then
  echo "Le premier nombre est supérieur au deuxième nombre"
elif [ $nb1 -lt $nb2 ]
then
  echo "Le premier nombre est inférieur au deuxième nombre"
else
  echo "Les deux nombres sont égaux"
fi
```

**Exécution du script** :

![Exemple 5 read](./exemple5_read.png?width=40vw)

### L'option -p de la commande *read*

L'option **`-p`** de la commande `read` permet **d'afficher un message avant la saisie de l'utilisateur**, pour lui indiquer quoi entrer.  

**Syntaxe générale** :
```bash
read -p "Message à afficher : " variable
```

- **`-p`** : Affiche le message spécifié sans retour à la ligne.  
- **`variable`** : Stocke la valeur saisie par l'utilisateur.  


**Exemple d’utilisation** :
```bash
#!/bin/bash

read -p "Entrez votre prénom : " prenom
echo "Bonjour, $prenom !"
```

**Résultat en exécutant le script :**
```bash
$ bash script.sh
Entrez votre nom : Nathalie
Bonjour, Nathalie !
```

