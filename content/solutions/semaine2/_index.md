+++
title = "Atelier 2"
weight = 172
+++

# Solution des exercices

---

## Exercice 1 : Explorer l’arborescence Linux

1. **Afficher le chemin de votre répertoire courant :**
   ```bash
   $ pwd
   ```

2. **Aller dans `/usr/share/doc` et vérifier le chemin :**
   ```bash
   $ cd /usr/share/doc
   $ pwd
   ```

3. **Remonter dans le répertoire parent :**
   ```bash
   $ cd ..
   $ pwd
   ```

4. **Retourner dans le répertoire personnel :**
   ```bash
   $ cd ~
   $ pwd
   ```

5. **Lister les fichiers présents dans le répertoire courant :**
   ```bash
   $ ls
   ```

6. **Lister les fichiers du répertoire `/usr` :**
   ```bash
   $ ls /usr
   ```

---

## Exercice 2 : Commandes Linux simples

1. **Afficher la date et l'heure actuelles :**
   ```bash
   $ date
   $ date +"%r"
   ```

2. **Afficher les 10 premières lignes de `/etc/services` :**
   ```bash
   $ head /etc/services
   ```

3. **Afficher les 10 dernières lignes de `/etc/services` :**
   ```bash
   $ tail /etc/services
   ```

4. **Répéter la commande précédente en trois frappes :**
   ```bash
   $ tail /etc/services  # (Utilisez la flèche "haut" pour la rappeler)
   ```

5. **Afficher les 20 dernières lignes :**
   ```bash
   $ tail -n 20 /etc/services
   ```

6. **Réutiliser l’historique pour afficher l’heure :**
   ```bash
   $ history
   $ !<numéro de la commande date +"%r">
   ```

---

## Exercice 3 : Commandes de base

1. **Créer le répertoire `Atelier2` :**
   ```bash
   $ mkdir Atelier2
   ```

2. **Copier le fichier `fichier.txt` dans `Atelier2` :**
   ```bash
   $ cp fichier.txt Atelier2/
   ```

3. **Créer le répertoire `Rep2` :**
   ```bash
   $ mkdir Rep2
   ```

4. **Déplacer `Atelier2` dans `Rep2` :**
   ```bash
   $ mv Atelier2 Rep2/
   ```

5. **Se déplacer dans `Atelier2` :**
   ```bash
   $ cd Rep2/Atelier2
   ```

6. **Modifier `fichier.txt` avec vim :**
   ```bash
   $ vim fichier.txt
   ```
   (Écrire votre nom complet, enregistrer et quitter avec `:wq`).

7. **Afficher le contenu de `fichier.txt` :**
   ```bash
   $ cat fichier.txt
   ```

8. **Créer `fichier2.txt` :**
   ```bash
   $ touch fichier2.txt
   ```

9. **Afficher le contenu des deux fichiers avec `cat` :**
   ```bash
   $ cat fichier.txt fichier2.txt
   ```

10. **Revenir dans le répertoire personnel :**
    ```bash
    $ cd ~
    ```

11. **Supprimer le répertoire `Rep2` :**
    ```bash
    $ rm -r Rep2
    ```

12. **Afficher le répertoire courant :**
    ```bash
    $ pwd
    ```

13. **Créer `Rep3` dans `/root` :**
    ```bash
    $ mkdir /root/Rep3
    ```
    (Peut échouer sans `sudo`).

14. **Lister le contenu de `/etc` avec `-l` :**
    ```bash
    $ ls -l /etc
    ```

15. **Identifier les caractères au début des lignes :**
    (Réponse : `d` pour répertoire, `-` pour fichier, `l` pour lien symbolique).

16. **Différence de `/proc` :**
    (Réponse : Contient des fichiers virtuels donc éphémères, représentant des informations sur le système).

17. **Différence entre `/bin` et `/sbin` :**
    (Réponse : `/bin` contient des binaires pour tous les utilisateurs, `/sbin` est réservé à l’administration).

18. **Répertoire du noyau :**
    (Réponse : `/boot`).

19. **Répertoire pour une clé USB :**
    (Réponse : `/media` ou `/mnt`).

20. **Répertoire pour Apache :**
    (Réponse : `/etc/apache2` ou `/etc/httpd`, selon la distribution).
