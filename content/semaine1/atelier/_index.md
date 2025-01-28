+++
title = "ATELIER #1: Installation de Linux sur une VM"
weight = 14
alwaysopen = true
+++

## Objectifs

- Installation du logiciel de virtualisation VMware workstation Pro.
- Création d'une machine virtuelle (VM).
- Installation de Linux sur la VM. 

---

## Prérequis pour l’atelier

1. Avoir Windows 11 installé sur votre disque SSD (**sur une seule partition**).
2. Télécharger un logiciel de virtualisation tel que VMWare Workstation Pro 17.
3. Télécharger la dernière version d'Almalinux (janvier 2025 c'est la version 9.5).

## Rappels (Cours ZE5 Virtualisation)

- VMWare permet d’installer différents systèmes d’exploitation sur une même machine.
- Le nombre de **machines virtuelles** (VM) que l’on peut installer dépend de la puissance en terme de CPU et de mémoire de la machine hôte.
- La **machine hôte** est celle qui héberge les machines virtuelles aussi appelées **les invités**.
- La machine hôte peut être Windows ou Linux et les invités peuvent être une grande variété de systèmes d’exploitation.

## Format de la remise

{{% notice style="warning" title="Attention" %}}
Vous devrez prendre des **captures d'écran de vos installations. Pour plus de détails, voir les documents ci-dessous:**.
{{% /notice %}}

---

# Atelier

### Étape 1: Réinstallation de Windows

Utiliser la procédure obtenue dans le cours 420-ZC5-MO de la session d'automne.

{{% notice style="warning" title="Attention" %}}
Vous devez installer **Windows 11** et sur **une seule partition**.
{{% /notice %}}


### Étape 2: Téléchargement et installation de VMWare sur la machine hôte (votre SSD Windows)

[Guide - Téléchargement WMWare](Telechargement-vmware.pdf)

[Guide - Installation de VMWare](Installation%20de%20VMware%20Workstation%2017%20Pro.pdf)

### Étape 3: Création d'une VM et installation d'Almalinux


1. Télécharger l'image d'Almalinux

[Site Almalinux](https://almalinux.org/get-almalinux/)

{{% notice note %}}
Choisir **AlmaLinux OS 9.5 DVD ISO**
{{% /notice %}}

Vous obtiendrez le fichier ***AlmaLinux-9.5-x86_64-dvd.iso***

2. Créer une VM pour y installer Almalinux

{{% notice style=warning title=Attention %}}
Ne pas sauvegarder le fichier `.iso` sur ***OneDrive***, ni dans le répertoire **Téléchargements** (*Downloads*), Sauvegardez le sur votre disque dur (en  général c'est le lecteur C:).
{{% /notice %}}

[Guide - Création d'une VM Almalinux](Creation%20VM%20Almalinux.pdf)


#### En cas de problème

**Cas #1**: Il arrive parfois que le serveur X ne démarre pas dans le temps imparti, ce qui force l'installation à basculer en mode texte. Vous le résolvez en augmentant le délai avec `inst.xtimeout=180` en début d'installation.

Pour résoudre le problème:
1. menu installation - choisir troubleshooting
2. touche tab
3. ajouter inst.xtimeout=valeur en seconde en bas ( comme l'image ci bas)

![HTTP](./vm27.png?height=200)

**Cas #2**: Si le processus d’installation exécute le ***Check*** et que c'est très long, il suffit d’appuyer plusieurs fois sur la touche `Esc` pour sauter la vérification et poursuivre l'installation.


**Cas #3**: Sur certains postes/SSD, la configuration ci-dessous règle les problèmes encourus pendant l'installation d'Almalinux.

Configuration de la VM:
 - 40 Gb au lieu de 20 Gb
 - 4096 en mémoire
 - 1 processeur et 4 Coeurs

<!--
[Vidéo par Dell](www.dell.com/support/contents/fr-ca/videos/videoplayer/création-d’une-machine-virtuelle-dans-vmware-workstation-pro/1700108455885340472)
-->

