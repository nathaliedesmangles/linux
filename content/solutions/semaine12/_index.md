+++
title = "Atelier #10c"
weight = 182
+++

# Solution de l'exercice

On suppose que l’interface Ethernet s’appelle `ens160` (vous pouvez vérifier avec `ip a` si elle s'appelle autrement comme `ens33`, `enp0s3`, etc.).

---

## 1. Afficher l’adresse IP de l’interface Ethernet

```bash
ip addr show ens160
```

Ou pour n’afficher que l’adresse IP :

```bash
ip -4 addr show ens160 | grep inet
```


## 2. Ajouter deux autres adresses IP à l’interface (même sous-réseau)

Si l’adresse actuelle est par exemple `192.168.1.10/24`, on peut ajouter `192.168.1.100` et `192.168.1.101` :

```bash
sudo ip addr add 192.168.1.100/24 dev ens160
sudo ip addr add 192.168.1.101/24 dev ens160
```


## 3. Vérifier la réponse avec *ping*

```bash
ping 192.168.1.100
ping 192.168.1.101
```

On doit voir des réponses si les adresses sont bien assignées.


## 4. Supprimer les adresses IP ajoutées

```bash
sudo ip addr del 192.168.1.100/24 dev ens160
sudo ip addr del 192.168.1.101/24 dev ens160
```


## 5. Faire un ping vers les adresses supprimées

```bash
ping 192.168.1.100
ping 192.168.1.101
```

Cette fois, on **ne devrait pas** avoir de réponse, mais un message comme *hôte de destination injoignable* (***destination host unreachable***), *Délai d’attente dépassé* (***Request timed out***) ou *0 reçus* (***100% packet loss***), puisque les adresses ont été retirées.

### 5.1 Options utiles avec ping

{{% notice style="secondary" title="-c et spécifier le nombre de paquets envoyés" %}}
Dans la commande :

```bash
ping -c 3 192.168.1.100
```

- `-c` signifie **"count"** : c’est le nombre de requêtes ICMP que `ping` va envoyer.
- `3` signifie qu'on veut envoyer **3 paquets**.

Donc : `ping -c 3 192.168.1.100`  
- envoie 3 paquets, attend les réponses, puis s'arrête automatiquement. 

Exemple de résultat typique :
```bash
$ ping -c 3 192.168.1.100
PING 192.168.1.100 (192.168.1.100) 56(84) bytes of data.
64 bytes from 192.168.1.100: icmp_seq=1 ttl=64 time=0.123 ms
64 bytes from 192.168.1.100: icmp_seq=2 ttl=64 time=0.098 ms
64 bytes from 192.168.1.100: icmp_seq=3 ttl=64 time=0.105 ms

--- 192.168.1.100 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2041ms
rtt min/avg/max/mdev = 0.098/0.108/0.123/0.011 ms

``` 

Si on omet l'option `-c` comme dans `ping 192.168.1.100`, ça continue **jusqu’à ce qu'on fasses Ctrl+C** pour l’interrompre.
{{% /notice %}}


