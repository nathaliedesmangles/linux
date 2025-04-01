+++
title = "Atelier 9"
weight = 179
draft = true
+++

# Solution des exercices

## Exercices 1 

### Solution 1: Paramètres entrés sur la ligne de commande

1. **Création du script `param3.sh` :**
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
resultat=$(( (paramPlusGrand / paramPlusPetit) * $3 ))

# Affichage du résultat
echo "L'expression ($paramPlusGrand / $paramPlusPetit) * $3 donne : $resultat"
```

#### Explications :
- `if [ $# -ne 3 ]`: Vérifie que trois paramètres sont fournis.
- `paramPlusGrand` et `paramPlusPetit` sont déterminés avec une simple condition.
- La division entière est effectuée avec `/`.
- L'opérateur `*` réalise la multiplication.

#### Exemple d'exécution :
```bash
$ bash param3.sh 5 10 3
L'expression (10 / 5) * 3 donne : 6
```


### Solution 2: Paramètres entrés par l'utilisateur

1. **Création du script `param3.sh` avec saisie interactive :**
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
resultat=$(( (paramPlusGrand / paramPlusPetit) * param3 ))

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

---

## Exercice 3

### Partie 1: calcul.sh

### Partie 2: calculV2.sh



