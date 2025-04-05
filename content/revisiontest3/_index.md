+++
title = "TEST #3 - Informations et notions à maitriser"
weight = 95
+++

{{% notice style="warning" title="Revenez me voir" %}}
D'ici le test #3 (<span style="color:red;">lundi 14 avril</span>), revenez sur cette page fréquemment, pour prendre connaissance des ajouts et/ou modifications.

***Ne vous limitez pas à cette page pour vous préparer au test #3, car certaines notions du cours ne s'y trouvent pas***.
{{% /notice %}}

# **Informations** 

- **Date**: Lundi 14 avril
- **Durée**: 1h40
- **Format**: Test sur Moodle
- **Documentation permise**: 2 feuilles recto-verso (manuscrites ou imprimées)
- **Matière**: Semaine #6 à #9 incluses (#7 uniquement des questions théoriques)


# **Semaine 6: Expressions régulières (regexp)**

## **Commandes de base**
| Commande | Description |
|----------|-------------|
| `cat`    | Affiche le contenu d’un fichier |
| `sed`    | Édite un fichier en ligne (remplacements, suppressions...) |
| `grep`   | Recherche des lignes contenant un motif |
| `egrep`  | Version améliorée de `grep`, accepte les regex étendues |


## **Motifs de base**
| Motif | Signification |
|-------|----------------|
| `ab`  | Chaîne exacte "ab" |
| `.`   | N'importe quel caractère |
| `^`   | Début d’une ligne |
| `$`   | Fin d’une ligne |


## **Quantificateurs**
| Symbole     | Signification |
|-------------|---------------|
| `?`         | 0 ou 1 fois |
| `+`         | 1 ou plusieurs fois |
| `*`         | 0 ou plusieurs fois |
| `{n}`       | Exactement n fois |
| `{n,m}`     | De n à m fois |
| `{n,}`      | Au moins n fois |


## **Ensembles de caractères**
| Syntaxe          | Signification |
|------------------|---------------|
| `[abc]`          | Un seul caractère : a, b ou c |
| `[^abc]`         | Tout sauf a, b ou c |
| `[a-z]`          | Lettre minuscule |
| `[A-Z]`          | Lettre majuscule |
| `[0-9]`          | Chiffre |
| `[a-zA-Z0-9]`    | Alphanumérique |

> **⚠️** Un ensemble correspond à *un seul* caractère.


## **Groupes**
- `(abc)` : groupe de caractères
- `(ab)*` : zéro ou plusieurs répétitions de "ab"
- `(ab)+` : au moins une répétition de "ab"


## **Opérateurs logiques**
| Symbole | Fonction |
|---------|----------|
| `\|`    | OU logique entre motifs |
  
```bash
  $ egrep 'ssh|ftp' /etc/services # Filtrer les lignes contenant "ssh" ou "ftp"
  $ egrep '^#|s$' /etc/services  # Filtrer les commentaires ou les lignes se terminant par "s"
```

## **Échappement**
- Pour rechercher un **symbole spécial**, on l’échappe avec `\`
  - Ex : `\.` pour un point littéral
  - Ex : `\$` pour le symbole dollar


## **Espaces blancs**
| Motif | Signification |
|-------|---------------|
| `\s`  | Espace, tab, retour à la ligne |
| `\S`  | Tout sauf un espace blanc |


## **Regex utile – URL Web**
```regex
https?://[a-zA-Z0-9\.-]+\.[a-zA-Z]{2,4}(/\S*)?
```
- **`https?://`** : HTTP ou HTTPS  
- **`[a-zA-Z0-9\.-]+`** : nom de domaine  
- **`\.[a-zA-Z]{2,4}`** : extension  
- **`(/\S*)?`** : chemin facultatif


## **Exemples pratiques avec egrep**
| Objectif | Commande |
|----------|----------|
| Lignes contenant `ssh` | `egrep 'ssh' fichier` |
| Commentaires (`#`)     | `egrep '^#' fichier` |
| Finissant par `s`      | `egrep 's$' fichier` |
| Contient `a` puis un char, puis `z` | `egrep 'a.z' fichier` |
| Ligne commençant par chiffre | `egrep '^[0-9]' fichier` |
| Exclure les lignes commençant par `#` | `egrep '^[^#]' fichier` |

---


# **Semaine 7: Vim et les fichiers de configuration**

## 1. **Modes de VIM**
- **Mode normal** : Par défaut, pour les commandes (copier, supprimer, naviguer). Retourner en mode normal avec `Échap` (ESC).
- **Mode visuel** : Pour sélectionner du texte.
  - `v` : Sélectionner par caractère.
  - `V` : Sélectionner par ligne.
