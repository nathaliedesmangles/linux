+++
title = "TEST #4: Résumés"
weight = 133
+++

# Informations

- **Date** : jeudi 8 mai
- **Durée** : 1h40, X questions (X à confirmer)
- **Format** : Test Moodle
- **Documentation permise** : 1 feuille recto-verso (manuscrites ou imprimées)

---

# Semaine #10: Utilisateurs et groupes

## 1. Utilisateurs

### Qu'est-ce qu'un utilisateur ?

- Une **entité** (personne ou processus) ayant un compte sur le système.
- Identifié par un **UID (User ID)**.
- Possède des **droits** et **permissions** spécifiques.

### Types de comptes

- **root (UID 0)** : super-utilisateur, tous les droits.
- **nobody (UID 65534)** : compte très limité.
- **Systèmes / applications (UID 1-999)** : pour les services, avec permissions minimales.
- **Comptes standards (UID ≥ 1000)** : pour les utilisateurs humains.

### Commandes importantes

- **`useradd`** : création d’un utilisateur.
- **`passwd`** : changement de mot de passe.
- **`userdel`** : suppression d’un utilisateur (`-r` pour supprimer son dossier personnel).
- **`usermod`** : modification d’un utilisateur (groupe, shell, répertoire, etc.).
- **`id`**, **`groups`** : voir UID/GID et groupes.

### Détails techniques

- Le groupe principal est créé automatiquement et associé aux fichiers créés.
- Le répertoire personnel est copié depuis **`/etc/skel`**.
- Le mail est stocké dans **`/var/spool/mail`**.
- Le mot de passe est **chiffré** dans **`/etc/shadow`**.

---

## 2. Groupes

### Qu'est-ce qu’un groupe ?

- Un **ensemble d’utilisateurs** partageant les mêmes permissions.
- Identifié par un **GID (Group ID)**.
- Utilisé pour **gérer collectivement** les permissions.

### Types de groupes

- **root (GID 0)**
- **nobody (GID 65534)**
- **Groupes système (GID 1 - 999)**
- **Groupes standards (GID ≥ 1000)**

### Groupe principal vs secondaire

- **Groupe principal** : utilisé lors de la création de fichiers (défini dans `/etc/passwd`).
- **Groupes secondaires** : ajoutent des permissions supplémentaires.
- Un utilisateur ne peut avoir **qu'un seul groupe principal**, mais il peut avoir **plusieurs groupes secondaires**.

### Commandes importantes

- **`groupadd`** : créer un groupe.
- **`groupdel`** : supprimer un groupe.
- **`groupmod`** : renommer ou modifier un groupe.
- **`usermod -g`** : changer le groupe principal d’un utilisateur.
- **`usermod -aG`** : ajouter à l'utilisateur, un ou plusieurs groupes secondaires.
- **`usermod -G`** : remplacer les groupes secondaires existants par un ou plusieurs autres groupes secondaires.
---

## Commandes clés à retenir

| Tâche | Commande |
|------|---------|
| Créer un utilisateur | `useradd nom` |
| Modifier un utilisateur | `usermod` (avec options) |
| Supprimer un utilisateur | `userdel` (avec `-r` pour supprimer le dossier) |
| Créer un groupe | `groupadd nom` |
| Supprimer un groupe | `groupdel nom` |
| Ajouter à un groupe secondaire | `usermod -aG groupe utilisateur` |
| Afficher UID/GID | `id` |
| Afficher les groupes | `groups utilisateur` |


## Points d’attention

- **Le mot de passe** n’est pas créé automatiquement lors de la création d'un utilisateur.
- **Impossible de supprimer un groupe s’il est groupe principal d’un utilisateur.**
- **`usermod -d`** ne déplace pas automatiquement les fichiers du répertoire personnel.


# Semaine #11: Droits d'accès

### Lire les permissions

La commande :
```bash
$ ls -l
```
affiche les **permissions sous forme symbolique**, ex. : `-rwxr-xr--`

Structure :
```
[ type ][ u ][ g ][ o ]
     -   rwx  r-x  r--
```

Signification des lettres (**les droits**) :
- `r` : lecture (read)
- `w` : écriture (write)
- `x` : exécution (execute) — aussi "traverser" un dossier

