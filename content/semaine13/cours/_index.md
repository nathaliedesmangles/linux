+++
title = "Gestion des disques"
weight = 131
+++

## Introduction

En Linux, il n’existe **qu’un seul système de fichiers** :  
**`/`** ← C’est la racine de tout.

Contrairement à Windows, il n’y a pas plusieurs racines comme `C:`, `D:`, etc.

En Linux, **tout est un fichier**, même les disques et périphériques.  
Ils se trouvent dans le répertoire :  
**`/dev`**

Les disques y apparaissent comme **fichiers de type bloc**.

**On ne peut pas utiliser ces fichiers directement.** Il faut suivre ces 3 étapes :

1. Créer une ou plusieurs partitions
2. Formater la partition (créer un système de fichiers)
3. Monter la partition (lui donner un chemin d’accès)


## Ajout de disques

Quand on ajoute un disque (réel ou virtuel), il apparaît dans **`/dev`**.

### Nommage des disques

- **SCSI ou SATA** : `sd[x]`  
- **IDE** : `hd[x]`  
- **NVMe** : `nvme0n[x]`

La lettre change selon l’ordre :  
`a`, puis `b`, puis `c`, etc.

> Exemple :  
> Premier disque SATA → `/dev/sda`  
> Deuxième disque SATA → `/dev/sdb`

**Un disque seul n’a pas de numéro** à la fin. Les numéros sont pour les partitions.

### Voir les disques disponibles

```bash
$ ls /dev/sd*
$ ls /dev/hd*
```

### Dans une machine virtuelle (VMware)

- Si le pilote est **SCSI** : `sd[a-z]`
- Si le pilote est **IDE** : `hd[a-z]`

### Nommage des partitions

Chaque disque peut avoir plusieurs partitions :

- `/dev/sda1`, `/dev/sda2`, ...
- `/dev/hda1`, `/dev/hda2`, ...


## Création de partitions

Quand un disque est ajouté, il faut le **partitionner**.

### Voir les partitions existantes

```bash
$ fdisk -l
```

Exemple de sortie :

```bash
Disque /dev/sda : 64.4 Go
/dev/sda1   *    ...   Linux
/dev/sda2        ...   Linux LVM

Disque /dev/mapper/centos-root : 41.1 Go
Disque /dev/mapper/centos-swap : 2 Go
Disque /dev/mapper/centos-home : 20.1 Go
```

### Quelques infos utiles

- On peut créer **4 partitions principales** maximum.
- Ou 1 partition principale + **1 étendue** (dans laquelle on met plusieurs partitions logiques).

### Créer une partition

Utilise la commande :

```bash
$ fdisk /dev/sdb
```

**NB** : pas de numéro à la fin !

#### Étapes typiques dans *fdisk*

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
- etc.


## Création du système de fichiers

Une partition vide ne sert à rien.  
Il faut y créer un **système de fichiers**.
```bash
$ mkfs -t ext4 /dev/sdb1
```

ou

```bash
$ mkfs.ext4 /dev/sdb1
```

Les deux font la même chose.

Types possibles : `ext2`, `ext3`, `ext4`, `xfs`, `fat32`, etc.  
(Linux ne gère pas bien **NTFS**.)

Une fois formatée, la partition est prête…  
… mais il faut encore **la monter** !


## Montage d’une partition

Monter une partition = **lui donner un chemin d’accès** dans le système.

### Rappel important

- On monte une partition dans **un répertoire vide**.
- Si le répertoire contient déjà des fichiers, ils **seront masqués** jusqu’au démontage.
- Chaque partition → **un répertoire différent**

### Deux façons de monter une partition

**1. Montage manuel (temporaire)**

```bash
$ mount /dev/sdb1 /root/data
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

**Résumé des étapes à retenir :**

1. Ajouter le disque
2. Créer des partitions avec `fdisk`
3. Créer un système de fichiers avec `mkfs`
4. Monter la partition avec `mount`
5. (Optionnel) Rendre le montage permanent avec `/etc/fstab`


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

