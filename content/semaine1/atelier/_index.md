+++
title = "ATELIER #1: Installation de Linux sur une VM"
weight = 14
alwaysopen = true
+++

## Objectifs

L'atelier a pour but de vous guider à travers le processus d'installation de Linux sur une machine virtuelle (VM). Cela permet d'expérimenter avec Linux sans affecter le système d'exploitation principal de l'ordinateur.

## Prérequis pour l’atelier

1. Avoir Windows 10 ou 11 installé sur votre disque SSD (sur une seule partition).
2. Télécharger un logiciel de virtualisation tel que VMWare Workstation Pro 17.
	- Vous trouverez le fichier executable de VMWare sur le Moodle du cours
3.Télécharger la dernière version d'Almalinux (janvier 2025 c'est la version 9.5).
	- Vous trouverez l'image sur le site suivant https://almalinux.org/get-almalinux/

{{% notice note %}}
Choisir **AlmaLinux OS 9.5 DVD ISO**
{{% /notice %}}


## Rappels (Cours ZE5 Virtualisation)

- VMWare permet d’installer différents systèmes d’exploitation sur une même machine.
- Le nombre de **machines virtuelles** (VM) que l’on peut installer dépend de la puissance en terme de CPU et de mémoire de la machine hôte.
- La **machine hôte** est celle qui héberge les machines virtuelles aussi appelées **les invités**.
- La machine hôte peut être Windows ou Linux et les invités peuvent être une grande variété de systèmes d’exploitation.

## Format de la remise

{{% notice style=warning title=Attention %}}
Vous devrez prendre des **captures d'écran de vos installations. Pour plus de détails, voir les documents ci-dessous:**.
{{% /notice %}}

# Atelier

### Étape 1: Réinstallation de Windows

Utiliser la procédure obtenue dans le cours 420-ZC5-MO de la session d'automne.

### Étape 2: Installation de VMWare sur la machine hôte (votre SSD Windows)

- Télécharger le fichier d'installation (.exe) de VMWare qui se trouve sur Moodle dans le dossier de l'atelier 1.

[Guide - Installation de VMWare](Installation%20de%20VMware%20Workstation%2017%20Pro.pdf)

### Étape 3: Création d'une VM et installation d'Almalinux

[Télécharger le fichier **AlmaLinux OS 9.5 DVD ISO**](https://almalinux.org/get-almalinux/)

Vous obtiendrez le fichier ***AlmaLinux-9.5-x86_64-dvd.iso***

[Guide - Création d'une VM Almalinux](Creation%20VM%20Almalinux.pdf)
<!--
[Vidéo par Dell](www.dell.com/support/contents/fr-ca/videos/videoplayer/création-d’une-machine-virtuelle-dans-vmware-workstation-pro/1700108455885340472)
-->

