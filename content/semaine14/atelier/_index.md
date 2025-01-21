 
+++
title = "ATELIER #2: WSL, Ubuntu et des commandes Linux simples"
weight = 22
+++

## Objectifs de l'atelier

Cet atelier a pour but de vous familiariser avec la ligne de commandes en utilisant Ubuntu comme distribution Linux. 

## Format de la remise

{{% notice style=warning title=Attention %}}
Pour chacune des étapes des **parties 2 et 3** vous devrez prendre une **capture d'écran de vos commandes et résultats**. **ATTENTION**: On doit pouvoir voir votre nom d'utilisateur. Ne travaillez donc **pas** avec l'utilisateur `root`.
{{% /notice %}}

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
- Prenez une capture d'écran de la fenêtre de la commande avec le résultat et nommez-la `1.png`.

**NOTE**: La commande `sudo` permet d’exécuter une commande en tant qu’administrateur du système.

Une fois installé, vous pouvez soit lancer l'application directement depuis le Microsoft Store, soit rechercher Ubuntu dans votre barre de recherche Windows.

- Prenez une capture d'écran de la fenêtre de terminal Ubuntu et nommez-la `2.png`.

---
**References**:  
1. [Site Ubuntu WSL](https://documentation.ubuntu.com/wsl/en/latest/guides/install-ubuntu-wsl2/)
2. [Vidéo YouTube](https://youtu.be/HrAsmXy1-78?si=VyvuNbkGmthsnLAI)
---