Signification des lettres (**les utilisateurs**)
-  `u`  : User (propriétaire)  
-  `g`  : Group (groupe propriétaire) 
- `o`   : Other (autres utilisateurs)
- `a`   : All (tous les utilisateurs) 

### Modifier les permissions (avec *chmod*)

Deux méthodes :

####  1. Méthode **symbolique**

- `chmod u+x fichier` → ajoute exécution à l'utilisateur
- `chmod go-w fichier` → retire écriture au groupe et autres
- `chmod a=r fichier` → définit lecture seule pour tous
- `chmod -R u-x dir/` → applique récursivement

####  2. Méthode **octale**

Basée sur la valeur binaire des permissions :
| Droit | Valeur |
|-------|--------|
| r     | 4      |
| w     | 2      |
| x     | 1      |

### Tableau des permissions Linux

| **Catégorie** | **Droit** | **Symbole** |**Valeur (binaire) | **Valeur (octale)** | **Effet sur un fichier** | **Effet sur un répertoire** |
|---------------|-----------|-------------|----------------------|---------------|---------------------------|------------------------------|
| Lecture        | read      | `r`         |  1 0 0   | 4                    | Lire le contenu           | Voir la liste des fichiers   |
| Écriture       | write     | `w`         |  0  1 0 | 2                    | Modifier / supprimer      | Créer ou supprimer des fichiers |
| Exécution      | execute   | `x`         |  0 0 1 | 1                    | Exécuter un script        | Accéder (entrer dans le dossier) |


### Exemples de permissions octales

| **Commande**         | **Symbolique**   | **Signification**                          |
|----------------------|------------------|--------------------------------------------|
| `chmod 777 fichier`  | `rwxrwxrwx`      | Tous les droits pour tous                 |
| `chmod 755 fichier`  | `rwxr-xr-x`      | Propriétaire : tout, autres : lecture+exécution |
| `chmod 644 fichier`  | `rw-r--r--`      | Propriétaire : lecture+écriture, autres : lecture |
| `chmod 700 fichier`  | `rwx------`      | Seul le propriétaire a tous les droits     |
|`chmod -R 777 dir/`  |`rwxrwxrwx`   | tous les droits, récursivement |

### Changer le propriétaire  (avec *chown*)

Seul `root` peut le faire :

```bash
$ chown user fichier
$ chown user:group fichier
$ chown -R user dir/
```

#### Changer le groupe ( avec *chgrp*)

Peut être fait par :
- `root`
- ou le propriétaire du fichier (s’il appartient au groupe visé)

```bash
$ chgrp group fichier
$ chgrp -R group dir/
```

### Le droit d’exécution (***x***)

- **Sur un fichier** : permet d’exécuter un script ou programme.
- **Sur un dossier** : permet d’y entrer (`cd`), mais pas de lister son contenu sans `r`.

Pour exécuter un script :
```bash
$ chmod +x script.sh
$ ./script.sh
```
Le `./` indique un **chemin relatif** (exécuter un fichier du répertoire courant)


### La variable ***$PATH***

- Liste des répertoires où le système cherche les commandes
- Voir son contenu :
```bash
$ echo $PATH
```
- Ajouter un chemin temporairement :
```bash
$ export PATH=$PATH:/chemin/vers/dossier
```
- Pour le rendre **permanent** : ajouter la ligne dans le fichier `.bashrc` ou le fichier `.bash_profile`

### Spécifier l’interpréteur d’un script

En haut du fichier, on ajoute :
```bash
#!/bin/bash
```

## À retenir

- `r`, `w`, `x` : lecture, écriture, exécution
- `chmod` : modifier les permissions
- `chown`, `chgrp` : modifier propriétaire et groupe
- `./` : exécuter un script du répertoire courant
- `$PATH` : répertoires contenant les commandes accessibles globalement


### Commandes courantes

