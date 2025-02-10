+++
title = "Test 1 - groupes"
weight = 171
draft = true
+++


2. Comment rechercher récursivement tous les fichiers contenant le mot "config" dans le répertoire /etc et ses sous-répertoires ?

* **Commande:** `grep -r "config" /etc`

2. Vous êtes dans le répertoire /etc et vous voulez rechercher toutes les occurrences du mot "password" dans tous les fichiers .conf. Quelle commande utiliserez vous ?
   * **Réponse :** `grep -r "password" *.conf`

2. OK Vous avez plusieurs fichiers de configuration dans le répertoire /etc. Vous voulez afficher toutes les lignes contenant le mot "port" dans tous ces fichiers. Quelle commande utiliserez vous ?
    * **Réponse :** `grep -r "port" /etc`

2. OK Vous avez un fichier de configuration `config.ini` qui contient des informations sensibles. Vous souhaitez afficher uniquement les lignes contenant le mot "password". Quelle commande utiliserez vous ? 
   * **Réponse:** `grep "password" config.ini`

2. OK2 Vous voulez vérifier si le mot "erreur" apparaît dans le fichier de configuration httpd.conf. Quelle commande utiliserez-vous ?
    * **Réponse :** `grep "erreur" httpd.conf`

2. Vous souhaitez rechercher tous les fichiers contenant le mot "rapport" dans tous les sous-répertoires de `Projets`. **Question:** Quelle commande utiliserez vous ?
    * **Réponse:** 
        1. `grep -r "rapport" .`

---


3. OK2 Vous souhaitez créer une copie de sauvegarde du fichier important.txt avant de le modifier. Quelle commande utiliserez-vous ?
    * **Réponse :** `cp important.txt important.txt.sauvegarde`

---

4. OK Vous souhaitez déplacer le fichier /config.ini vers un répertoire ancien_config. Créez le répertoire ancien_config puis déplacez le fichier config.ini vers ce répertoire. Quelles commandes utilisez-vous ?**
    * **Réponse :**
        1. `mkdir ancien_config`
        2. `mv config.ini ancien_config`


4. OK Vous avez plusieurs fichiers `.txt` dans votre répertoire actuel. Vous souhaitez tous les déplacer dans un nouveau sous-répertoire nommé `fichiers_txt`. Quelles commandes utilisez-vous ?
    * **Réponse :**
        1. `mkdir documents`
        2. `mv *.txt documents`

4. OK Vous avez créé un nouveau répertoire nommé `Archive` dans le répertoire `Projets`. Vous souhaitez déplacer tous les fichiers dont l'extension est `.bak` vers ce nouveau répertoire. **Question:** Quelles commandes utiliserez-vous ? 
    * **Réponse:** 
        1. `mkdir Archive`
        2. `mv *.bak Archive`

