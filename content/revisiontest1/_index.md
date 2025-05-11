+++
title = "TEST #1-Quelques notions à maitriser"
weight = 35
+++

{{% notice style="warning" title="Revenez me voir" %}}
***Ne vous limitez pas à cette page pour vous préparer au test #2, car certaines notions du cours ne s'y trouvent pas***.
{{% /notice %}}

# Semaine 2

## Structure hiérarchique de Linux

Le système de fichiers Linux est organisé **comme un arbre inversé** :

* Le sommet est la **racine `/`**
* Tout (fichiers, dossiers, périphériques) est situé en dessous.

**Exemple :**

```
/
├── home
│   └── utilisateur
│       └── Documents
├── bin
├── etc
```


## Tout est fichier

Sous Linux, **tout est vu comme un fichier**, même les périphériques :

| Élément          | Est un fichier ? |
| ---------------- | ---------------- |
| Un fichier texte | ✅                |
| Un dossier       | ✅                |
| Une clé USB      | ✅                |
| Un disque dur    | ✅                |


## Répertoires principaux

Voici les plus importants, avec des exemples simples :

| Répertoire | Rôle                                     | Exemple               |
| ---------- | ---------------------------------------- | --------------------- |
| `/`        | Racine principale                        | `cd /` va au sommet   |
| `/home`    | Dossiers des utilisateurs                | `cd /home/paul`       |
| `/bin`     | Commandes de base comme `ls`, `cp`, `mv` | `ls /bin`             |
| `/etc`     | Fichiers de configuration système        | `cat /etc/hosts`      |
| `/dev`     | Fichiers pour les périphériques          | `ls /dev/sda`         |
| `/tmp`     | Fichiers temporaires                     | `touch /tmp/test.txt` |

---

## Chemins absolus vs relatifs

* **Chemin absolu** : Commence par `/`, donne l’adresse complète.
  → Ex : `/home/paul/fichier.txt`

* **Chemin relatif** : Dépend d'où vous êtes.
  → Ex : `Documents/fichier.txt` (si vous êtes déjà dans `/home/paul`)

**Commandes utiles** :

```bash
pwd     # Où suis-je ?
cd ..   # Revenir au dossier parent
cd ~    # Aller à mon dossier personnel
```


## Le Shell (Bash)

Le **shell** est l'interface texte où vous tapez des commandes.

* `$` : utilisateur standard
* `#` : super-utilisateur (root)

**Structure d’une commande** :

```bash
commande [options] [arguments]
```

**Exemples** :

```bash
whoami             # Affiche votre nom d'utilisateur
date -R            # Date formatée
sudo ls /root      # Affiche le contenu de /root avec droits admin
```

**Astuce** : Si vous vous trompez de commande → faites `Ctrl+C` pour annuler.

---

## Navigation avec Bash

| Commande | Action                        | Exemple                       |
| -------- | ----------------------------- | ----------------------------- |
| `pwd`    | Affiche le répertoire courant | `/home/paul`                  |
| `cd`     | Change de répertoire          | `cd Documents`                |
| `ls`     | Liste le contenu d’un dossier | `ls -l` pour voir les détails |

---

## Créer, supprimer, copier, déplacer

| Commande | Action              | Exemple                   |
| -------- | ------------------- | ------------------------- |
| `touch`  | Crée un fichier     | `touch test.txt`          |
| `mkdir`  | Crée un dossier     | `mkdir dossier`           |
| `rm`     | Supprime un fichier | `rm test.txt`             |
| `cp`     | Copie un fichier    | `cp test.txt copie.txt`   |
| `mv`     | Déplace ou renomme  | `mv test.txt nouveau.txt` |


## Lire des fichiers

| Commande | Usage                   | Exemple              |
| -------- | ----------------------- | -------------------- |
| `cat`    | Affiche tout le contenu | `cat notes.txt`      |
| `less`   | Lecture page par page   | `less longtexte.txt` |
| `head`   | Début du fichier        | `head fichier.txt`   |
| `tail`   | Fin du fichier          | `tail fichier.txt`   |

---

## À retenir

* Linux est structuré proprement sous `/`.
* Tout est fichier, même le matériel.
* Les chemins et commandes sont puissants mais simples.
* Bash permet d’automatiser et d’exécuter des tâches.
* Apprendre les commandes de base vous rend **autonome** dans Linux.

# Semaine 3

## Le processus de démarrage Linux : étapes essentielles

1. **BIOS/UEFI**
   → Vérifie le matériel et trouve un disque avec un secteur de démarrage.
   *Exemple : l’ordinateur s’allume et cherche le disque dur.*

2. **Chargeur d’amorçage (GRUB)**
   → Permet de choisir quel système démarrer.
   *Exemple : menu où vous choisissez "Ubuntu" ou "Windows".*

3. **Noyau Linux**
   → Lance les pilotes et un mini-système (`initramfs`).
   *Exemple : le noyau sait gérer la souris, clavier, etc.*

4. **`systemd` (ou `init`)**
   → Lance les services (réseau, interface graphique...).
   *Exemple : le Wi-Fi est activé automatiquement.*

5. **Écran de connexion**
   → Vous entrez votre nom d'utilisateur et mot de passe.

6. **Système prêt à l'emploi**
   → Vous pouvez utiliser le système et exécuter des commandes comme `shutdown`.


## *Runlevels* et *Targets*

Linux utilise maintenant des **cibles** (`targets`) pour gérer les modes de fonctionnement.

| But                  | Commande                       |
| -------------------- | ------------------------------ |
| Redémarrer           | `systemctl isolate reboot`     |
| Mode texte (console) | `systemctl isolate multi-user` |
| Mode graphique       | `systemctl isolate graphical`  |

**Défaut au démarrage** :

```bash
$ systemctl get-default
```

**Différence** :

* `set-default` : pour le prochain démarrage.
* `isolate` : effet immédiat.


## Substitution de commande

Permet d’insérer **le résultat d’une commande** dans une autre :

```bash
$ touch $(whoami).txt
```

👉 Crée un fichier nommé avec votre identifiant (ex: `nathalie.txt`)


## Variables et expansion

Créer une variable :

```bash
$ nom="toto"
```

Utiliser son contenu :

```bash
$ echo $nom
toto
```

Stocker une commande :

```bash
$ date=$(date)
$ echo "Nous sommes le $date"
```


## Caractères génériques

* `*` → remplace tout (ex : `*.txt` pour tous les fichiers texte)
* `?` → remplace un seul caractère (ex : `t?ti.txt` → `titi.txt`, `toti.txt`)


## Expansion d’accolades

Crée rapidement plusieurs fichiers ou dossiers.

```bash
$ touch test{1..3}.txt
```

👉 Crée `test1.txt`, `test2.txt`, `test3.txt`

```bash
$ mkdir -p boite{1,2}/fichier{a,b,c}
```

👉 Crée deux dossiers (`boite1`, `boite2`) contenant chacun trois fichiers.




