+++
title = "Atelier #10c: Réseau"
weight = 132
draft = true
+++


# Solution des exercices



## Exercice 2 — Reproduire une petite infrastructure réseau virtuelle sur une machine Linux.

### Étapes à réaliser

1. **Ajouter les interfaces (sur votre VM)**  
   → Vous pouvez le faire dans la configuration de la VM (VMware).

2. **Déclarer les interfaces dans `nmcli`** :

```bash
$ sudo nmcli con add con-name ens224 type ethernet ifname ens224
$ sudo nmcli con add con-name ens225 type ethernet ifname ens225
```

3. **Attribuer des adresses IP statiques :**

```bash
$ sudo nmcli con mod ens224 ipv4.addresses 192.168.50.10/24
$ sudo nmcli con mod ens224 ipv4.method manual

$ sudo nmcli con mod ens225 ipv4.addresses 192.168.60.10/24
$ sudo nmcli con mod ens225 ipv4.method manual
```

4. **Redémarrer les connexions :**

```bash
$ sudo nmcli con up ens224
$ sudo nmcli con up ens225
```

5. **Modifier `/etc/hosts` :**

```bash
$ sudo nano /etc/hosts
```

Ajoutez :

```
192.168.50.10   interface-50
192.168.60.10   interface-60
```

6. **Tester la communication entre interfaces :**

```bash
$ ping interface-50
$ ping interface-60
```

7. **Rendre `ens224` dynamique (DHCP), mais garder `ens225` en IP fixe :**

```bash
$ sudo nmcli con mod ens224 ipv4.method auto
$ sudo nmcli con mod ens224 ipv4.addresses ""
$ sudo nmcli con up ens224
```

8. **Vérifier les IP finales avec `ip a`**  
9. **Documenter vos étapes dans un petit fichier `rapport.txt`**

---

## Variante possible

Faites la même chose **sans `nmcli`**, en modifiant directement les fichiers de configuration.

### Étape 1 : Créer les fichiers de configuration

Les fichiers sont situés dans :

```bash
/etc/sysconfig/network-scripts/
```

#### A. Configuration statique pour `ens224` (IP fixe au début)

Créer le fichier :

```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-ens224
```

Contenu :

```ini
DEVICE=ens224
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.50.10
NETMASK=255.255.255.0
GATEWAY=192.168.50.1
DNS1=8.8.8.8
```

#### B. Configuration statique pour `ens225`

```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-ens225
```

Contenu :

```ini
DEVICE=ens225
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.60.10
NETMASK=255.255.255.0
```


### Étape 2 : Modifier `/etc/hosts`

```bash
sudo nano /etc/hosts
```

Ajoutez :

```
192.168.50.10 interface-50
192.168.60.10 interface-60
```


### Étape 3 : Redémarrer le service réseau

```bash
sudo systemctl restart network
```


### Étape 4 : Vérification

```bash
ip a show ens224
ip a show ens225
ping interface-50
ping interface-60
```


### Étape 5 : Revenir à DHCP sur `ens224`

Éditez le fichier `ifcfg-ens224` :

```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-ens224
```

Remplacez le contenu par :

```ini
DEVICE=ens224
BOOTPROTO=dhcp
ONBOOT=yes
```

Puis redémarrez le réseau :

```bash
sudo systemctl restart network
```

### Remarques

- Cette méthode est **persistante** automatiquement, car elle repose sur des fichiers lus au démarrage.
- `nmcli` et les fichiers `ifcfg-*` utilisent la même base : NetworkManager.
- Sur certaines machines, il peut être nécessaire de désactiver NetworkManager pour que la configuration manuelle fonctionne à 100 %.

```bash
sudo systemctl stop NetworkManager
sudo systemctl disable NetworkManager
```
