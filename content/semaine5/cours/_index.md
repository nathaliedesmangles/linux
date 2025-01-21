+++
title = "Les processus de Linux"
weight = 51
draft = true
+++


Un processus est une instance d'un programme en cours d'exécution. Sous Linux, les processus jouent un rôle central dans la gestion des tâches et des ressources. 

Dans cette leçon nous voyons comment Linux gère les processus, ainsi que les commandes essentielles pour les superviser et les contrôler.

---

## Qu'est-ce qu'un processus ?

Un processus est une entité active qui exécute des instructions d'un programme. Il inclut :
- **Code exécutable** : Les instructions du programme.
- **Espace mémoire** : Contient les variables, les données, et la pile d'exécution.
- **Identifiant unique (PID)** : Chaque processus a un PID unique pour l'identifier.

Les processus peuvent être classés en deux catégories principales :
- **Processus parents** : Ceux qui initient d'autres processus.
- **Processus enfants** : Créés par un processus parent.

---

## Types de processus

1. **Processus en premier plan (foreground)** :
   - Exécutés directement dans le terminal et occupent l'entrée/sortie standard.
   - Exemple :
     ```
     nano fichier.txt
     ```

2. **Processus en arrière-plan (background)** :
   - Exécutés sans bloquer le terminal.
   - Exemple :
     ```
     ./script.sh &
     ```

3. **Démons** :
   - Processus s'exécutant en tâche de fond pour des services système (comme `sshd`).

---

## Gestion des processus

### Commandes de base pour superviser les processus

1. **`ps` (Process Status)** :
   - Affiche des informations sur les processus en cours.
   - Exemple :
     ```
     ps
     ps aux  # Affiche tous les processus avec des détails
     ```

2. **`top`** :
   - Affiche une vue interactive des processus en temps réel.
   - Contrôles :
     - `q` : Quitter
     - `h` : Aide

3. **`htop`** :
   - Une alternative à `top` avec une interface plus conviviale.

4. **`jobs`** :
   - Liste les processus en arrière-plan du terminal actuel.
   - Exemple :
     ```
     jobs
     ```

5. **`kill`** :
   - Termine un processus en utilisant son PID.
   - Exemple :
     ```
     kill 1234  # Termine le processus avec le PID 1234
     kill -9 1234  # Forcer l’arrêt
     ```

6. **`bg` (Background)** :
   - Reprend un processus arrêté en arrière-plan.
   - Exemple :
     ```
     bg %1
     ```

7. **`fg` (Foreground)** :
   - Reprend un processus en premier plan.
   - Exemple :
     ```
     fg %1
     ```

8. **`nice` et `renice`** :
   - Modifient la priorité d'un processus.
   - Exemple :
     ```
     nice -n 10 ./script.sh
     renice 5 -p 1234  # Change la priorité du PID 1234
     ```


