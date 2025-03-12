+++
title = "Tableaux récapitulatifs des symboles des regexp"
weight = 610
+++

Ces tableaux couvrent **les symboles essentiels** pour utiliser les expressions régulières !

## **1. Opérateurs spéciaux (métacaractères)**  
| **Symbole** | **Signification** | **Exemple** | **Correspondances** |
|------------|-----------------|-------------|-----------------|
| `.` | N'importe quel caractère sauf un saut de ligne | `a.b` | `acb`, `a1b`, `a_b` |
| `^` | Début de ligne | `^Hello` | `Hello world` (valide), `Salut Hello` (non valide) |
| `$` | Fin de ligne | `end$` | `C'est la fin` |
| `[...]` | Un seul caractère parmi ceux spécifiés | `[aeiou]` | `a`, `e`, `o` |
| `[^...]` | Un seul caractère **sauf** ceux spécifiés | `[^aeiou]` | `b`, `c`, `x` (tout sauf voyelles) |
| `(xyz)` | Capture un groupe | `(abc)` | `abc` (capture complète) |
| `\|` | OU logique | `chien\|chat` | `chien`, `chat` |
| `\s` | Un espace blanc (y compris tabulation, retour à la ligne) | `\s+` → `"   "` | `[ \t\n\r\f\v]`|
| `\S` | Tous **sauf** un espace blanc (y compris tabulation, retour à la ligne) | `\S+` → `"abc"` | `[^ \t\n\r\f\v]` (Tout sauf les espaces)|

---

## **2. Quantificateurs**  
| **Symbole** | **Signification** | **Exemple** | **Correspondances** |
|------------|-----------------|-------------|-----------------|
| `*` | 0 ou plusieurs fois | `ab*c` | `ac`, `abc`, `abbc` |
| `+` | 1 ou plusieurs fois | `ab+c` | `abc`, `abbc` mais pas `ac` |
| `?` | 0 ou 1 fois (optionnel) | `colou?r` | `color`, `colour` |
| `{n}` | Exactement `n` répétitions | `[0-9]{4}` | `2025`, `1234` |
| `{n,}` | Au moins `n` fois | `[0-9]{2,}` | `12`, `456`, `7890` |
| `{n,m}` | Entre `n` et `m` fois | `[0-9]{2,4}` | `12`, `123`, `4567` |

---

## **3. Séquence d’échappement**  
| **Symbole** | **Signification** | **Exemples** |
|------------|-----------------|-------------|
| `\` | Échappe un métacaractère | `\.` → correspond à `.` (point) <br> `\+` → correspond au symbole `+`, <br> `\$` → correspond au symbole `$` <br>etc.|

