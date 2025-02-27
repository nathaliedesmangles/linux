+++
title = "Test 1"
weight = 171
+++

## Critères de correction appliqués

| Question | Points | -100% | -75% | -50% | -25% | Réponses |
|----------|:--------:|--------|--------|--------|--------|----------|
| **1** | **3** | `cd` absent <br>cd ../../home/user<br>cd root| | cd /home/user <br> cd /home <br>~ <br>cd /~ |  | cd ~ |
| **2** | **2** | mkdir absente <br> autre commande | | mkdir /home/user/projets/python/scripts <br> mkdir projets/python/scripts | mkdir -p /home/user/projets/python/scripts | mkdir -p projets/python/scripts |
| **3** | **2** | sudo seul <br>Flèche <br> Mauvaise commande (ex: history -!100)| | history !sudo | | !sudo <br> sud tab |
| **4** | **2** | Mauvais caractère générique | | find -name <br> pas assez de `?` | 8 `?` | ls log?????.txt <br> ls-l log?????.txt |
| **5** | **2** | Mauvaise commande<br> Boucle  | touch rapport_20{00,01,02, ..., 25}.txt <br> mkdir rapport_{2000..2025} | touch /rapport_20{00..25}<br> touch rapport_20{00..25} | Toutes les années<br> Extension manquante | touch rapport_{2000..2025}.txt <br> touch rapport_20{00..25}.txt |
| **6** | **2** | Mauvaise syntaxe de la boucle <br> Mauvaise commande (ex : rmdir) | | Mauvais chemin<br>pas reutiliser la variable | | for i in /home/user/Documents/*.bak; do rm "$i"; done |
| **7** | **2** | Commande **et** chemin erronés (ex: cd ../../var/log)| | Mauvais chemin relatif (ex: ls ../../var/log) <br>  Mauvaise commande et bon chemin (ex: cd /var/log)| | ls /var/log <br> ls -l /var/log |
| **8** | **2** | Commande et chemin erronés <br>Chemin relatif erroné<br> Mauvaise commande (ex: mv)| | cd /home/user/Documents/projets/developpement/scripts<br>cd /developpement/scripts <br>cd developpement| | cd developpement/scripts |
| **9** | **2** | Option manquante<br> Mauvaise commande | | head -15 data.csv | | head -n 15 data.csv <br> head data.csv -n 15<br>head -15 data.csv<br>head 15 data.csv |
| **10** | **2** | Mauvaise commande | | tail -n 10 data.csv <br> tail 10 data.csv| | tail data.csv | 
| **11** | **2** | Mauvaise commande | | history !-2 <br> history !49<br> history 49<br>!2| | !-2<br> !49 <br>!48 |
| **12** | **2** | Absence de boucle<br> Syntaxe de la boucle | | Mauvaise extension<br> Mauvais chemin<br> Mauvaise commande | | for i in *.log; do echo $i; done |
| **13** | **2** | sudo absent **et** mauvaise commande/chemin| | sudo absent + rm + chemin <br>sudo présent + chemin, mais mauvaise commande (ex : rmdir) | | sudo rm /etc/secret.conf |
| **14** | **4** | Mauvaise commande | | ls *.log *.txt *.csv<br>ls -name {*.log, *.txt, *.csv}| | ls *.{log,txt,csv}<br> ls *{.log,.txt,.csv}|
| **15** | **3** | Mauvaise commande (ex : mv) <br> syntaxe erronée| | syntaxe `cp` inversée<br>Toutes les années<br> copy backup_{2000 .. 2025}.tar /mnt/archives/<br>Extension manquante | | cp backup_{2000..2025}.tar /mnt/archives <br> cp backup_20{00..25}.tar /mnt/archives <br>cp backup_{2000..2025}.{b,t}ar /mnt/archives|
| **16** | **2** | Mauvaise commande |seulement la commande | Tous les noms <br> Extension manquante | Nombres impairs| mv config-{2,4,6,8,10}.txt configs/ |
| **17** | **2** | Pas de commande<br>Mauvaise commande (ex : ls) | | Mauvais chemin<br>Commande `find` sans l’option `-name`| | find /home/user/scripts -name "*.sh" |
| **18** | **2** | Commande autre que systemctl, init | | Absence d’isolate <br>Utilisation de runlevel (init)<br> Mauvaise cible| | systemctl isolate multi-user.target<br> systemctl isolate multi-user |
| **19** | **5** | Aucune des 2 réponses sont bonnes | | 1 seule des 2 réponses est bonne|  | 1. systemctl multi-user.target: requiert un redémarrage. 2. systemctl isolate multi-user.target : ne requiert pas de redémarrage|
| **20** | **5** | Aucune des 2 réponses sont bonnes |  | 1 seule des 2 réponses est bonne | | 1. touch tests/test{1..5}.log <br>2. ls tests |
| **TOTAL** | **50** | | | | | |


## Rappels des notions de base importantes non réussies

1. **Syntaxe de base d'une commande dans l'ordre**

   ```bash
   commande -option arguments
   ```

   - **commande** : action à exécuter.
   - **option** : modifie le comportement de la commande. Généralement commence par le symbole `-` (moins).
   - **arguments** : cible sur laquelle la commande s'applique. Peut être un chemin vers un **fichier/répertoire**, un **texte**, un **nombre**, etc.

2. **Chemin relatif vs absolu**

   - Un **chemin absolu** commence toujours par `/`.
   - Les caractère `/` correspond à la racine de l'arborescence de Linux [voir cours semaine 2](https://linuxh25.netlify.app/semaine2/cours/).
   - Un **chemin relatif** NE COMMENCE PAS par `/`. Dépendamment de où on se trouve, un chemin relatif commencera soit par:
      - le nom (chemin) du répertoire/fichier à atteindre.
      - Un ou plusieurs `../` pour remonter dans l'arborescence.

3. **La commande *cd***

   - **`cd`** ➝ *Change Directory*, se déplacer dans l'arborescence de fichiers/repertoires de Linux.

4. **Difference entre *find* et *ls*** 
 
   - **`ls`** → Affiche le contenu d'un répertoire donné.  
   - **`find`** → Recherche des fichiers/dossiers selon des critères (nom, taille, date, etc.), même dans les sous-dossiers.  

   **Exemple concret** :  
   - **Lister tous les fichiers `.txt`** dans le répertoire courant :  
     ```bash
     ls *.txt
     ```
     ➝ Ne fonctionne que pour le répertoire actuel. 
 
   - **Trouver tous les fichiers `.txt`** dans tous les sous-dossiers :  
     ```bash
     find . -name "*.txt"
     ```
     ➝ Recherche dans le dossier actuel **et tous ses sous-dossiers**.

5. Les commandes touch et mkdir

   - **`touch`** ➝ création de fichiers
   - **`mkdir`** ➝ création de répertoires (**dir**ectory)
      - L'option `-p` permet de créer les sous répertoires 

6. **Boucle for**

   La syntaxe:
   ```bash
   for variable in liste
   do
       commande
   done
   ```

   - **variable** : la variable qui prendra successivement les valeurs de liste.
   - **liste** : une séquence de valeurs (peut être une liste explicite, une plage de nombres, une liste de fichiers, etc.).
   - **commande** : l'instruction exécutée à chaque itération.

   **Exemples:**
   ```bash
   for fruit in pommes bananes oranges	# Pas de virgule entre les arguments
   do
       echo "J'aime les $fruit"		# $fruit = affiche le nom du fruit traité
   done
   ```
   🡪 Affiche 
   ```
   J'aime les pommes
   J'aime les bananes
   J'aime les oranges
   ```
   ```bash
   for fichier in *.txt
   do
       echo "Traitement de $fichier"
   done
   ```
   🡪 Affiche les noms des fichiers `.txt` dans le dossier courant.


   **NB**: Si la liste représente un chemin vers un fichier/répertoire, cela ne veut pas dire qu'on est dedans, mais que la variable aura comme valeur les fichiers/répertoires **un à un**.

   **Ex**: `$(find /home/user/Documents -name "*.bak")` **cherche** tous les répertoires dont le **nom** contient `Documents` et non les fichiers contenant `.bak`.


7. **L'expansion d'accolades** { }

8. **Rôle de *isolate* dans la commande *systemctl***

   - Dans `systemctl`, la commande `isolate` sert à basculer **immédiatement** vers une cible (target) **sans avoir à redémarrer** le système.
   - `isolate` **ne redémarre pas la machine**, mais change l’environnement d’exécution.
