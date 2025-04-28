+++
title = "Gestion des disques"
weight = 131
+++

## Rappels

En Linux, il n’existe **qu’un seul système de fichiers** :  
**`/`** ← C’est la racine de tout.

Contrairement à Windows, il n’y a pas plusieurs racines comme `C:`, `D:`, etc.

## Introduction

En Linux, **tout est un fichier**, même les disques et périphériques.  
Ils se trouvent dans le répertoire : `/dev`

Les disques y apparaissent comme **fichiers de type bloc**.

**On ne peut pas utiliser ces fichiers directement.** Il faut suivre ces 3 étapes :

1. Créer une ou plusieurs partitions
2. Formater la partition (créer un système de fichiers)
3. Monter la partition (lui donner un chemin d’accès)

---

## Voir les disques disponibles

```bash
$ ls /dev
$ ls /dev/sd*
$ ls /dev/hd*
```

### Nommage des disques

- **SCSI ou SATA** : `sd[x]`  
- **IDE** : `hd[x]`  
- **NVMe** : `nvme0n[x]`

La lettre change selon l’ordre :  
`a`, puis `b`, puis `c`, etc.
`1`, puis `2`, puis `3`, etc. pour les NVMe

> Exemple :  
> Premier disque SATA → `/dev/sda`  
> Deuxième disque SATA → `/dev/sdb`
> Premier disque NVMe → `/dev/nvme0n1`

Mise à part les disques NVMe, **Un disque seul n’a pas de numéro** à la fin. Les numéros sont pour les partitions.

### Nommage des partitions

Chaque disque peut avoir plusieurs partitions :

- `/dev/sda1`, `/dev/sda2`, ...
- `/dev/hda1`, `/dev/hda2`, ...
- `/dev/nvme0n1p1`, `/dev/nvme0n1p2`, ...

## Ajout de disques

- Quand on ajoute un disque (réel ou virtuel), il apparaît dans `/dev`.
- Quand un disque est ajouté, il faut le **partitionner**

## Création de partitions

### Voir les partitions existantes

```bash
$ sudo fdisk -l
```

Exemple de sortie :

```bash
Disque /dev/nvme0n1 : 20 GiB, 21474836480 octets, 41943040 secteurs

Périphérique   Amorçage   Début      Fin Secteurs Taille Id Type
/dev/nvme0n1p1 *           2048  2099199  2097152     1G 83 Linu
/dev/nvme0n1p2          2099200 41943039 39843840    19G 8e LVM 

Disque /dev/mapper/almalinux-root : 17 GiB, 18249416704 octets, 
Disque /dev/mapper/almalinux-swap : 2 GiB, 2147483648 octets, 
```

### Quelques infos utiles

- On peut créer **4 partitions principales** maximum.
- Ou **1 partition principale** + **1 étendue** (dans laquelle on met plusieurs partitions logiques).

### Créer une partition

Utilise la commande :

```bash
$ sudo fdisk /dev/sdb  # + n, p + Entrée
```

**NB** : pas de numéro à la fin !

**Étapes typiques dans *fdisk***

- `n` → nouvelle partition
- `p` → partition principale
- `Entrée` → accepte le numéro proposé (ou entre-en un)
- `Entrée` → début de la partition (ou indique-le)
- `Entrée` → fin de la partition  
   ==> Exemple : `+3G` pour une taille de 3 Go
- `w` → **sauvegarde et quitte**

Les nouvelles partitions seront visibles dans `/dev` :

- `/dev/sdb1`
- `/dev/sdb2`
- `/dev/nvme0n1p1`
- etc.


## Création du système de fichiers

Une partition vide ne sert à rien.  
Il faut y créer un **système de fichiers**.
```bash
$ sudo mkfs -t ext4 /dev/sdb1
```
> `-t` ext4: spécifie le type de système de fichiers à créer (la valeur par défaut est ext2 si non spécifié).

ou

```bash
$ sudo mkfs.ext4 /dev/sdb1
```

Les deux font la même chose.

Types possibles : `ext2`, `ext3`, `ext4`, `xfs`, `fat32`, etc.  
(Linux ne gère pas bien **NTFS**.)

Une fois formatée, la partition est prête…  
… mais il faut encore **la monter** !


## Montage d’une partition

Monter une partition = **lui donner un chemin d’accès** dans le système.

### Rappels importants

- On monte une partition dans **un répertoire vide**.
- Si le répertoire contient déjà des fichiers, ils **seront masqués** jusqu’au démontage.
- Chaque partition → **un répertoire différent**

### Deux façons de monter une partition

**1. Montage manuel (temporaire)**

```bash
$ sudo mount /dev/sdb1 /root/data
```

Vérifie le montage :

```bash
$ df -h
```

À partir de maintenant, **tout ce que tu écris dans `/root/data`** sera enregistré sur la partition `/dev/sdb1`.

Ce montage **disparaît après redémarrage**.

**2. Montage automatique (permanent)**

Il faut modifier le fichier **`/etc/fstab`**.
  
{{% notice style="warning" title="Attention" %}}
- Une erreur dans ce fichier peut empêcher Linux de démarrer !  
- En cas de doute, faites une sauvegarde ou utilisez `mount -a` pour tester.
{{% /notice %}}


#### Ajouter une ligne dans */etc/fstab*

```
/dev/sdb1    /root/data    ext4    defaults    0 0
```

Tester si tout est correct :

```bash
$ mount -a
```

La commande `mount -a` sert à monter automatiquement **tous les systèmes de fichiers** qui sont listés dans le fichier `/etc/fstab`, à condition qu’ils soient configurés pour être montés automatiquement.

- `mount` est la commande pour monter des systèmes de fichiers (disques, partitions, etc.).
- `-a` (abréviation de `--all`) indique à mount de lire `/etc/fstab` et de monter tout ce qui y est défini, sauf les entrées marquées avec l’option `noauto`.


Exemple du fichier `/etc/fstab` :
```php-template
# <file system>  <mount point>  <type>  <options>       <dump>  <pass>
UUID=1234abcd-56ef-78gh-90ij-123456klmnop /mnt/backup   ext4    defaults        0       2
/dev/sdb1        /mnt/usb       vfat    defaults,noauto 0       0
```

**Explication** :

- La première ligne dit que la partition avec l'UUID donné sera montée automatiquement sur `/mnt/backup` au format `ext4`.

- La deuxième ligne concerne une clé USB sur /dev/sdb1, qui sera montée sur `/mnt/usb` au format vfat, mais **avec l'option** `noauto` → elle ne sera pas montée automatiquement avec `mount -a`.

## Démonter un disque ou une partition avec *umount*

Lorsqu'on a terminé d'utiliser un disque ou une partition (clé USB, disque dur externe, etc.), il est important de le **démonter proprement** avant de le retirer physiquement. Cela permet d’éviter la perte de données ou la corruption du système de fichiers.

La commande utilisée pour démonter un périphérique est `umount` (et non "unmount").

```bash
$ sudo umount /dev/sdb1
```

### Démonter par point de montage

On peut aussi démonter en indiquant le **point de montage** :

```bash
$ sudo umount /media/usb
```

ou

```bash
$ sudo umount /mnt/mon_disque
```

