+++
title = "Atelier #10d"
weight = 183
draft = true
+++

# Solution de l'exercice

---

## **1. Ajouter un disque virtuel de 10G**
Cela se fait via l’interface de VirtualBox ou VMware, selon ce que vous utilisez :

- Éteignez la VM.
- Dans les paramètres de la VM, ajoutez un nouveau disque virtuel (VHD, VDI, VMDK...) de **10 Go**.
- Redémarrez la VM.

Dans le terminal :

```bash
ls /dev
```

Le nouveau disque apparaîtra probablement comme `/dev/sdb` (si votre disque principal est `/dev/sda`).


## **2. Créer une partition primaire sur le disque**

```bash
sudo fdisk /dev/sdb
```

Dans le menu `fdisk`, tapez les commandes suivantes :

- `n` → créer une nouvelle partition
- `p` → partition primaire
- `1` → numéro de la partition
- Appuyez sur Entrée pour accepter les valeurs par défaut de début et de fin
- `w` → écrire la table de partition et quitter


## **3. Vérifier la nouvelle partition**

```bash
ls /dev
```

Vous verrez maintenant une nouvelle entrée, comme `/dev/sdb1`.


## **4. Créer un système de fichiers**

On va utiliser `ext4`, par exemple :

```bash
sudo mkfs.ext4 /dev/sdb1
```


## **5. Créer un répertoire et monter la partition**

Créez un dossier de point de montage :

```bash
sudo mkdir /mnt/mon_disque
```

Montez la partition :

```bash
sudo mount /dev/sdb1 /mnt/mon_disque
```

Vous pouvez vérifier avec :

```bash
df -h
```


## **6. Démonter la partition**

```bash
sudo umount /mnt/mon_disque
```


# Résumé des commandes clés

```bash
ls /dev
sudo fdisk /dev/sdb
sudo mkfs.ext4 /dev/sdb1
sudo mkdir /mnt/mon_disque
sudo mount /dev/sdb1 /mnt/mon_disque
sudo umount /mnt/mon_disque
```