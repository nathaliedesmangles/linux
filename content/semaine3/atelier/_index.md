+++
title = "ATELIER #3: Cibles et variables utilisateurs et for"
weight = 32
+++

## Objectifs de l'atelier

- Se familiariser avec les cibles (niveaux d'exécution).
- Comprendre les bases des variables utilisateur en Bash.
- Apprendre à manipuler et utiliser des variables pour stocker des résultats de commandes.
---

# Atelier 

## Exercice 1 : Manipuler les cibles (niveaux d'exécution)

1. Utiliser la commande `systemctl` pour passer en mode multi-utilisateur sans interface graphique
2. Vérifier que vous êtes maintenant en mode multi-utilisateur sans interface graphique.
3. Définir le mode multi-utilisateur avec interface graphique comme cible par défaut.
4. Redémarrer votre système pour vérifier que le mode graphique est bien la cible par défaut.

## Exercice 2 : Création et affichage de variables

1. Déclarez une variable `nom` avec votre prénom.
2. Affichez la valeur de la variable.
3. Essayez d’accéder à la variable sans `$`.
   - Notez la différence.

## Exercice 3 : Capturer une date formatée

1. Stockez la date actuelle dans une variable `date_actuelle` avec le format AAAA/MM/JJ hh:mm:ss.
2. Affichez la date formatée.

## Exercice 4 : Supprimer une variable

1. Déclarez une variable temporaire.
2. Supprimez la variable avec `unset`.
3. Essayez d’afficher la variable supprimée.

## Exercice 5: Expansion de variables et d'accolades

1. Créer une variable `variable_etc` contenant la liste des fichiers du répertoire `/etc` et l'afficher. 
- Son contenu est-il facile à lire ?
- Que se passe-t-il si vous exécutez `ls` suivi du nom de votre variable ? Pourquoi ?
2. Sachant que beaucoup de fichiers de configuration se terminent par `.conf`, les trouver et stocker leur nom dans une variable.
- Que se passe-t-il si vous exécutez `ls` suivi du nom de votre variable?
- Seriez-vous capable d’afficher la taille de chacun des fichiers de configuration ? La commande du `-sh <fichier>` permet d’afficher la taille de fichier.
3. Créer un répertoire dans lequel vous créerez les fichiers suivants à l’aide de la commande `touch` en utilisant la syntaxe permettant de factoriser une commande:
`test1.txt, test2.txt, test3.txt, test1.doc, test2.doc, test3.doc, test1.tot, test2.tot, test3.tot`
4. Grâce aux caractères génériques, n’afficher que les fichiers `.txt` qui commencent par `test` (plusieurs possibilités existent, essayez de les trouver).
a. Tous les fichiers `.txt et `.tot`.
b. Tous les fichiers test1

## Exercice 6: Expansion d’accolade et boucle for

- En faisant cet exercice, vérifiez pour cette question le résultat de vos commandes en utilisant la commande `tree`. 
- La figure ci-dessous montre un exemple d’utilisation de cette commande.
- Assurez-vous d’être revenu dans votre répertoire personnel

1. À l’aide d’une seule commande et en utilisant l’expansion d’accolade, créez l’arborescence des dossiers suivante :

![structure](atelier3.png)

2. À l’aide d’une seule commande et en utilisant l’expansion d’accolade, créer le fichier vide **priseNote** dans chaque répertoire **lab**.
3. À l’aide d’une boucle for, renommer les fichier **priseNote** en **priseNote.txt**.
4. À l’aide d’une boucle for, déplacer les fichiers **priseNote.txt** du répertoire **lab** vers le répertoire **leçon** correspondant.
