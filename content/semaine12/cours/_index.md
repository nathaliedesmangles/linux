+++
title = "Le réseau sous Linux"
weight = 121
+++


## Introduction

Configurer un réseau sous Linux se fait à l’aide de commandes et de fichiers texte.

Dans le cours [7 - vim et fichiers de configuration](https://linuxh25.netlify.app/semaine7/), nous avons vu comment modifier ces fichiers.  
Dans ce cours-ci, nous allons explorer des **commandes réseau essentielles** et faire quelques **exercices pratiques**.


## Rappel : les fichiers texte importants

Voici deux fichiers que nous avons déjà vus :

- **`/etc/hosts`** : permet une **résolution de noms simple** (utile si un serveur DNS n’est pas disponible).
- **`/etc/resolv.conf`** : contient la **liste des serveurs DNS** utilisés par la machine.


## Les commandes réseau

### La commande *nmcli*

La commande `nmcli` sert à **gérer les interfaces réseau**.

#### Lister les connexions réseau
```bash
# nmcli dev
```

#### Afficher la configuration IP
```bash
# ip a
# nmcli con show ens160
```

#### Configurer une adresse IP statique
```bash
# nmcli con mod ens160 ipv4.address 192.168.230.10/24
# nmcli con mod ens160 ipv4.gateway 192.168.230.2
# nmcli con mod ens160 ipv4.dns 8.8.8.8,8.8.4.4
# nmcli con mod ens160 ipv4.method manual
# nmcli con down ens160
# nmcli con up ens160
```

#### Revenir à une adresse IP dynamique (DHCP)
```bash
# nmcli con mod ens160 ipv4.method auto
# nmcli con mod ens160 ipv4.dns ""
# nmcli con mod ens160 ipv4.gateway "" ipv4.addresses ""
# nmcli con down ens160
# nmcli con up ens160
```

#### Ajouter une nouvelle interface réseau
```bash
# nmcli con add con-name ens224 type ethernet ifname ens224
```
Ensuite, vous pouvez lui attribuer une IP fixe ou utiliser le DHCP.


### La commande *ip*

La commande `ip` remplace `ifconfig`, qui est maintenant obsolète.  
Elle permet de **lire et modifier temporairement** la configuration IP d’une interface.

{{% notice style="warning" title="Attention" %}}
Les changements faits avec `ip` **ne sont pas permanents**. Ils seront perdus après un redémarrage.
{{% /notice %}}

#### Afficher les interfaces réseau
```bash
$ ip address
# ou plus court :
$ ip a
```

#### Afficher une seule interface
```bash
$ ip a show <interface>
```

#### Redémarrer une interface réseau
```bash
$ ifdown <interface>
$ ifup <interface>
```

#### Ajouter plusieurs adresses IP sur une même interface (même sous-réseau obligatoire)
```bash
$ ip addr add 192.168.230.132/24 dev ens33
```

#### Supprimer une adresse IP
```bash
$ ip addr del 192.168.230.132/24 dev ens33
```

#### Ajouter une passerelle par défaut
```bash
$ ip route add default via 192.168.230.2
```

#### Voir la table de routage
```bash
$ ip route
```

### La commande *ifconfig*

La commande `ifconfig` est plus ancienne et tend à disparaître, mais reste parfois utile.

#### Afficher les interfaces réseau
```bash
$ ifconfig
```

#### Voir une interface en particulier
```bash
$ ifconfig <interface>
```

#### Activer/désactiver une interface
```bash
$ ifconfig <interface> up
$ ifconfig <interface> down
```

#### Attribuer une adresse IP (temporairement)
```bash
$ ifconfig ens33 10.0.2.34 netmask 255.255.224.0
```

#### Ajouter une adresse IP secondaire (alias)
```bash
$ ifconfig ens33:1 10.0.2.56 netmask 255.255.255.0
```

> L’interface alias (`ens33:1`) utilise la même carte réseau (donc la même adresse MAC) et doit être dans le **même sous-réseau**.

#### Désactiver un alias
```bash
$ ifconfig ens33:1 down
```

## Le service réseau

Sous Linux, il faut parfois **redémarrer le service réseau** pour que les changements soient pris en compte.

#### Désactiver le service
```bash
$ nmcli networking off
```

#### Réactiver le service
```bash
$ nmcli networking on
```

---

## Exercice 1

Remplissez le tableau avec les paramètres actuels de votre machine :

| Adresse IP | Masque de sous-réseau | Passerelle par défaut | DNS1 | DNS2 |
|:----------:|:---------------------:|:----------------------:|:----:|:----:|
|            |                       |                        |      |      |

1. Votre adresse IP est-elle **statique** ou **dynamique (DHCP)** ?
2. Modifiez le bon fichier de configuration pour attribuer une **adresse IP statique**.
3. Redémarrez le service réseau et testez l'accès à Internet.
4. Revenez à une configuration en DHCP.
5. Testez à nouveau la connexion.

{{% notice style="green" title="Solution (à venir)" groupid="notice-toggle" expanded="false" %}}

{{% /notice %}}

## Exercice 2

1. Ajoutez **deux adresses IP supplémentaires** à votre interface avec la commande `ip`.  
   → Vous devez avoir **trois adresses IP différentes**.
 
   {{% notice style="warning" title="Attention" %}}
   Toutes les adresses doivent être dans le **même réseau**.
   {{% /notice %}}

2. Modifiez le fichier `hosts` pour associer **un nom différent à chaque adresse** (pour que les trois répondent à un ping).

3. Redémarrez le service réseau.  
   Est-ce que les adresses IP sont toujours là ?

4. Comment rendre ces adresses **persistantes** ?  
   (Trouvez la réponse en théorie, ou testez si vous le souhaitez.)


{{% notice style="green" title="Solution (à venir)" groupid="notice-toggle" expanded="false" %}}

{{% /notice %}}
