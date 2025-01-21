+++
title = "ATELIER #5: Gestion des processus Linux"
weight = 52
+++


## Objectifs de l'atelier

- Comprendre les processus sous Linux.
- Apprendre à lister, gérer et contrôler les processus.
- Manipuler les processus en premier plan et en arrière-plan.


# Atelier

Dans cet atelier, vous apprendrez à manipuler les processus sous Linux en utilisant des commandes de base. Nous allons explorer les différents types de processus, ainsi que les commandes essentielles pour les superviser et les contrôler. Cet atelier est conçu pour être pratique et interactif.

---

## Exercice 1 : Identifier les processus

### Commande : `ps`
1. Ouvrez un terminal.
2. Tapez la commande suivante pour lister les processus associés à votre session actuelle :
   ```
   ps
   ```
3. Essayez d’utiliser `ps aux` pour afficher tous les processus en cours d’exécution :
   ```
   ps aux
   ```
   Observez les colonnes importantes comme **PID**, **USER**, et **COMMAND**.

---

## Exercice 2 : Observer les processus en temps réel

### Commande : `top`
1. Lancez la commande :
   ```
   top
   ```
2. Notez les informations fournies : utilisation du CPU, de la mémoire, etc.
3. Appuyez sur `q` pour quitter.

### Alternative : `htop`
1. Si disponible, essayez `htop` pour une interface plus conviviale :
   ```
   htop
   ```

---

## Exercice 3 : Gérer les processus en arrière-plan

### Commandes : `jobs`, `bg`, et `fg`

1. Lancez une commande en arrière-plan en ajoutant un `&` à la fin :
   ```
   sleep 30 &
   ```
2. Listez les processus en arrière-plan :
   ```
   jobs
   ```
3. Suspendez un processus (en premier plan) avec `Ctrl+Z` et relancez-le en arrière-plan :
   ```
   bg %1
   ```
4. Ramenez un processus en premier plan :
   ```
   fg %1
   ```

---

## Exercice 4 : Terminer un processus

### Commandes : `kill` et `ps`

1. Identifiez un processus à l’aide de `ps` :
   ```
   ps aux | grep sleep
   ```
2. Notez le **PID** du processus.
3. Terminez le processus avec la commande `kill` :
   ```
   kill <PID>
   ```
4. Pour forcer l’arrêt d’un processus :
   ```
   kill -9 <PID>
   ```



