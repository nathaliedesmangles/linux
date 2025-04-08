+++
title = "5. Détermination du type adresses reseau hôte multidiffusion ou diffusion"
weight = 1235
draft = true
+++


- Il existe différentes façons d’envoyer un paquet à partir d’un périphérique source, et ces différentes transmissions affectent les adresses IPv4 de destination.
- Une **adresse IP source** ne peut être qu’une adresse **monodiffusion**, car le paquet ne peut provenir que d’une seule source.

## Adresse de diffusion (broadcast)

- Un paquet de diffusion a une adresse IP de destination avec tous les bits à 1 dans la partie hôte.

## Adresse de monodiffusion (unicast)

- La transmission monodiffusion fait référence à un périphérique qui envoie un message à un autre périphérique dans les communications un-à-un.
- Un paquet monodiffusion a une adresse IP de destination qui est une adresse monodiffusion qui va à un seul destinataire.

## Adresse de multidiffusion (multicast)

- La transmission multidiffusion réduit le volume du trafic en permettant à un hôte d’envoyer un seul paquet à un groupe d’hôtes.

## Étapes pour identifier le type d’une adresse IPv4

1. Calculez l’adresse réseau: L’adresse réseau est obtenue en appliquant une opération AND bit à bit entre l’adresse IP et le masque de sous-réseau.
2. Identifiez le type d’adresse:
   a. Si l’adresse IP est dans la plage de la classe D (224.0.0.0 à 239.255.255.255), il s’agit d’une adresse de multidiffusion.
   b. Si l’adresse IP est égale à l’adresse réseau ou à l’adresse de diffusion du réseau, il s’agit d’une adresse de réseau ou de diffusion, respectivement.
   c. Sinon, il s’agit d’une adresse d’hôte.