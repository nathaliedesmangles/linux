+++
title = "ATELIER #9: Tests, paramètres et opérations arithmétiques"
weight = 92
+++

## Objectifs de l'atelier

- Créer un script qui récupère trois valeurs numériques passées en paramètre, effectue des opérations mathématiques et affiche le résultat.
- Créer un script pour tester l’existence et les permissions d’un fichier.
- Créer des scripts permettant d’effectuer des opérations mathématiques à partir des arguments fournis.

---

# Atelier

{{% notice style="warning" title="ATTENTION" %}}
Aucun point ne sera accordé sans la remise des scripts (**fichiers .sh**) demandés.
{{% /notice %}}

## Exercice 1 : Manipulation de valeurs numériques

1. Créez un script `param3.sh` qui :
   - Récupère trois paramètres en entrée.
   - Détermine le plus grand et le plus petit des trois nombres.
   - Effectue la division entière du plus grand par le plus petit et stocke le résultat dans une variable.
   - Multiplie ce résultat par le troisième paramètre.
   - Affiche le résultat sous la forme :
     
     **"L'expression (paramPlusGrand / paramPlusPetit) * param3 donne : résultat"**

### Remise

- Le script `param3.sh`
- Une capture d’écran montrant son exécution avec les paramètres `5 10 3`

---

## Exercice 2 : Tests sur les fichiers

1. Écrivez un script `testFichier.sh` qui :
   - Vérifie si le fichier `/etc/passwd` est un fichier normal (et non un répertoire ou un lien symbolique).
   - Affiche un message indiquant si c'est un fichier normal ou non.
   - Affiche les droits d’accès sur ce fichier.

   ![HTTP](./l13-1.png?height=80&classes=border,shadow,inline)

### Remise

- Le script `testFichier.sh`
- Une capture d’écran montrant son exécution

---

## Exercice 3 : Opérations arithmétiques et tests sur les chaînes de caractères

1. Créez un script `calcul.sh` qui :
   - Accepte trois paramètres : deux nombres et un opérateur (`+`, `-`, `^`).
   - Réalise l’opération indiquée par l’opérateur.
   - Affiche le résultat de l’opération.
   - Retourne un code d'erreur `1` si le nombre de paramètres est incorrect.

   ![HTTP](./l13-2.png?height=100&classes=border,shadow,inline)

### Remise

- Le script `calcul.sh`
- Une capture d’écran montrant son exécution avec les paramètres `+ 4 6`, `- 4 6` et `^ 4 6`

---

### Amélioration du script :

2. Modifiez `calcul.sh` pour créer `calculV2.sh` qui :
   - Vérifie le nombre de paramètres.
   - Si le nombre de paramètres est incorrect, demande à l’utilisateur de saisir l’opérateur et les deux nombres.
   - Exécute ensuite l’opération comme dans `calcul.sh`.
   - Optimise le code pour éviter les répétitions inutiles.

   ![HTTP](./l13-3.png?height=150&classes=border,shadow,inline)

### Remise

- Le script `calculV2.sh`
- Une capture d’écran montrant les deux modes d’exécution du script avec les valeurs `+ 3 4`

