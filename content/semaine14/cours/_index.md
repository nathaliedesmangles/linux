+++
title = "WSL avec Ubuntu et VS Code"
weight = 141
draft = true
+++

## Qu'est-ce que WSL?

***Windows Subsystem for Linux*** (WSL) est une fonctionnalité de Windows qui permet d'exécuter un environnement Linux directement sur un système Windows sans avoir besoin d'une machine virtuelle. 

Grâce à WSL, vous pouvez :
- Choisir et installer des distributions Linux à partir du Microsoft Store.
- Exécuter des commandes en ligne de commande tels que grep, sed et awk et autres 
- Exécuter des scripts Bash et des logiciels Linux

## Développement Croisé

- WSL est particulièrement utile pour les développeurs qui travaillent avec des technologies basées sur Linux ou des projets qui doivent être exécutés ou testés dans un environnement Linux. 
- Ils peuvent développer sur Windows tout en exécutant et en testant leur code dans un environnement Linux.

## Interopérabilité

- WSL permet une interaction transparente entre Windows et Linux, où vous pouvez accéder aux fichiers Windows depuis Linux et vice-versa, exécuter des commandes Linux dans PowerShell, et même lancer des applications Windows depuis l'environnement Linux.
- Pour accéder aux répertoires partagés, 
  - Du terminal linux, aller dans le répertoire /mnt. Vous y trouverez des dossiers correspondant à chaque lecteur de votre système Windows. Par exemple, /mnt/c représente le lecteur C: de Windows, /mnt/d le lecteur D:, et ainsi de suite.
  - Depuis l'Explorateur de Fichiers de Windows, vous pouvez taper \\wsl$ dans la barre d'adresse de l'Explorateur de Fichiers de Windows. Cela vous donnera accès aux fichiers de votre distribution Linux.

Dans l'atelier, nous allons voir comment installer et utiliser WSL avec Ubuntu et Visual Studio Code (VS Code).

## Prérequis

- Un PC sous Windows 10 (version 2004 ou ultérieure) ou Windows 11.
- Accès à une connexion Internet.


<!--
---

## 1. Activation de WSL

1. **Activer les fonctionnalités Windows :**
   - Ouvrez "Panneau de configuration" > "Programmes" > "Activer ou désactiver des fonctionnalités Windows".
   - Cochez les cases suivantes :
     - **Sous-système Windows pour Linux**
     - **Plateforme de machine virtuelle**
   - Cliquez sur "OK" et redémarrez votre PC.

2. **Installer WSL 2 :**
   - Ouvrez PowerShell en mode administrateur.
   - Exécutez la commande suivante pour définir WSL 2 comme version par défaut :
     ```
     wsl --set-default-version 2
     ```
---

## 2. Installation d'Ubuntu sur WSL

1. **Installer Ubuntu :**
   - Ouvrez le Microsoft Store.
   - Recherchez "Ubuntu" et choisissez une version (par ex., "Ubuntu 22.04 LTS").
   - Cliquez sur "Installer".

2. **Configurer Ubuntu :**
   - Lancez l'application Ubuntu depuis le menu Démarrer.
   - Créez un utilisateur et un mot de passe lors du premier démarrage.

---
-->

