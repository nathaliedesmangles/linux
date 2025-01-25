+++
title = "Atelier 3"
weight = 163
draft = true
+++

# Solution des exercices

## Exercice 1 : Manipuler les cibles (niveaux d'exécution)

1. **Passer en mode multi-utilisateur sans interface graphique :**
   ```bash
   $ sudo systemctl isolate multi-user.target
   ```

2. **Vérifier que vous êtes en mode multi-utilisateur sans interface graphique :**
   ```bash
   $ systemctl get-default
   ```
   La sortie devrait être `multi-user.target`.

3. **Définir le mode multi-utilisateur avec interface graphique comme cible par défaut :**
   ```bash
   $ sudo systemctl set-default graphical.target
   ```

4. **Redémarrer le système pour vérifier :**
   ```bash
   $ sudo reboot
   ```

---

## Exercice 2 : Création et affichage de variables

1. **Déclarer une variable `nom` :**
   ```bash
   $ nom="VotrePrénom"
   ```

2. **Afficher la valeur de la variable :**
   ```bash
   $ echo $nom
   ```

3. **Essayer d’accéder à la variable sans `$` :**
   ```bash
   $ nom
   ```
   La commande retournera une erreur.

---

## Exercice 3 : Capturer une date formatée

1. **Stocker la date actuelle dans une variable :**
   ```bash
   $ date_actuelle=$(date +"%Y/%m/%d %H:%M:%S")
   ```

2. **Afficher la date formatée :**
   ```bash
   $ echo $date_actuelle
   ```

---

## Exercice 4 : Supprimer une variable

1. **Déclarer une variable temporaire :**
   ```bash
   $ temp_var="temporaire"
   ```

2. **Supprimer la variable avec `unset` :**
   ```bash
   $ unset temp_var
   ```

3. **Essayer d’afficher la variable supprimée :**
   ```bash
   $ echo $temp_var
   ```

---

## Exercice 5 : Expansion de variables et d'accolades

1. **Créer une variable contenant la liste des fichiers dans `/etc` :**
   ```bash
   $ variable_etc=$(ls /etc)
   $ echo $variable_etc
   ```

   - Le contenu peut être difficile à lire car tout est affiché sur une seule ligne.

   **Exécuter `ls` sur la variable :**
   ```bash
   $ ls $variable_etc
   ```
   - Peut afficher une erreur si des fichiers n'existent pas dans le répertoire courant.

2. **Trouver les fichiers `.conf` et stocker dans une variable :**
   ```bash
   $ fichiers_conf=$(find /etc -type f -name "*.conf")
   ```

   **Exécuter `ls` sur cette variable :**
   ```bash
   $ ls $fichiers_conf
   ```
   - Peut produire une erreur similaire si les chemins complets ne sont pas valides.

   **Afficher la taille de chaque fichier `.conf` :**
   ```bash
   $ for fichier in $fichiers_conf; do du -sh "$fichier"; done
   ```

3. **Créer des fichiers avec factorisation :**
   ```bash
   $ mkdir test_dir
   $ touch test_dir/test{1,2,3}.{txt,doc,tot}
   ```

4. **Afficher uniquement les fichiers `.txt` commençant par `test` :**
   ```bash
   $ ls test_dir/test*.txt
   ```

   **Afficher tous les fichiers `.txt` et `.tot` :**
   ```bash
   $ ls test_dir/*.{txt,tot}
   ```

   **Afficher tous les fichiers `test1` :**
   ```bash
   $ ls test_dir/test1.*
   ```

---

## Exercice 6 : Expansion d’accolade et boucle for


1. **Créer l'arborescence avec expansion d’accolade :**
   ```bash
   $ mkdir -p coursLinux/semaine{1..5}/{lab,lecon}
   ```

2. **Créer un fichier `priseNote` dans chaque répertoire `lab` :**
   ```bash
   $ touch coursLinux/semaine{1..5}/lab/priseNote
   ```

3. **Renommer `priseNote` en `priseNote.txt` :**
   ```bash
   $ for fichier in coursLinux/semaine{1..5}/lab/priseNote; do mv "$fichier" "${fichier}.txt"; done
   ```

4. **Déplacer `priseNote.txt` vers le répertoire `lecon` correspondant :**
   ```bash
   $ for semaine in coursLinux/semaine{1..5}; do mv "$semaine/lab/priseNote.txt" "$semaine/lecon/"; done
   ```