4. ??? Vous souhaitez déplacer tous les fichiers .jpg présents dans le répertoire /home/utilisateur/Images vers un nouveau répertoire nommé "archives". Quelle commande utiliserez-vous ?
   * **Réponse :** 
        1. `mkdir archives
        2. `mv *.jpg archives` (à exécuter depuis le répertoire /home/utilisateur/Images)

---

5. OK Vous avez installé un nouveau noyau Linux et vous souhaitez redémarrer votre système pour appliquer les modifications. Quelle commande utiliserez vous ?
    * **Réponse:** `reboot` ou `shutdown -r now`
    * **Explication:** Ces deux commandes redémarrent le système immédiatement.

5. OK Vous avez effectué une mise à jour majeure du système et vous souhaitez redémarrer pour appliquer les changements, mais vous voulez afficher un message aux utilisateurs connectés avant l'arrêt. Quelle commande utiliserez vous ?**
    * **Réponse:** `shutdown -r now "Le système va redémarrer pour la mise à jour. Veuillez enregistrer votre travail."`
    * **Explication:** Cette commande redémarre immédiatement le système et affiche le message spécifié aux utilisateurs connectés.


---

Vous êtes toujours dans le répertoire `Projets` et vous avez une structure de fichiers similaire à celle de la question précédente (avec des fichiers `.log` répartis dans différents sous-dossiers).

1. Vous souhaitez afficher la taille totale (en octets) de tous les fichiers `.log` dans le répertoire `Projets` et ses sous-dossiers. Quelle commande utiliserez vous ? 
   * **Réponse:** `du -sch *.log`
   * **Explication:**
     * `du`: calcule la taille des fichiers et des répertoires.
     * `-s`: affiche uniquement la taille totale de chaque argument.
     * `-c`: affiche un total général.
     * `h`: affiche les tailles en format lisible par l'homme (Ko, Mo, Go).
     * `*.log`: cible tous les fichiers avec l'extension `.log`.

2. Vous voulez copier tous les fichiers `.log` commençant par "journal2" dans un nouveau répertoire nommé "archives". Quelle commande utiliserez vous ? 
   * **Réponse:** 
     1. `mkdir archives`
     2. `find . -name "journal2*" -exec cp {} archives \;`
   * **Explication:**
     * `find . -name "journal2*"`: cherche tous les fichiers dont le nom commence par "journal2" dans le répertoire courant et ses sous-répertoires.
     * `-exec cp {} archives \;`: exécute la commande `cp` pour copier chaque fichier trouvé vers le répertoire "archives".

3. Vous souhaitez supprimer tous les fichiers `.log` qui ont plus de 30 jours. Quelle commande utiliserez-vous ? (Note : assumez que `find` supporte l'option `-mtime +30` pour les fichiers modifiés il y a plus de 30 jours)
   * **Réponse:** `find . -name "*.log" -mtime +30 -delete`
   * **Explication:**
     * `find . -name "*.log"`: cherche tous les fichiers avec l'extension `.log`.
     * `-mtime +30`: sélectionne les fichiers modifiés il y a plus de 30 jours.
     * `-delete`: supprime les fichiers correspondants.

4. Vous voulez afficher les 10 premières lignes de tous les fichiers `.log` dans le répertoire `Projets` et ses sous-répertoires. Quelle commande utiliserez-vous ?
   * **Réponse:** `find . -name "*.log" -exec head -n 10 {} \;`
   * **Explication:**
     * `find . -name "*.log"`: cherche tous les fichiers avec l'extension `.log`.
     * `-exec head -n 10 {} \;`: exécute la commande `head -n 10` (afficher les 10 premières lignes) sur chaque fichier trouvé.



---

2. OK Vous avez constaté une anomalie dans le système de fichiers et vous souhaitez le réparer. Après avoir effectué les réparations nécessaires, quelle commande utiliserez vous pour redémarrer en mode sans échec afin de vérifier si le problème est résolu ?
    * **Réponse:** `reboot -x` (pour les systèmes utilisant systemd) ou `reboot --safe` (pour certaines distributions) 


3. Vous devez arrêter complètement votre serveur et vous voulez vous assurer qu'aucun processus ne soit interrompu brutalement. Quelle commande utiliserez vous ?
    * **Réponse:** `shutdown -h now`
    * **Explication:** Cette commande arrête le système de manière propre, en donnant le temps aux processus en cours de se terminer.


2. Vous avez un fichier log.txt qui devient trop volumineux. Vous souhaitez en créer une copie pour le conserver et supprimer les 1000 premières lignes du fichier d'origine. Quelles commandes utilisez-vous ?
    * **Réponse :**
        1. `cp log.txt log.txt.sauvegarde`
        2. `tail -n +1001 log.txt > temp.txt`
        3. `mv temp.txt log.txt`


Vous êtes toujours dans le dossier `Projets` et vous avez besoin de créer de nouveaux fichiers de configuration pour différents environnements.

1. Vous souhaitez créer cinq fichiers de configuration nommés `config_prod.ini`, `config_dev.ini`, `config_test.ini`, `config_staging.ini` et `config_local.ini`. Écrivez une commande utilisant l'expansion d'accolades pour créer ces fichiers.
   * **Réponse:** `touch config_{prod,dev,test,staging,local}.ini`

2. Vous avez besoin de créer des fichiers de journalisation pour différents modules de votre application : `module1.log`, `module2.log`, et `module3.log`. De plus, vous souhaitez créer des fichiers de sauvegarde pour chacun de ces fichiers, avec l'extension `.bak`. Écrivez une commande utilisant l'expansion d'accolades pour créer ces fichiers.
   * **Réponse:** `touch module{1,2,3}.{log,.bak}`

3. Vous voulez créer des fichiers de sauvegarde pour les fichiers de configuration existants (dont les noms commencent par "config_"). Les fichiers de sauvegarde doivent avoir le même nom, mais avec l'extension `.bak`. Écrivez une commande utilisant une wildcard et l'expansion d'accolades pour créer ces fichiers.
   * **Réponse:** `cp config_* config_{}.bak`

4. Vous avez besoin de créer des répertoires pour différents projets, nommés `projet_A`, `projet_B`, et `projet_C`. Dans chaque répertoire, vous voulez créer un fichier `README.md`. Écrivez une commande utilisant l'expansion d'accolades pour créer ces répertoires et fichiers.
   * **Réponse:** `for i in A B C; do mkdir projet_$i && touch projet_$i/README.md; done`

5. Vous souhaitez créer des fichiers de rapport pour différentes périodes (mois). Les fichiers seront nommés `rapport_mois_1.txt`, `rapport_mois_2.txt`, etc., jusqu'à `rapport_mois_12.txt`. Écrivez une commande utilisant une séquence numérique dans l'expansion d'accolades pour créer ces fichiers.
   * **Réponse:** `for i in {1..12}; do touch rapport_mois_$i.txt; done`

---

1. Vous travaillez sur un projet où vous avez de nombreux fichiers de données avec des noms similaires.

1. Vous avez des fichiers de configuration nommés `config_partie1.conf`, `config_partie2.conf`, etc. Vous souhaitez copier tous ces fichiers dans un répertoire nommé `backup`. Écrivez un script utilisant une boucle `for` et une expression régulière pour effectuer cette tâche.
   * **Réponse:**
     ```bash
     for file in config_*.conf; do
         cp "$file" backup/
     done
     ```

1. **Question 11:** Vous avez des fichiers de log avec des dates dans leur nom (par exemple, `log_20230401.txt`). Vous souhaitez supprimer tous les fichiers de log plus anciens que 30 jours. Utilisez `find` et une boucle `for` pour réaliser cette tâche.
   * **Réponse:**
     ```bash
     find . -name "log_*.txt" -mtime +30 -exec rm {} \;
     ```
   * **Explication:** La commande `find` cherche tous les fichiers nommés "log_*.txt" modifiés il y a plus de 30 jours et les supprime.

1. Vous avez des fichiers de données avec des extensions différentes (.csv, .json, .xml). Vous souhaitez renommer tous les fichiers .csv en .txt. Utilisez une boucle `for` et l'outil `mv` pour effectuer cette opération.
   * **Réponse:**
     ```bash
     for file in *.csv; do
         mv "$file" "${file%.csv}.txt"
     done
     ```

1. Vous avez plusieurs fichiers de rapport avec des numéros de version (par exemple, rapport_v1.pdf, rapport_v2.pdf). Vous voulez renommer tous ces fichiers en supprimant la partie "v" et le numéro de version. Utilisez une boucle `for` et une expression régulière pour cela.
   * **Réponse:**
     ```bash
     for file in rapport_v*.pdf; do
         mv "$file" "${file%_v*}.pdf"
     done
     ```

1. Vous avez des fichiers de sauvegarde avec des dates au format JJ-MM-AAAA. Vous souhaitez déplacer tous les fichiers de sauvegarde d'un mois spécifique (par exemple, avril 2023) dans un répertoire dédié. Utilisez `find`, `grep`, et une boucle `for` pour réaliser cette tâche.
   * **Réponse:**
     ```bash
     mkdir sauvegarde_avril_2023
     find . -name "*202304*" -exec mv {} sauvegarde_avril_2023 \;
     ```

1. Vous êtes chargé de gérer un serveur de fichiers contenant un grand nombre de fichiers et de répertoires. 
Vous êtes dans le répertoire `/var/log`. Vous souhaitez supprimer tous les fichiers de log plus anciens que 30 jours. Avant de procéder à la suppression, quelle commande utiliserez-vous pour afficher la liste des fichiers concernés ?
   * **Réponse:** `find /var/log -name "*.log" -mtime +30 -print`


1. Vous avez un répertoire `tmp` qui contient de nombreux fichiers temporaires. Vous souhaitez déplacer tous les fichiers commençant par "tmp_" vers un répertoire `archive`. Avant de déplacer les fichiers, quelle commande utiliserez-vous pour vérifier si le répertoire `archive` existe et le créer si nécessaire ?
   * **Réponse:**
     ```bash
     if [ ! -d archive ]; then
         mkdir archive
     fi
     mv tmp_* archive
     ```

1. Vous avez un répertoire contenant des fichiers avec des extensions variées (.txt, .pdf, .docx). Vous souhaitez déplacer tous les fichiers .docx vers un répertoire spécifique. Avant de déplacer les fichiers, quelle commande utiliserez-vous pour afficher un aperçu des fichiers qui seront déplacés ?
   * **Réponse:** `ls *.docx`

1. Vous devez supprimer récursivement un répertoire et tout son contenu. Cependant, vous souhaitez d'abord vérifier le contenu de ce répertoire avant de procéder à la suppression. Quelle commande utiliserez-vous pour afficher le contenu du répertoire de manière détaillée (permissions, propriétaire, taille, etc.) ?
   * **Réponse:** `ls -la /chemin/vers/le/repertoire`

1. Vous avez un grand nombre de fichiers dans un répertoire et vous souhaitez les trier par date de modification. Avant de supprimer les plus anciens, quelle commande utiliserez-vous pour afficher la liste des fichiers triés par date ?
   * **Réponse:** `ls -lt`


1. Vous êtes un administrateur système et vous devez gérer un serveur avec un système de fichiers complexe.
Vous êtes dans le répertoire `/var/log`. Vous souhaitez lister tous les fichiers de ce répertoire, triés par date de modification, du plus récent au plus ancien. Quelle commande utiliserez-vous ? 
   * **Réponse:** `ls -lt /var/log`

1. Vous êtes dans votre répertoire personnel (`/home/<nomUtilisateur>`). Vous souhaitez identifier tous les fichiers de configuration (souvent avec des extensions comme `.conf`, `.ini`, `.yaml`). Quelle commande utiliseriez-vous avec une expression régulière pour cela ?
   * **Réponse:** `find . -name "*.[c|i|y]onfig"`


1. Vous avez un répertoire contenant de nombreux fichiers et sous-répertoires. Vous souhaitez obtenir un aperçu rapide de la taille totale de ce répertoire et de son contenu. Quelle commande utiliserez-vous ?
   * **Réponse:** `du -sh .`
     * `du`: Calcule la taille de chaque fichier, répertoire et de leurs sous-répertoires.
     * `-s`: Affiche uniquement la taille totale.
     * `-h`: Affiche la taille en format humain lisible (Ko, Mo, Go).
     * `.`: Indique le répertoire courant.

1. Vous avez un répertoire contenant des fichiers avec des dates dans leur nom (par exemple, `backup_20230401.tar.gz`). Vous souhaitez lister tous les fichiers de sauvegarde créés en avril 2023. Quelle commande utiliseriez-vous ?
   * **Réponse:** `find . -name "backup_202304*" -print`


---


1. Vous êtes un administrateur système et vous devez nettoyer régulièrement un serveur pour optimiser ses performances.

Vous avez un répertoire temporaire qui contient de nombreux fichiers sans extension. Vous souhaitez supprimer tous les fichiers qui commencent par "tmp_". Quelle commande utiliserez-vous ?
   * **Réponse:** `rm tmp_*`


1. Vous avez un répertoire contenant des fichiers de log avec des dates dans leur nom (par exemple, `log_20230401.log`). Vous souhaitez supprimer tous les fichiers de log plus anciens que 6 mois. Quelle commande utiliserez vous ? (Note : supposons que `find` supporte l'option `-mtime +180` pour les fichiers modifiés il y a plus de 180 jours)
   * **Réponse:** `find . -name "log_*.log" -mtime +180 -delete`
   * **Explication:** Cette commande est similaire à la question 13, mais elle cible les fichiers de log et utilise un délai de 180 jours.

1. Vous avez un répertoire contenant des fichiers de configuration en double (par exemple, `config.old`, `config.bak`, `config.new`). Vous souhaitez supprimer tous les fichiers de configuration qui ne sont pas le fichier principal (par exemple, `config`). Quelle commande utiliseriez-vous ? (Note : cette commande suppose que le fichier principal est nommé simplement "config")
   * **Réponse:** `find . -name "config*" ! -name "config" -delete`


1. Vous avez un répertoire contenant des fichiers de différents types. Vous souhaitez supprimer tous les fichiers sauf les fichiers texte (avec l'extension `.txt`). Quelle commande utiliseriez vous ?
   * **Réponse:** `find . ! -name "*.txt" -delete`


1. Vous êtes un administrateur système et vous devez nettoyer un serveur pour libérer de l'espace disque.
1. Vous avez un répertoire temporaire nommé "tmp" que vous souhaitez supprimer complètement, y compris tous les fichiers et sous-répertoires qu'il contient. Quelle commande utiliserez vous ?
   * **Réponse:** `rm -rf tmp`


1. Vous avez un répertoire nommé "ancien_config" qui contient d'anciennes configurations. Vous souhaitez supprimer ce répertoire et tout son contenu. Quelle commande utiliserez vous, en prenant soin de demander une confirmation avant la suppression ?
   * **Réponse:** `rm -ri ancien_config`


1. Vous avez un répertoire "logs" qui contient de nombreux fichiers de log. Vous souhaitez supprimer tous les fichiers de log datant de plus d'un an. Quelle commande utiliserez vous ? (Note : supposons que `find` supporte l'option `-mtime +365` pour les fichiers modifiés il y a plus de 365 jours)
   * **Réponse:** `find logs -name "*.log" -mtime +365 -delete`
   * **Explication:** Cette commande recherche tous les fichiers se terminant par ".log" dans le répertoire "logs" et ses sous-répertoires, et qui ont été modifiés il y a plus de 365 jours, puis les supprime.

1. Vous avez un répertoire "téléchargements" qui contient de nombreux fichiers téléchargés. Vous souhaitez déplacer tous les fichiers téléchargés il y a plus d'un mois vers un répertoire d'archive. Quelle commande utiliserez vous ?
   * **Réponse:**
     ```bash
     mkdir archives
     find téléchargements -mtime +30 -exec mv {} archives \;
     ```

---


Vous êtes un administrateur système et vous devez analyser le contenu de différents fichiers pour résoudre des problèmes ou effectuer des audits.

1. Vous avez un fichier de log volumineux nommé `access.log`. Vous souhaitez compter le nombre d'occurrences du mot "erreur" dans ce fichier. Quelle commande utiliserez vous ? 
   * **Réponse:** `grep -c "erreur" access.log`
   * **Explication:**
     * `grep`: Recherche du texte dans des fichiers.
     * `-c`: Affiche uniquement le nombre de lignes contenant la chaîne recherchée.




3. **Question 17:** Vous avez un fichier texte nommé `liste_clients.txt`. Vous souhaitez afficher les 10 premières lignes de ce fichier. Quelle commande utiliserez-vous ?
   * **Réponse:** `head -n 10 liste_clients.txt`
   * **Explication:**
     * `head`: Affiche les premières lignes d'un fichier.
     * `-n 10`: Affiche les 10 premières lignes.

4. **Question 18:** Vous avez un fichier de log très volumineux et vous souhaitez afficher les 10 dernières lignes. Quelle commande utiliserez-vous ?
   * **Réponse:** `tail -n 10 access.log`
   * **Explication:**
     * `tail`: Affiche les dernières lignes d'un fichier.
     * `-n 10`: Affiche les 10 dernières lignes.

5. **Question 19:** Vous avez un fichier texte contenant une liste d'adresses IP. Vous souhaitez afficher uniquement les lignes contenant des adresses IP commençant par "192.168". Quelle commande utiliserez-vous ?
   * **Réponse:** `grep "^192.168" liste_adresses.txt`
   * **Explication:**
     * `^192.168`: Recherche les lignes commençant par "192.168".
---

**Contexte:** Vous êtes un administrateur système et vous devez organiser les fichiers sur un serveur en fonction de leur nature et de leur importance.

1. **Question 16:** Vous êtes dans le répertoire `/home/nomUtilisateur/Personnel`. Vous avez un fichier important nommé `rapport_annuel.pdf` que vous souhaitez déplacer dans un nouveau répertoire nommé `Archives` qui sera créé dans votre répertoire personnel. Quelle commande utiliserez-vous ?
   * **Réponse:**
     ```bash
     mkdir ~/Archives
     mv rapport_annuel.pdf ~/Archives
     ```
   * **Explication:** La première commande crée le répertoire `Archives` dans votre répertoire personnel. La deuxième commande déplace le fichier `rapport_annuel.pdf` vers ce nouveau répertoire.

2. **Question 17:** Vous avez plusieurs fichiers de configuration (`.conf`) dans votre répertoire actuel. Vous souhaitez créer un sous-répertoire nommé `config` et y déplacer tous ces fichiers. Quelle commande utiliserez vous ?
   * **Réponse:**
     ```bash
     mkdir config
     mv *.conf config/
     ```
   * **Explication:** La première commande crée le répertoire `config`. La deuxième commande déplace tous les fichiers se terminant par `.conf` vers ce nouveau répertoire.

3. **Question 18:** Vous avez un répertoire nommé `documents` contenant des sous-répertoires pour chaque année (par exemple, `documents/2022`, `documents/2023`). Vous souhaitez déplacer tous les fichiers de l'année 2022 vers un nouveau répertoire nommé `archives_2022`. Quelle commande utiliserez vous ?
   * **Réponse:**
     ```bash
     mkdir archives_2022
     mv documents/2022/* archives_2022/
     ```
   * **Explication:** La première commande crée le répertoire `archives_2022`. La deuxième commande déplace tous les fichiers du répertoire `documents/2022` vers le nouveau répertoire.

4. **Question 19:** Vous avez un répertoire nommé `projets` contenant plusieurs sous-projets. Vous souhaitez créer un fichier `README.md` dans chaque sous-projet. Quelle commande utiliserez vous ?
   * **Réponse:**
     ```bash
     for projet in */; do
         touch "$projet"/README.md
     done
     ```
   * **Explication:** La boucle `for` itère sur tous les sous-répertoires de `projets` et crée un fichier `README.md` dans chacun d'eux.

5. **Question 20:** Vous avez un répertoire nommé `images` contenant des images avec différentes extensions (`.jpg`, `.png`, `.gif`). Vous souhaitez créer trois sous-répertoires : `images_jpg`, `images_png` et `images_gif`, puis déplacer les images correspondantes dans les répertoires appropriés. Quelle commande utiliserez vous ?
   * **Réponse:**
     ```bash
     mkdir images_jpg images_png images_gif
     mv *.jpg images_jpg
     mv *.png images_png
     mv *.gif images_gif
     ```


1. Vous êtes toujours dans le répertoire `Projets` et vous souhaitez trier les fichiers par date de modification, du plus récent au plus ancien. **Question:** Quelle commande utiliserez vous ? 
    * **Réponse:** 
        1. `ls -lt`




