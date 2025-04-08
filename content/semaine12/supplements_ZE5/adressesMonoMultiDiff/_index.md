+++
title = "4. Détermination des adresses IPv4 publiques et privées"
weight = 1234
draft = true
+++


Tout comme il existe différentes façons de transmettre un paquet IPv4, il existe également différents types d’adresses IPv4.

Certaines adresses IPv4 **ne peuvent pas être utilisées pour aller sur Internet**, tandis que d’autres sont spécifiquement allouées pour le **routage vers Internet**.

## Adresses IPv4 publiques

Les **adresses publiques** sont acheminées de manière globale entre les routeurs des fournisseurs d’accès à Internet (**FAI**).

## Adresses IPv4 privées

Toutes les adresses IPv4 disponibles **ne peuvent pas être utilisées sur Internet**.  
Certains blocs d’adresses, appelés **adresses privées**, sont utilisés par la plupart des entreprises pour attribuer des adresses IPv4 aux hôtes **internes**.


### Blocs d’adresses privées (RFC 1918)

| Adresse réseau | Préfixe | Plage d’adresses privée             |
|----------------|---------|-------------------------------------|
| 10.0.0.0       | /8      | 10.0.0.0 – 10.255.255.255           |
| 172.16.0.0     | /12     | 172.16.0.0 – 172.31.255.255         |
| 192.168.0.0    | /16     | 192.168.0.0 – 192.168.255.255       |