- **Mode insertion** : Pour ajouter ou modifier du texte.
  - `i` : Insérer avant le curseur.
  - `a` : Insérer après le curseur.
  - `I` : Insérer au début de la ligne.
  - `A` : Insérer à la fin de la ligne.


## 2. **Navigation dans VIM**
- Un caractère à gauche : `h`
- Un caractère à droite : `l`
- Une ligne en bas : `j`
- Une ligne en haut : `k`
- Un mot à droite : `w`
- Un mot à gauche : `b`
- Début de la ligne : `0`
- Fin de la ligne : `$`
- Aller à une ligne précise : `:numéro` (ex. `:100`)

*Astuce :* Ajoutez un quantificateur pour répéter une commande, ex. `3w` (avance de 3 mots).


## 3. **Commandes de base**
- **Copier** : `y`
  - Une ligne : `yy`
  - Jusqu’à la fin du mot : `yw`
  - Trois lignes : `3yy`
- **Coller** : `p` (après) / `P` (avant)
  - Copier 3 mots : `y3w`
  - Coller 3 fois : `3p`
- **Modifier du texte** :
  - Remplacer un caractère : `r` + (caractère)
  - Remplacer plusieurs caractères : `R` (mode remplacement)
- **Annuler et répéter** :
  - Annuler : `u` (undo)
  - Répéter : `.`
- **Supprimer (couper)** :
  - Supprimer un caractère sous le curseur : `x`
  - Supprimer avant le curseur : `X`
  - Supprimer une ligne : `dd`
  - Supprimer jusqu’à la fin du mot : `dw`
  - Supprimer jusqu’à la fin de la ligne : `d$`


## 4. **Fichiers de configuration Linux**
- **Réseau** :
  - `/etc/resolv.conf` : Serveurs DNS.
  - `/etc/hosts` : Noms de machine et adresses IP.
- **Personnalisation du shell** :
  - `~/.bashrc` : Alias, par exemple `alias lh="ls -lh"`.
- **Autres fichiers utiles** :
  - `/etc/selinux/config` : Sécuriser avec SELinux.
  - `/etc/passwd` et `/etc/group` : Gestion des utilisateurs et groupes.
  - `/etc/locale.conf` : Définir la langue du système.
  - `/etc/fstab` : Configurer le montage des partitions.
  - `/etc/httpd/conf/httpd.conf` : Configurer Apache.
  - `/etc/grub2.cfg` : Configurer le gestionnaire de démarrage.

---

# **Semaine 8: DNF et CRON**

## **Cron**

### **Qu’est-ce que *cron* et *crontab* ?**
- `cron` = planificateur de tâches automatique sous Linux.
- `crontab` = fichier contenant les tâches planifiées d’un utilisateur.
- Les crontabs sont stockées dans : `/var/spool/cron/`
- Le démon qui exécute les tâches : `crond`.


#### **Commandes essentielles**

| Commande | Description |
|---------|-------------|
| `crontab -l` | Affiche les tâches de l'utilisateur |
| `crontab -e` | Ouvre/modifie la crontab dans un éditeur |
| `crontab -r` | Supprime **toutes** les tâches (⚠️ irréversible) |
| `sudo crontab -u <utilisateur> -l` | Voir les tâches d’un autre utilisateur |
| `crontab <fichier>` | Charge des tâches depuis un fichier (**écrase** l’ancienne crontab) |


### **Syntaxe d’une tâche *cron***

```bash
* * * * * commande_ou_script
```

| Champ | Signification | Valeurs |
|-------|----------------|---------|
| 1     | Minute         | 0–59    |
| 2     | Heure          | 0–23    |
| 3     | Jour du mois   | 1–31    |
| 4     | Mois           | 1–12    |
| 5     | Jour de semaine| 0–7 (0/7 = dimanche) |

#### **Opérateurs utiles**
- `*` = chaque unité de temps
- `,` = liste (ex: `1,3,5`)
- `-` = intervalle (ex: `9-17`)
- `*/n` = toutes les n unités (ex: `*/2` = toutes les 2 heures)


### **Exemples utiles**

| Objectif | Tâche cron |
|---------|-------------|
| Chaque jour à 14h30 | `30 14 * * * bash /chemin/script.sh` |
| Toutes les 2 heures | `0 */2 * * * bash /chemin/script.sh` |
| Tous les lundis à midi | `0 12 * * 1 bash /chemin/script.sh` |
| Chaque heure en mars | `25 * * 3 * bash /chemin/script.sh` |

📌 **Scripts = toujours avec le chemin absolu !**


## **DNF : gestionnaire de paquets** (Fedora, AlmaLinux…)

| Tâche | Commande |
|-------|----------|
| Installer un paquet | `sudo dnf install -y <paquet>` |
| Supprimer un paquet | `sudo dnf remove <paquet>` |
| Mettre à jour tous les paquets | `sudo dnf update` |
| Voir les mises à jour sans les installer | `dnf check-update` |
| Mettre à jour un paquet | `sudo dnf update <paquet>` |


