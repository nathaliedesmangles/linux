+++
title = "2. Détermination de la plage d’adresses hôtes et de diffusion d’un réseau"
weight = 1232
draft = true
+++


Les **adresses hôtes** sont des adresses qui peuvent être affectées à un périphérique tel qu’un ordinateur hôte, un ordinateur portable, un téléphone intelligent, une imprimante, un routeur, etc.

La **partie hôte** de l’adresse correspond aux bits à `0` dans le masque de sous-réseau.

Les adresses hôtes peuvent avoir n’importe quelle combinaison de bits dans la partie hôte de l’adresse IPv4.  
Il existe deux cas particuliers :

- Si **tous les bits sont à 0**, il s’agit de **l’adresse réseau**.  
- Si **tous les bits sont à 1** (255), il s’agit de **l’adresse de diffusion** (*broadcast*), qui permet d’atteindre tous les périphériques du réseau IPv4.


## Calcul du nombre d’hôtes

Pour déterminer le nombre d’hôtes possibles dans un réseau, on utilise la formule :

```
2ⁿ – 2
```

Où `n` est le **nombre de bits alloués à la partie hôte**.


## Exemple : `192.168.10.10/24`

- 24 bits pour la partie réseau  
  ➔ Masque de sous-réseau : `255.255.255.0`

- 32 bits (totaux) – 24 bits = **8 bits alloués à la partie hôte**

- `2⁸ – 2 = 256 – 2 = 254 hôtes`


## Plage d’adresses IP des 254 hôtes

- **Adresse du premier hôte** : On ajoute `1` à l’adresse réseau  
  ➔ `192.168.10.1`

- **Adresse de diffusion (broadcast)** : Tous les bits de la partie hôte sont à `1`  
  ➔ `192.168.10.255`

- **Adresse du dernier hôte** : On soustrait `1` à l’adresse de diffusion  
  ➔ `192.168.10.254`
