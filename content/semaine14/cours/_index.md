+++
title = "Installation et manipulation de WSL avec Ubuntu et VS Code"
weight = 141
draft = true
+++

Le ***Windows Subsystem for Linux*** (WSL) est une fonctionnalité de Windows qui permet d'exécuter un environnement Linux directement sur un système Windows sans avoir besoin d'une machine virtuelle. 

Nous allons voir comment installer et utiliser WSL avec Ubuntu et Visual Studio Code (VS Code).

## Prérequis

- Un PC sous Windows 10 (version 2004 ou ultérieure) ou Windows 11.
- Accès à une connexion Internet.

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

## 3. Installation de Visual Studio Code

1. **Installer VS Code :**
   - Téléchargez et installez Visual Studio Code depuis le site officiel : [code.visualstudio.com](https://code.visualstudio.com).

2. **Installer l'extension WSL :**
   - Ouvrez VS Code.
   - Accédez à l'onglet des extensions (icône de carré à gauche ou `Ctrl+Shift+X`).
   - Recherchez et installez l'extension **Remote - WSL**.

---

## 4. Configuration de l'environnement

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

---

## 5. Manipulation de l'environnement Ubuntu dans WSL

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

---

## 6. Conseils et Astuces

- **Partage de fichiers entre Windows et WSL :** Les fichiers créés sous WSL sont accessibles dans l’explorateur Windows sous : `\\wsl$\Ubuntu\`.
- **Performances :** Pour des performances optimales, stockez vos fichiers de projet dans le système de fichiers Linux (dans WSL) plutôt que dans le système de fichiers Windows.
- **Mises à jour :** Pensez à mettre à jour régulièrement WSL et Ubuntu :
  ```
  sudo apt update && sudo apt upgrade
  ```

---

## Conclusion

Avec WSL, Ubuntu et VS Code, vous disposez d’un environnement puissant pour le développement sous Linux, tout en conservant la commodité de Windows.