### **Rechercher / explorer des paquets**

| Objectif | Commande | Exemple |
|----------|----------|---------|
| Lister paquets installés | `dnf list installed` | |
| Rechercher par mot-clé | `dnf search <mot>` | `dnf search editor` |
| Obtenir info sur un paquet | `dnf info <nom>` | `dnf info httpd` |
| Trouver le paquet lié à une commande | `dnf provides <chemin>` | `dnf provides /bin/cat` |


### **Gestion des dépôts**

| Tâche | Commande |
|-------|----------|
| Voir les dépôts actifs | `dnf repolist` |
| Voir tous les dépôts | `dnf repolist all` |
| Ubuntu ? Installer dnf : | `sudo apt install dnf` |


### **Groupes de paquets**

| Tâche | Commande |
|-------|----------|
| Lister les groupes | `dnf grouplist` |
| Voir info d’un groupe | `dnf groupinfo "Nom du groupe"` |
| Installer un groupe | `sudo dnf groupinstall "Nom du groupe"` |


### **Shell interactif **dnf***

| Tâche | Commande |
|-------|----------|
| Lancer le shell | `dnf shell` |
| Script d’install automatique | `dnf shell <fichier>` |
| Exécuter sans confirmation | `dnf -y shell <fichier>` |

---

# **Semaine 9: Variables, paramètres de script et structure conditionnelle IF**

## 1. **Opérations mathématiques en Bash**

- **Addition** : `+`
- **Soustraction** : `-`
- **Multiplication** : `*`
- **Division entière** : `/` (pas de décimales)
- **Puissance** : `**`
- **Modulo** (reste) : `%`

**Exemples** :
```bash
let "a = 5 + 3"  # Addition
let "a = 4 * 3"  # Multiplication
let "a = 3 ** 2" # Puissance
let "a = 10 / 3" # Division entière, résultat: 3
let "a = 10 % 3" # Modulo, résultat: 1
```

## 2. **Variables de paramètres dans les scripts**

- `$#` : Nombre de paramètres
- `$0` : Nom du script
- `$1` à `$9` : Paramètres 1 à 9
- `$?` : Code de retour de la dernière commande
- `$*` : Liste de tous les paramètres

**Exemple** :
```bash
bash script.sh param1 param2 param3
```

## 3. **Tester des conditions avec la commande *test***

### Tests sur les chaînes de caractères :
- `test -z "$var"` : Vrai si la variable est vide
- `test -n "$var"` : Vrai si la variable n'est pas vide
- `test "$var" = "chaine"` : Vrai si la variable est égale à "chaine"
- `test "$var" != "chaine"` : Vrai si la variable est différente de "chaine"

### Tests sur les nombres :
- `-eq` : égal
- `-ne` : différent
- `-lt` : inférieur
- `-gt` : supérieur
- `-le` : inférieur ou égal
- `-ge` : supérieur ou égal

### Tests sur les fichiers :
- `-e` : Existe
- `-s` : Non vide
- `-f` : Fichier standard
- `-d` : Répertoire
- `-r` : Lecture autorisée
- `-w` : Écriture autorisée
- `-x` : Exécution autorisée

**Exemple** :
```bash
test "$a" -ne "$b"; echo $? # Affiche 0 si vrai
```

## 4. **Structure conditionnelle *if...then...elif ...else***

- Syntaxe de base :
```bash
if [ condition 1 ]
then
  # commandes à exécuter si la condition 1 est vraie
    elif [ condition 2]
       # commande à exécuter si la condition 2 est vraie
    else
       # commande à exécuter si la commande 2 est fausse
else
  # commandes à exécuter si la condition 1 est fausse
fi
```

- Exemple avec les paramètres :
```bash
if [ $# -ne 0 ]
then
    elif [ $# -le 2 ] || [ $# -ge 4 ]
         echo "Il y a moins de 3 paramètres ou plus de 3 paramètres
    else
         echo "Il y a 3 paramètres en ligne de commande"
else
  echo "Pas de paramètres"
fi
```

## 5. **Lire des Entrées Clavier avec *read***

- **Commande** : `read variable`
- **Avec message** (option `-p`) :
```bash
read -p "Entrez votre prénom : " prenom
```

**Exemple d’utilisation** :
```bash
echo "Entrez un nombre"
read nb1
echo "Entrez un autre nombre"
read nb2
```

## 6. **Notations et remarques Importantes**
- Toujours entourer les variables par des guillemets `""` pour éviter les erreurs (espaces, chaîne vide).
- La commande `test` ou les crochets `[]` peuvent être utilisés pour les conditions.
- La syntaxe de `if` nécessite des espaces après le `[` et avant le `]`.




