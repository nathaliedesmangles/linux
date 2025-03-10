+++
title = "Les expressions régulières"
weight = 61
+++

## Introduction aux expressions régulières

Dans l'univers Linux, la manipulation des fichiers texte est une tâche essentielle. Parmi les outils utilisés pour ce faire, on trouve notamment :

- **`cat`** : pour afficher le contenu des fichiers,
- **`sed`** : pour les transformations textuelles,
- **`grep`** : pour rechercher et filtrer des lignes.

Avec **`grep`**, vous pouvez filtrer un texte pour ne conserver que les lignes contenant un mot ou une expression donnée, ou bien les exclure. Mais comment faire si vous souhaitez rechercher des motifs plus complexes, comme des adresses e-mail ou des numéros de téléphone ? C'est ici qu'interviennent les **expressions régulières**, un outil puissant pour décrire des motifs précis et identifier des textes ayant une structure particulière.

### Exemple : URL Web

Un exemple d'expression régulière pour capturer une URL Web :

```
https?://[a-zA-Z0-9\.-]+\.[a-zA-Z]{2,4}(/\S*)?
```

---

## Premiers pas avec les expressions régulières

Voici quelques motifs de base et leurs significations :

| **Motif**   | **Description**                            | **Exemple**                  | **Contre-exemple**            |
|-------------|--------------------------------------------|------------------------------|-------------------------------|
| `ab`        | Recherche la chaîne exacte "ab".           | "ab"                         | "a", "b", chaîne vide         |
| `.`         | Correspond à n'importe quel caractère.     | "a", "b"                     | "ab", chaîne vide             |
| `^`         | Indique le début d'une ligne.              | `^a` : un "a" au début.      | Toute ligne ne commençant pas par "a".   |
| `$`         | Indique la fin d'une ligne.                | `a$` : un "a" à la fin.      | Toute ligne ne se terminant pas par "a". |

---

### Commandes pratiques avec *egrep*

La commande **`egrep`** est une version avancée de `grep`, qui prend en charge les expressions régulières étendues (ERE).

- **Rechercher les lignes contenant "ssh" dans un fichier :**
  ```bash
  $ egrep 'ssh' /etc/services
  ```

- **Rechercher uniquement les commentaires (lignes commençant par `#`) :**
  ```bash
  $ egrep '^#' /etc/services
  ```

- **Rechercher les lignes se terminant par "s" :**
  ```bash
  $ egrep 's$' /etc/services
  ```

- **Rechercher les lignes contenant "a" et "z" séparées par un caractère quelconque :**
  ```bash
  $ egrep 'a.z' /etc/services
  ```

---

## Opérateurs logiques

### Le OU (**|**)

L'opérateur **`|`** permet de rechercher des lignes contenant l'une ou l'autre des expressions spécifiées.

- **Exemple : Filtrer les lignes contenant "ssh" ou "ftp" :**
  ```bash
  $ egrep 'ssh|ftp' /etc/services
  ```

- **Filtrer les commentaires ou les lignes se terminant par "s" :**
  ```bash
  $ egrep '^#|s$' /etc/services
  ```

---

## Ensembles de caractères

Les **ensembles** permettent de rechercher plusieurs possibilités similaires en regroupant des caractères entre crochets `[ ]`.

- **Exemple : Rechercher "loucher", "toucher", "doucher", ou "coucher" :**
  ```bash
  $ egrep '[ltdc]oucher' fichier
  ```

- **Exclure ces mots tout en recherchant ceux contenant "oucher" :**
  ```bash
  $ egrep '[^ltdc]oucher' fichier
  ```

### Intervalles

| **Ensemble**     | **Description**                          |
|------------------|------------------------------------------|
| `[a-z]`          | Toutes les lettres minuscules.           |
| `[A-Z]`          | Toutes les lettres majuscules.           |
| `[0-9]`          | Tous les chiffres.                       |
| `[a-zA-Z0-9]`    | Tous les caractères alphanumériques.     |

{{% notice style="warning" title="Important"  %}}
 - Un ensemble décrit un seul caractère.
{{% /notice %}}


- **Rechercher des mots contenant un "f" et un "p" séparés par une lettre minuscule :**
  ```bash
  $ egrep 'f[a-z]p' /etc/services
  ```

- **Rechercher les lignes commençant par un chiffre :**
  ```bash
  $ egrep '^[0-9]' /etc/services
  ```

- **Exclure les commentaires :**
  ```bash
  $ egrep '^[^#]' /etc/services
  ```

---

## Quantificateurs

Les quantificateurs précisent le nombre de répétitions d'un motif.

| **Quantificateur** | **Signification**             |
|--------------------|-------------------------------|
| `?`                | 0 ou 1 fois.                  |
| `+`                | 1 ou plusieurs fois.          |
| `*`                | 0 ou plusieurs fois.          |
| `{n}`              | Exactement n fois.            |
| `{n,m}`            | Entre n et m fois.            |
| `{n,}`             | Au moins n fois.              |

- **Rechercher "www" dans un texte :**
  ```bash
  $ egrep 'w{3}' fichier
  ```

- **Rechercher "http" ou "https" :**
  ```bash
  $ egrep 'https?' fichier
  ```

- **Rechercher une lettre minuscule répétée entre 3 et 6 fois :**
  ```bash
  $ egrep '[a-z]{3,6}' fichier
  ```

---

## Groupes

Les **groupes** permettent de regrouper des parties d'expressions avec des parenthèses `( )`. Cela permet d'appliquer un quantificateur ou de réutiliser le groupe.

- **Exemple :**
  ```
  (ab)*c
  ```
  Correspond à : "zéro ou plusieurs 'ab', suivi d'un 'c'". Cela capture "c", "abc", "ababc", etc.

---

## Échappement

Pour rechercher des caractères ayant une signification spéciale dans les expressions régulières (`.`, `+`, `*`, etc.), il faut les **échapper** avec un antislash (\).

- **Exemple : Rechercher les lignes se terminant par un point :**
  ```bash
  $ egrep '\.$' fichier
  ```

---

## Exercices pratiques

1. Trouvez les numéros de cartes de crédit valides (16 chiffres, commençant par 4540 et sans 9 dans le dernier groupe) :

   ```
   4540 6010 4510 8888
   5440 5010 6610 1010
   4540 7010 4428 5490
   4540 8523 4013 1314
   4540 8710 5410 1012 1314
   ```

2. Identifiez les noms de variables valides (lettres, chiffres, underscores, mais ne commençant pas par un chiffre) :

   ```
   Abcd
   abcd_
   var123
   _var2
   1nombre
   ```

3. Recherchez les adresses IPv4 valides (quatre nombres entre 0 et 255, séparés par des points) :

   ```
   1.240.40.15
   2.256.20.190
   192.168.255.255
   300.200.100.10
   30.40.50.60
   192.168.2
   10.10.10.10.10
   ```

