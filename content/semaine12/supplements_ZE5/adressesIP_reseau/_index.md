+++
title = "1. Détermination de la partie réseau d’une IPv4"
weight = 1231
draft = true
+++


## AND (ET) logique et masque de sous-réseau

Pour identifier l’adresse réseau d’un hôte IPv4, l’adresse IPv4 est soumise bit par bit à l’opération **AND (ET)** de manière logique avec le **masque de sous-réseau**. Lorsque cette opération AND est appliquée entre l’adresse et le masque de sous-réseau, le résultat obtenu est l’adresse réseau.

### Rappel des opérations logiques AND :

- `1 AND 1 = 1`  
- `0 AND 1 = 0`  
- `1 AND 0 = 0`  
- `0 AND 0 = 0`  

### Exemple : `192.168.10.10/24`

1. La longueur du préfixe `/24` permet de trouver le masque de sous-réseau.  
   Le préfixe indique que le masque contient 24 bits à `1`, soit :

   ```
   11111111.11111111.11111111.00000000
   ```

   Ce qui équivaut, en notation décimale pointée, à :

   ```
   255.255.255.0
   ```

2. On effectue l’opération **ET logique** entre l’adresse IP et le masque de sous-réseau.  
   L’adresse IPv4 doit d’abord être convertie en binaire :

   ```
   IPv4     : 192       168       10        10
   Binaire  : 11000000.10101000.00001010.00001010
   Masque   : 11111111.11111111.11111111.00000000
   Résultat : 11000000.10101000.00001010.00000000
   ```

3. Le résultat binaire correspond à l’adresse réseau :

   ```
   Adresse réseau : 192.168.10.0
   ```