+++
title = "Les processus de Linux"
weight = 51
draft = true
+++

### Introduction à l'éditeur de texte **vim**

**vim** (Vi IMproved) est un éditeur de texte très puissant, souvent utilisé dans les environnements Unix/Linux. Il est particulièrement adapté pour les utilisateurs qui souhaitent travailler rapidement avec un clavier sans souris. Bien qu’il puisse sembler intimidant au premier abord, il devient très efficace une fois maîtrisé.  

#### Pourquoi utiliser **vim** ?
- **Disponibilité** : Installé par défaut sur presque tous les systèmes Unix/Linux.  
- **Léger et rapide** : Idéal pour éditer des fichiers même sur des systèmes limités en ressources.  
- **Personnalisable** : Peut être configuré pour répondre à vos besoins spécifiques.  
- **Puissant** : Supporte des fonctionnalités avancées comme la recherche, la substitution, et l'édition de plusieurs fichiers simultanément.  

---

### Premiers pas avec **vim**

Pour ouvrir un fichier avec **vim**, utilisez la commande suivante :  
```bash
$ vim nom_du_fichier
```
Si le fichier n'existe pas, **vim** le créera.

Lorsque vous ouvrez **vim**, il commence en **mode commande**. Vous ne pouvez pas directement écrire du texte. Vous devez d'abord passer au **mode insertion**.  

---

### Modes principaux de **vim**

1. **Mode commande** (par défaut)  
   - Permet de naviguer, de sauvegarder, et d'effectuer d'autres actions sur le fichier.  
   - Appuyez sur `Esc` pour revenir à ce mode.  

2. **Mode insertion**  
   - Permet d’écrire du texte dans le fichier.  
   - Pour passer en mode insertion, appuyez sur `i`.  

3. **Mode ligne de commande**  
   - Utilisé pour exécuter des commandes (sauvegarder, quitter, rechercher, etc.).  
   - Appuyez sur `:` en mode commande pour l’activer.  

---

### Commandes de base pour débutants

#### Édition
- **i** : Passer en mode insertion.  
- **o** : Ajouter une nouvelle ligne et passer en mode insertion.  
- **x** : Supprimer un caractère sous le curseur.  

#### Navigation
- Flèches directionnelles : Déplacer le curseur (ou utiliser les touches `h` (gauche), `j` (bas), `k` (haut), `l` (droite)).  
- `gg` : Aller au début du fichier.  
- `G` : Aller à la fin du fichier.  

#### Sauvegarder et quitter
- `:w` : Sauvegarder les modifications.  
- `:q` : Quitter si aucune modification n’a été effectuée.  
- `:wq` ou `:x` : Sauvegarder et quitter.  
- `:q!` : Quitter sans sauvegarder.  

#### Recherche
- `/mot` : Rechercher un mot ou une phrase (appuyez sur `n` pour trouver la prochaine occurrence).  
- `?mot` : Rechercher en remontant dans le fichier.  

#### Annuler et rétablir
- `u` : Annuler la dernière modification.  
- `Ctrl+r` : Rétablir une modification annulée.  

---

### Exercices pratiques

1. **Ouvrez un fichier** nommé `test.txt` avec la commande :  
   ```bash
   $ vim test.txt
   ```  
   Passez en mode insertion (`i`), écrivez quelques lignes, puis sauvegardez et quittez avec `:wq`.

2. **Recherchez du texte** : Ouvrez un fichier existant, cherchez un mot avec `/mot`, puis naviguez entre les occurrences avec `n`.

3. **Testez l'annulation** : Modifiez une ligne, annulez avec `u`, puis rétablissez avec `Ctrl+r`.

---

### Astuces pour les débutants
- **Soyez patient !** vim peut être difficile au début, mais une fois que vous le maîtrisez, il devient un outil très puissant.  
- Entraînez-vous régulièrement avec les commandes de base avant d'apprendre les fonctionnalités avancées.  
- Si vous êtes bloqué, quittez avec `:q!` sans sauvegarder et réessayez.  

Avec le temps, **vim** deviendra un outil incontournable pour éditer vos fichiers rapidement et efficacement.

=================

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


