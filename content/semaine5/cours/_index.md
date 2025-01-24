+++
title = "Les processus de Linux"
weight = 51
draft = true
+++

## Qu'est-ce qu'un processus ?

Un **processus** est une application ou une commande en cours d'exécution. Certains processus s'arrêtent automatiquement une fois leur tâche terminée, tandis que d'autres continuent de s'exécuter jusqu'à ce que vous les arrêtiez vous-même.

---

## Exemple de processus

1. **Commande `ls` :**  
   Cette commande affiche le contenu d’un dossier, s’exécute, puis se termine immédiatement. Vous pouvez enchaîner avec une autre commande.  
   ```bash
   $ ls
   ```
2. **Commande `firefox` :**  
   Cette commande ouvre le navigateur Firefox. Tant que Firefox est ouvert, la commande reste active et bloque le terminal.  
   ```bash
   $ firefox
   ```

---

## Exécution en arrière-plan

Si une commande empêche l’utilisation du terminal, c’est parce qu’elle s’exécute au **premier plan**. Voici comment continuer à utiliser le terminal :

1. **Lancer une commande directement en arrière-plan :**  
   Ajoutez `&` à la fin de la commande.  
   ```bash
   $ firefox &
   ```

2. **Passer une commande déjà en cours au second plan :**  
   - Appuyez sur `Ctrl + Z` pour suspendre temporairement la commande.  
   - Tapez `bg` pour la reprendre en **arrière-plan**.

3. **Revenir au premier plan :**  
   Utilisez `fg`.  
   ```bash
   $ fg
   ```


### Exercices 1

1. Lancez Firefox. Faites-le passer en arrière-plan puis ramenez-le au premier plan.  
2. Fermez Firefox depuis le terminal en tapant `Ctrl + C`.

---

## Visualiser les processus

Pour afficher les processus lancés depuis le terminal, utilisez :  
```bash
$ ps -f
```

Chaque processus est identifié par deux numéros :  
- **PID** : Identifiant unique du processus.  
- **PPID** : Identifiant du processus père (celui qui a lancé le processus).

**Exemple :**  
Si vous lancez une commande dans un terminal, ce terminal devient le **processus père**.


### Exercices 2

1. Notez le **PID** de votre shell avec `ps`.  
2. Lancez Firefox et notez son **PID** et son **PPID**. Quel est le **PPID** de Firefox ?  

---

## États des processus

Un processus peut être dans différents états :  
- **Élu :** En cours d’exécution.  
- **Prêt :** En attente d’être exécuté.  
- **Bloqué :** En attente d’une ressource (par ex. disque).  
- **Zombie :** Terminé, mais le processus père n’a pas encore pris en compte sa fin.

Utilisez `top` pour surveiller les processus et leur consommation de ressources :  
```bash
$ top
```


### Exercices 3

1. Lancez Firefox en tâche de fond. Notez son **PID** et son **PPID**.  
2. Tuez le parent de Firefox. Quel est le nouveau **PPID** de Firefox ?

---

## Gestion des processus

- **Arrêter un processus :**  
  ```bash
  $ kill <PID>
  ```
  Pour forcer l’arrêt :  
  ```bash
  $ kill -9 <PID>
  ```

- **Tuer tous les processus d’un même nom :**  
  ```bash
  $ killall <nom_du_processus>
  ```

- **Préserver un processus si le terminal est fermé :**  
  - Avant fermeture :  
    ```bash
    $ disown <PID>
    ```
  - Lors du lancement :  
    ```bash
    $ nohup commande &
    ```

### Exercices 4

1. Lancez la commande suivante :  
   ```bash
   $ grep <fichier>
   ```
   - Trouvez le **PID** avec un autre terminal et tuez le processus.  
2. Lancez Firefox en tâche de fond, puis fermez le terminal.  
   - Réessayez avec `disown`.  
   - Essayez ensuite avec `nohup firefox`.

---

## Codes de retour des commandes

Chaque commande retourne un code :  

- **0** : Succès.  
- **Différent de 0** : Erreur.

Pour afficher le code de retour de la dernière commande :  
```bash
$ echo $?
```


### Exercices 5

1. Lancez `ls`. Quel est son code de retour ?  
2. Essayez :  
   ```bash
   $ find / -name "*.conf"
   ```
   Quel est le code de retour ? Pourquoi ?

---

## Combinaison de commandes

La **combinaison de commandes** permet de lier plusieurs commandes dans un même processus, facilitant ainsi l'automatisation et le traitement de données en une seule étape. 

Elle s'effectue grâce à des opérateurs comme `|` (pipe), `&&` (exécuter si la commande précédente réussit) ou `;` (exécuter séquentiellement).

1. **Exécuter successivement :**  
   ```
   $ commande1 ; commande2
   ```
2. **Exécuter en parallèle :**  
   ```
   $ commande1 & commande2
   ```
3. **Exécuter si succès :**  
   ```
   $ commande1 && commande2
   ```
4. **Exécuter si échec :**  
   ```
   $ commande1 || commande2
   ```


### Exercices 6

1. Testez :  
   ```bash
   $ find / -name "*.conf" && ls
   ```
   Que se passe-t-il si vous inversez les commandes ?  
2. Testez :  
   ```bash
   $ find / -name "*.conf" || ls
   ```
   Observez les différences.

---

## Création de scripts Bash

Un script Bash est un fichier exécutable contenant des commandes.  

1. Créez un fichier :  
   ```bash
   $ vim script.sh
   ```
2. Ajoutez cette entête :  
   ```
   #!/bin/bash
   ```
3. Ajoutez des commandes :  
   ```
   echo "Bonjour"
   pwd
   touch fichier{1..5}.txt
   ```
4. Exécutez-le :  
   ```bash
   $ bash script.sh
   ```

Pour lancer des tâches en parallèle dans un script, utilisez `&` et `wait` :  
```
#!/bin/bash
(cp dossier1/* destination1 &)
(cp dossier2/* destination2 &)
wait
echo "Copie terminée"
```

