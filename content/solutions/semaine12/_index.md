+++
title = "Atelier #10c"
weight = 182
draft = true
+++

# Solution de l'exercice

Les commandes doivent être exécutées avec les privilèges root ou avec `sudo`.


### 1. **Afficher l’adresse IP de l’interface Ethernet**
```bash
ip addr show
```
ou spécifiquement pour l’interface (souvent `eth0` ou `enp0s3`, à adapter selon ta VM) :
```bash
ip addr show eth0
```
Cherche une ligne comme :
```
inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0
```
C’est l’adresse IP principale de l’interface.


### 2. **Ajouter deux autres adresses IP sur la même interface Ethernet**
Admettons que ton IP actuelle est `192.168.1.100/24`, tu peux ajouter :
```bash
sudo ip addr add 192.168.1.101/24 dev eth0
sudo ip addr add 192.168.1.102/24 dev eth0
```


### 3. **Tester les deux adresses IP ajoutées**
Fais un ping vers chaque adresse :
```bash
ping -c 3 192.168.1.101
ping -c 3 192.168.1.102
```
Tu devrais obtenir une réponse comme :
```
64 bytes from 192.168.1.101: icmp_seq=1 ttl=64 time=0.045 ms
```


### 4. **Supprimer les deux adresses IP**
```bash
sudo ip addr del 192.168.1.101/24 dev eth0
sudo ip addr del 192.168.1.102/24 dev eth0
```


### 5. **Refaire un ping vers les deux adresses supprimées**
```bash
ping -c 3 192.168.1.101
ping -c 3 192.168.1.102
```
Tu devrais maintenant avoir un message d’erreur :
```
Destination Host Unreachable
```
ou
```
100% packet loss
```