| **But**                              | **Commande**                              |
|-------------------------------------|-------------------------------------------|
| Donner tous les droits à tous       | `chmod a+rwx fichier`                     |
| Enlever le droit d’écriture à tous sauf au propriétaire | `chmod go-w fichier`              |
| Rendre un script exécutable         | `chmod +x script.sh`                      |
| Changer le propriétaire             | `chown utilisateur fichier`              |
| Changer le groupe                   | `chgrp groupe fichier`                   |
| Changer les deux                    | `chown utilisateur:groupe fichier`       |
| Voir les permissions                | `ls -l`                                   |

---

# Semaine #12: Réseau

## Commandes essentielles

| Commande                    | Rôle                                                           |
|-----------------------------|----------------------------------------------------------------|
| `ip a`                      | Affiche les interfaces réseau et leurs adresses IP             |
| `ip addr add <IP>`          | Ajoute une adresse IP temporaire à une interface               |
| `ip addr del <IP>`          | Supprime une adresse IP                                        |
| `ip route`                  | Affiche la table de routage                                    |
| `ip route add default via`  | Définit une passerelle par défaut                              |
| `nmcli`                     | Gère les connexions réseau (NetworkManager)                    |
| `nmcli con show`            | Liste les connexions                                           |
| `nmcli con mod`             | Modifie les paramètres d’une connexion                         |
| `nmcli con add`             | Crée une nouvelle connexion                                    |
| `nmcli con up/down`         | Active ou désactive une connexion                              |
| `ifconfig`                  | Ancienne commande pour afficher/configurer les interfaces      |
| `ping <adresse>`            | Teste la connectivité réseau                                   |
| `cat /etc/resolv.conf`      | Montre les serveurs DNS utilisés                               |


## Fichiers importants

| Fichier                        | Rôle                                                               |
|--------------------------------|--------------------------------------------------------------------|
| `/etc/hosts`                   | Associe adresses IP et noms locaux                                 |
| `/etc/resolv.conf`             | Contient les serveurs DNS utilisés                                 |
| `/etc/sysconfig/network-scripts/ifcfg-*` | Fichiers de configuration réseau (RedHat, CentOS, etc.)  |
| `/etc/network/interfaces`      | Fichier réseau (Debian/Ubuntu)                                     |


## À retenir

- Les commandes `ip` modifient **temporairement** la configuration
- Pour une configuration **persistante**, utilisez `nmcli` ou modifiez les fichiers.
- Le fichier `/etc/hosts` permet d’attribuer des noms locaux (utile pour les pings).
- Le DNS est défini dans `/etc/resolv.conf`.
- Toujours **redémarrer le réseau** ou la connexion après une modification.

---

# Semaine #13: Gestion des disques


## Étapes essentielles 

```
1. Ajouter le disque (réel ou virtuel)
2. Créer les partitions → fdisk /dev/sdX
3. Formater la partition → mkfs -t ext4 /dev/sdX1
4. Créer un répertoire vide → mkdir /mnt/data
5. Monter la partition → mount /dev/sdX1 /mnt/data
6. (Optionnel) Montage permanent → /etc/fstab
7. Démonter la partition → umount /dev/sdX1 /mnt/data
```

## Schéma visuel simplifié 

```
[ Nouveau disque ]
        ↓
/dev/sdb   ← Apparaît comme fichier bloc
        ↓
[ Partitionnement ]
→ /dev/sdb1  /dev/sdb2
        ↓
[ Formatage ]
→ mkfs.ext4 /dev/sdb1
        ↓
[ Montage ]
→ mount /dev/sdb1 /mnt/data
        ↓
[ Utilisation ]
→ Écriture/lecture dans /mnt/data
        ↓
(Optionnel)
→ /etc/fstab → montage automatique au démarrage
        ↓
[ Démontage ]
→ umount /dev/sdb1 /mnt/data

```

## Quelques commandes utiles :

| Objectif                  | Commande                            |
|---------------------------|-------------------------------------|
| Lister les disques        | `ls /dev/sd*` ou `fdisk -l`         |
| Créer une partition       | `fdisk /dev/sdb`                    |
| Formater une partition    | `mkfs.ext4 /dev/sdb1`               |
| Monter une partition      | `mount /dev/sdb1 /mnt/data`         |
| Démonter une partition    | `umount /dev/sdb1 /mnt/data`        |
| Voir les montages actifs  | `df -h`                             |
| Tester le fichier fstab   | `mount -a`                          |


