+++
title = "ATELIER #9: Tests, paramètres et opérations arithmétiques"
weight = 92
+++

## Objectifs de l'atelier

1. Créer un script qui récupère des valeurs numériques passées en paramètre et effectue des opérations mathématiques
2. Créer un script pour tester l’existence et les permissions d’un fichier.
3. Créer des scripts permettant d’effectuer des opérations mathématiques à partir des arguments fournis.

---

# Atelier

{{% notice style="warning" title="ATTENTION" %}}
1. Vous devez utiliser uniquement les commandes vues en classe jusqu’à maintenant. L’utilisation de commandes non couvertes entraînera la note de 0 pour cet exercice.
2. Aucun point ne sera accordé sans la remise des scripts (**fichiers .sh**) demandés.
{{% /notice %}}

## Exercice 1 : Manipulation de valeurs numériques

1. Créez un script `param3.sh` qui :
   - Récupère les **valeurs de trois paramètres en entrée**.
   - Détermine **le plus grand** et **le plus petit** des deux premiers paramètres.
   - Effectue la **division entière** du plus grand par le plus petit et stocke le résultat dans une variable.
   - Multiplie ce résultat par le **troisième paramètre**.
   - Affiche le résultat sous la forme :
     
     **"L'expression (paramPlusGrand / paramPlusPetit) * param3 donne : résultat"**

### Remise

- Le script `param3.sh`
- Une **capture d’écran** montrant son exécution avec les paramètres `5 10 3`

---

## Exercice 2 : Tests sur les fichiers

1. Écrivez un script `testFichier.sh` qui :
   - Vérifie si le fichier `/etc/passwd` est un **fichier standard** (et non un répertoire ou un lien symbolique).
   - Si oui → afficher : "/etc/passwd est un fichier standard".
   - Sinon → afficher : "/etc/passwd n'est pas un fichier standard".
2. Vérifier les droits d’accès :
   - Si on peut **lire** le fichier → afficher : "lecture : oui" / sinon "lecture : non"
   - Si on peut **écrire** dans le fichier → afficher : "écriture : oui" / sinon "écriture : non"
   - Si on peut **exécuter** le fichier → afficher : "exécution : oui" / sinon "exécution : non"

#### Remise

- Le script `testFichier.sh`
- Une capture d’écran montrant son exécution

---

## Exercice 3 : Opérations arithmétiques et tests sur les chaînes de caractères avec un script

Vous devez créer **deux scripts** : `calcul.sh` et `calculV2.sh` qui permettent de faire des opérations entre deux nombres.

### Partie 1. Le script *calcul.sh*

1. Créez un script `calcul.sh` qui reçoit trois paramètres :
   - un opérateur (+, -, ^)
   - un premier nombre
   - un deuxième nombre

2. Le script doit :
   - Vérifier que le **nombre de paramètres est exactement 3**.
      - Si ce n’est pas le cas → sortir avec un **code de retour 1** ( utiliser la commande **`exit 1`**)
   - Faire le calcul selon l’opérateur fourni :
      - `+` → addition
      - `-` → soustraction
      - `^` → puissance (ex: 4 ^ 6 = 4096)
   - Afficher le résultat (ex: 4+6=10)

#### Remise

- Le script `calcul.sh`
- Une **capture d’écran** montrant son exécution avec les paramètres:
   - `+ 4 6`
   - `- 4 6` 
   - `^ 4 6`

---

### Partie 2: Le script *calculV2.sh*

1. Faites une copie du script `calcul.sh` et renommez la copie `calculV2.sh`.
2. Modifiez le code du script `calculV2.sh` pour qu'il:
   - Vérifie le **nombre de paramètres**.
   - Si le nombre de paramètres est **différent de 3**, il doit demander à l’utilisateur de saisir 
       - l’opérateur et les deux nombres séparés par un espace.
3. Une fois les 3 valeurs obtenues, le script fait le calcul comme dans `calcul.sh`.


#### Remise

- Le script `calculV2.sh`
- Une **capture d’écran** montrant les deux façons d'utiliser le script:
    - En passant les 3 paramètres directement (ex: `bash calculV2.sh + 3 4`)
    - En les entrant à la main après le lancement (ex: `bash calculV2.sh`)

