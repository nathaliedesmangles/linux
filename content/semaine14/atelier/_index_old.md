+++
title = "ATELIEROLD: WSL, Ubuntu et des commandes Linux simples"
weight = 142
draft = true
+++

## Objectifs de l'atelier

Cet atelier a pour but de vous familiariser avec la ligne de commandes en utilisant Ubuntu comme distribution Linux. 

<!--

## Format de la remise

{{% notice style=warning title=Attention %}}
Pour chacune des étapes des **parties 2 et 3** vous devrez prendre une **capture d'écran de vos commandes et résultats**. **ATTENTION**: On doit pouvoir voir votre nom d'utilisateur. Ne travaillez donc **pas** avec l'utilisateur `root`.
{{% /notice %}}

-->

# Atelier

## Partie 1: Installations WSL (*Windows Subsystem for Linux*)

1. Rechercher les fonctionnalités Windows

![Recherche fonctionnalités](recherche-fonctionnalites.png?width=25vw)

2. Dans la liste, cocher **Sous-Système Windows pour Linux**

![Activer fonctionnalités](activer-fonctionnalite.png?width=25vw)

3. Redémarrer

Une fois redémarré, vous pouvez installer la distribution Ubuntu depuis le Microsoft Store.

## Partie 2: Installation d'Ubuntu

WSL prend en charge une variété de distributions Linux, y compris la dernière version LTS d'Ubuntu. 

Il existe plusieurs façons d'installer des distributions sur WSL, nous nous concentrons ici sur la méthode via l'application dans Microsoft Store et les commandes WSL exécutées dans le terminal. Le résultat est le même quelle que soit la méthode.

**Application dans Microsoft Store**

1. Ouvrir Microsoft Store et trouver la dernière version d'Ubuntu.

![Résultats de recherche pour Ubuntu 24.04 LTS dans la barre de recherche Windows.](search-ubuntu-windows.png?width=40vw)

2. Cliquez sur **Free/Gratuit**, puis sur **Get/Obtenir**.

![Page d'installation pour Ubuntu 24.04 LTS dans le Microsoft Store.](choose-distribution.png?width=40vw)

3. Patienter durant l’installation. Ubuntu sera alors installé sur votre machine. 

4. Avant de commencer, s’assurer qu’Ubuntu est à jour:
```plaintext
$ sudo apt update
```
<!--
- Prenez une capture d'écran de la fenêtre de la commande avec le résultat et nommez-la `1.png`.
-->

**NOTE**: La commande `sudo` permet d’exécuter une commande en tant qu’administrateur du système.

Une fois installé, vous pouvez soit lancer l'application directement depuis le Microsoft Store, soit rechercher Ubuntu dans votre barre de recherche Windows.

<!--
- Prenez une capture d'écran de la fenêtre de terminal Ubuntu et nommez-la `2.png`.
-->


## Partie 3: Installation et configuration de Visual Studio Code

### Installation

1. **Installer VS Code :**
   - Téléchargez et installez Visual Studio Code depuis le site officiel : [code.visualstudio.com](https://code.visualstudio.com).

2. **Installer l'extension WSL :**
   - Ouvrez VS Code.
   - Accédez à l'onglet des extensions (icône de carré à gauche ou `Ctrl+Shift+X`).
   - Recherchez et installez l'extension **Remote - WSL**.

### Configuration de l'environnement

1. **Accéder à WSL depuis VS Code :**
   - Lancez Ubuntu (WSL) et naviguez jusqu'à votre répertoire de projet ou créez-en un :
     ```
     mkdir mon_projet
     cd mon_projet
     ```
   - Tapez `code .` pour ouvrir VS Code directement dans ce répertoire.

2. **Configurer le terminal :**
   - Dans VS Code, allez dans `Fichier > Préférences > Paramètres`.
   - Recherchez "terminal.integrated.defaultProfile.windows" et sélectionnez "WSL" comme terminal par défaut.


## Partie 4 : Manipulation de l'environnement Ubuntu dans WSL

1. **Installer des outils de développement :**
   - Utilisez `apt` pour installer des packages :
     ```
     sudo apt update
     sudo apt install build-essential git curl
     ```

2. **Cloner un projet Git :**
   - Utilisez la commande suivante pour cloner un projet :
     ```
     git clone https://github.com/utilisateur/projet.git
     ```

3. **Exécuter un projet :**
   - Par exemple, pour un projet Node.js :
     ```
     sudo apt install nodejs npm
     npm install
     npm start
     ```

## Conseils et Astuces

- **Partage de fichiers entre Windows et WSL :** Les fichiers créés sous WSL sont accessibles dans l’explorateur Windows sous : `\\wsl$\Ubuntu\`.
- **Performances :** Pour des performances optimales, stockez vos fichiers de projet dans le système de fichiers Linux (dans WSL) plutôt que dans le système de fichiers Windows.
- **Mises à jour :** Pensez à mettre à jour régulièrement WSL et Ubuntu :
  ```
  sudo apt update && sudo apt upgrade
  ```

## Conclusion

Avec WSL, Ubuntu et VS Code, vous disposez d’un environnement puissant pour le développement sous Linux, tout en conservant la commodité de Windows.

---
**References**:  
1. [Site Ubuntu WSL](https://documentation.ubuntu.com/wsl/en/latest/guides/install-ubuntu-wsl2/)
2. [Vidéo YouTube](https://youtu.be/HrAsmXy1-78?si=VyvuNbkGmthsnLAI)
---

