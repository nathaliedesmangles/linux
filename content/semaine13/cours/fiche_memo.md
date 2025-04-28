+++
title = "Gestion des disques (étapes)"
weight = 1311
+++


## Créer et utiliser un disque (étapes par étapes)

**1. Lister les disques**
```bash
$ ls /dev
```

**2. Créer une partition**
```bash
$ sudo fdisk /dev/sdb   # n → p → Entrée → Entrée → Entrée → w
```

**3. Formater la partition**
```bash
$ sudo mkfs.ext4 /dev/sdb1
```

**4. Vérifier les montages existants**
```bash
$ df -h
```

**5. Créer un dossier de montage**
```bash
$ sudo mkdir /mnt/mon_disque
```

**6. Monter la partition**
```bash
$ sudo mount /dev/sdb1 /mnt/mon_disque
```

**7. Monter automatiquement au démarrage**
```bash
$ sudo vim /etc/fstab
# Ajouter la ligne suivante :
/dev/sdb1 /mnt/mon_disque ext4 defaults 0 0

$ sudo mount -a
```

## Supprimer ou retirer un disque

**8. Démonter la partition**
```bash
$ sudo umount /mnt/mon_disque
```
ou
```bash
$ sudo umount /dev/sdb1
```

{{% notice style="accent" icon="Note" %}}
**Note** : Adapter les chemins (/dev/sdb1, /mnt/mon_disque) selon votre cas.
{{% /notice %}}


