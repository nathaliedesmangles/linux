+++
title = "Système de fichiers, Shell et commandes de base"
weight = 21
+++

![Arborescence](filesystem.png?width=100vw)

La structure du système de fichiers Linux est hiérarchique et organisée sous la forme d'un arbre inversé, où la racine (root) est représentée par `/`. 
Tous les fichiers et répertoires sont situés sous cette racine. 

La structure du système de fichiers Linux est conçue pour être logique et organisée, facilitant ainsi la gestion et la navigation. 

Comprendre cette structure est essentiel pour naviguer et gérer efficacement un système Linux.

## Tout est fichier

Sous Linux, TOUT les éléments visibles dans l’arborescence du système de fichiers sont des fichiers.

- Un fichier est un fichier
- Un répertoire est un fichier
- Une clé USB est un fichier
- Une partition est un fichier
- Un disque dur est un fichier
- etc.

## Répertoires principaux

{{% notice style="warning" title="Important" %}}
Chaque répertoire a un rôle spécifique et contient des types de fichiers bien définis. 
{{% /notice %}}

1. **/** (Racine)
   - Le point de départ de l'arborescence du système de fichiers. Tous les autres répertoires et fichiers sont situés sous ce répertoire.
2. **/bin**
   - Contient les binaires essentiels nécessaires au démarrage du système et à l'exécution des commandes de base, comme `ls`, `cp`, `mv`, etc.
3. **/boot**
   - Contient les fichiers nécessaires au démarrage du système, y compris le noyau Linux et les fichiers de configuration du chargeur de démarrage (bootloader).
4. **/dev**
   - Contient les fichiers de périphériques. Chaque périphérique matériel (comme les disques durs, les clés USB, etc.) est représenté par un fichier dans ce répertoire.
5. **/etc**
   - Contient les fichiers de configuration du système. Par exemple, les fichiers de configuration des services, des utilisateurs, des réseaux, etc.
6. **/home**
   - Contient les répertoires personnels des utilisateurs. Chaque utilisateur a son propre répertoire sous `/home`, par exemple `/home/ndesmangles`.
7. **/lib**
   - Contient les bibliothèques partagées nécessaires pour les binaires situés dans `/bin` et `/sbin`.
8. **/media**
   - Point de montage pour les périphériques amovibles comme les CD-ROM, les clés USB, etc.
9. **/mnt**
   - Utilisé pour monter temporairement des systèmes de fichiers. Par exemple, pour monter un disque dur externe.
10. **/opt**
    - Contient les logiciels optionnels et les paquets additionnels qui ne sont pas inclus dans la distribution standard.
11. **/proc**
    - Système de fichiers virtuel qui contient des informations sur les processus en cours et le système. Par exemple, `/proc/cpuinfo` contient des informations sur le processeur.
12. **/root**
    - Répertoire personnel de l'utilisateur root (administrateur du système).
13. **/run**
    - Contient des informations sur l'état du système depuis le dernier démarrage. Utilisé pour stocker des fichiers temporaires nécessaires au fonctionnement du système.
14. **/sbin**
    - Contient les binaires essentiels pour l'administration du système, comme `fdisk`, `ifconfig`, etc.
15. **/srv**
    - Contient les données spécifiques aux services fournis par le système. Par exemple, les fichiers de données pour un serveur web peuvent être stockés ici.
16. **/tmp**
    - Contient les fichiers temporaires créés par les utilisateurs et les applications. Ce répertoire est souvent vidé au redémarrage du système.
17. **/usr**
    - Contient les applications et les fichiers utilisés par les utilisateurs. Sous-répertoires importants :
      - **/usr/bin** : Contient les binaires des applications utilisateur.
      - **/usr/lib** : Contient les bibliothèques partagées pour les applications utilisateur.
      - **/usr/local** : Contient les logiciels installés localement par l'administrateur du système.
18. **/var**
    - Contient les fichiers variables, tels que les journaux système, les fichiers de spool, et les fichiers temporaires des applications. Par exemple, `/var/log` contient les fichiers journaux.

## Les chemins absolu et relatif

### Chemin absolu

Un chemin absolu est un chemin complet qui commence à la racine du système de fichiers. Il indique l'emplacement exact d'un fichier ou d'un répertoire, peu importe où vous vous trouvez dans le système de fichiers. Par exemple :
```
/home/utilisateur/Documents/fichier.txt
```
Dans cet exemple, le chemin commence par `/`, qui est la racine du système de fichiers, et suit l'arborescence jusqu'au fichier `fichier.txt`.

### Chemin relatif

Un chemin relatif, quant à lui, est un chemin qui est **relatif à votre répertoire de travail actuel**. Il ne commence pas par `/`. Par exemple, si vous êtes dans le répertoire `/home/utilisateur`, et que vous voulez accéder à `fichier.txt` dans le sous-répertoire `Documents`, vous pouvez utiliser :
```
Documents/fichier.txt
```
Ou, si vous voulez remonter d'un niveau dans l'arborescence, vous pouvez utiliser `..` pour représenter le répertoire parent. Par exemple, si vous êtes dans `/home/utilisateur/Documents` et que vous voulez accéder à un fichier dans `/home/utilisateur`, vous pouvez utiliser :
```
../fichier.txt
```

**En résumé**

- **Chemin absolu** : Commence à la racine `/` et donne l'emplacement complet.
- **Chemin relatif** : Dépend de votre répertoire de travail actuel et ne commence pas par `/`.

---

## Qu'est-ce que le SHELL?

Le terme ***Shell*** désigne un programme qui interprète les commandes que vous tapez et les exécute. Il existe plusieurs types de shells, comme le ***Bourne Shell (sh)***, le ***C Shell (csh)***, le ***Korn Shell (ksh)***, et bien d'autres.

### Le shell *Bash*

***Bash*** (*Bourne Again Shell*) est le shell par défaut sur de nombreuses distributions Linux. Il agit comme une interface entre l’utilisateur et le système d’exploitation, permettant d’exécuter des commandes, des scripts, et d’automatiser des tâches.

#### Fonctionnalités clés de Bash

- **Historique des commandes** : Bash conserve un historique des commandes entrées, ce qui permet de les réutiliser facilement.
- **Redirection** : Les flux d’entrée et de sortie peuvent être redirigés pour enregistrer des résultats ou chaîner des commandes.
- **Variables** : Bash prend en charge les variables, qui peuvent stocker des données pour une utilisation ultérieure.
- **Alias** : Vous pouvez créer des alias pour simplifier des commandes longues ou fréquemment utilisées.

### La ligne de commande

La ligne de commande est l'interface où vous tapez vos commandes. Elle est souvent représentée par un symbole `$` ou `#`:
- `$` signifie que vous êtes un utilisateur standard
- `#` signifie que vous êtes le super-utilisateur `root` (administrateur du système).
- `~` signifie le répertoire personnel, les symboles `$` et `#` seront précédés du symbole tilde: `~$` ou `~#`.

Une commande dans le shell suit généralement cette structure :

```
commande [options] [arguments]
```

- **commande** : Le programme ou l'outil que vous souhaitez exécuter.
- **options** : Des paramètres supplémentaires qui modifient le comportement de la commande.
- **arguments** : Les cibles sur lesquelles la commande doit agir (fichiers, répertoires, etc.).

Lorsque vous êtes prêt à exécuter une commande, appuyez sur la touche Entrée. Tapez chaque commande sur une ligne séparée. Le résultat de la commande est affiché avant l’invite du shell suivante.

**Exemple de commande sans option** :
```bash
[ndesmangles@localhost ~]$ whoami
ndesmangles
[ndesmangles@localhost ~]$
```

**Exemple de commande avec une option** :
```bash
[ndesmangles@localhost ~]$ date -R
Fri, 17 Jan 2025 20:19:50 -0500
[ndesmangles@localhost ~]$
```

Pour exécuter une commande avec des privilèges de **super-utilisateur (`root`)**, on la précède de `sudo`:

```bash
[ndesmangles@localhost ~]$ sudo ls /root
```

## Commandes de base en *Bash*

Bash propose une variété de commandes puissantes pour interagir avec le système. Ces commandes de base sont essentielles pour naviguer, gérer des fichiers, et interagir avec votre système sous Bash.

---

## Navigation dans le système de fichiers

| **Commande** | **Description** |
|--------------|-----------------|
| `pwd`        | Affiche le chemin absolu du répertoire courant.    |
| `cd`         | Change le répertoire courant.                      |
| `ls`         | Affiche le contenu d'un répertoire.                |

1. **`pwd` (Print Working Directory)** :
     ```bash
     [ndesmangles@localhost ~]$ pwd
     /home/ndesmangles			# Le répertoire personnel dans home
     [ndesmangles@localhost ~]$ 
     ```

2. **`cd` (Change Directory)** :
     ```bash
     [ndesmangles@localhost ~]$ cd /etc
     [ndesmangles@localhost etc]$	# Notez le changement du répertoire courant (etc)
     ```
   - Remonter d'un niveau.
     ```bash
     [ndesmangles@localhost etc]$ cd ..
     [ndesmangles@localhost /]$ 	# Notez le positionnement à la racine /
     ```
   - Revenir dans le répertoire `etc`
     ```bash
     [ndesmangles@localhost /]$ cd etc
     [ndesmangles@localhost etc]$ 
     ```
   - Remonter de deux niveaux.
     ```bash
     [ndesmangles@localhost etc]$ cd ../..
     [ndesmangles@localhost /]$ 	# Notez le retour à la racine /
     ```
   - Revenir à notre répertoire personnel
     ```bash
     [ndesmangles@localhost etc]$ cd ~
     [ndesmangles@localhost ~]$ 	# Notez le retour au répertoire personnel ~
     ```

3. **`ls` (List)** :
   - Options utiles :
     - `-l` : Affiche des détails comme les permissions[^1], la taille, etc.
     - `-a` : Montre les fichiers cachés.

     ```bash
     [ndesmangles@localhost /]$ ls
     afs  bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
     [ndesmangles@localhost /]$ ls -l
     total 24
     dr-xr-xr-x.   2 root root    6  2 oct 17:00 afs
     lrwxrwxrwx.   1 root root    7  2 oct 17:00 bin -> usr/bin
     dr-xr-xr-x.   5 root root 4096 11 jan 23:06 boot
     ```
**Quelques explications** :

1. **Première colonne**: -rwxr-xr-x par exemple représente le type de fichier et les droits d’accès (abordés en détail dans un prochain cours) qui lui sont associés.
2. **Deuxième colonne** : ce qu’elle représente dépend du type de fichier:
   - **Répertoire** : indique le nombre de sous-répertoires (+2 pour . et ..).
   - **Fichier** : nombre de lien physiques (vu plus loin dans ce cours).
3. **Troisième et quatrième colonnes** représentent l’utilisateur propriétaire du fichier et le groupe propriétaire du fichier.
4. **Cinquième colonne** indique la taille du fichier (notez qu’un répertoire a une taille qui correspond à la taille du fichier répertoire sur le disque).
5. **Sixième colonne** indique la date de dernière modification.
6. **Septième colonne** est le nom du fichier.

---

## Manipulation de fichiers et répertoires

| **Commande** | **Description** |
|--------------|-----------------|
| `touch`      | Crée un fichier vide ou met à jour la date de modification d’un fichier existant.   |
| `mkdir`      | Crée un nouveau répertoire.                                                         |
| `rm`         | Supprime des fichiers. Pour supprimer des répertoires, utilisez `-r` (récursif).    |
| `rmdir`      | Supprime un répertoire vide.                                                        |
| `cp`         | Copie des fichiers ou des répertoires.                                              |
| `mv`         | Déplace ou renomme des fichiers et des répertoires.                                 |


1. **`touch`** :
     ```bash
     [ndesmangles@localhost ~]$ touch nouveau_fichier.txt
     ```

2. **`mkdir` (Make Directory)** :
     ```bash
     [ndesmangles@localhost ~]$ mkdir nouveau_repertoire
     ```

3. **`rm` (Remove)** :
     ```bash
     [ndesmangles@localhost ~]$ rm fichier.txt
     [ndesmangles@localhost ~]$ rm -r dossier_a_supprimer
     ```

4. **`rmdir` (Remove Directory)** :
     ```bash
     [ndesmangles@localhost ~]$ rmdir dossier_vide
     [ndesmangles@localhost ~]$ rmdir dossier_pas_vide   # Affiche une erreur
     ```

5. **`cp` (Copy)** :
     ```bash
     [ndesmangles@localhost ~]$ cp fichier_source.txt fichier_destination.txt
     [ndesmangles@localhost ~]$ cp -r dossier_source dossier_destination
     ```

6. **`mv` (Move)** :
     ```bash
     [ndesmangles@localhost ~]$ mv ancien_nom.txt nouveau_nom.txt
     [ndesmangles@localhost ~]$ mv fichier.txt /nouveau/chemin/
     ```

---

## Affichage et lecture de fichiers

| **Commande** | **Description** |
|--------------|-----------------|
| `cat`        | Affiche le contenu complet d'un fichier.   |
| `less`       | Permet de lire un fichier page par page.   |
| `head`       | Affiche les premières lignes d'un fichier. 10 lignes par défaut. |
| `tail`       | Affiche les dernières lignes d'un fichier. 10 lignes par défaut.  |


1. **`cat`** :
     ```bash
     [ndesmangles@localhost ~]$ cat fichier.txt
     [ndesmangles@localhost ~]$ cat fichier1 fichier2
     Hello World!!
     Introduction aux commandes Linux.
     [ndesmangles@localhost ~]$ cat /etc/shells		# Affiche les Shells installés sur la machine.
     ```

2. **`less`** :
   - Contrôles :
     - `Espace` : Page suivante
     - `q` : Quitter
     ```bash
     [ndesmangles@localhost ~]$ less fichier.txt
     ```

3. **`head`** :
     ```bash
     [ndesmangles@localhost ~]$ head fichier.txt       # Affiche les 10 premières lignes
     [ndesmangles@localhost ~]$ head -n 5 fichier.txt  # Affiche les 5 premières lignes
     ```

4. **`tail`** :
     ```bash
     [ndesmangles@localhost ~]$ tail fichier.txt       # Affiche les 10 dernières lignes
     [ndesmangles@localhost ~]$ tail -n 5 fichier.txt  # Affiche les 5 dernières lignes
     ```
---

## Informations système et historique

| **Commande** | **Description** |
|--------------|-----------------|
| `date`       | Affiche la date et l'heure actuelles.        |
| `history`    | Liste les commandes précédemment exécutées.  |


1. **`date`** :
   - Options utiles :
     - `+` : Pour spécifier un format personnalisé.
   - Formats: 
     - `%Y` : Année complète (ex. 2025).
     - `%m` : Mois (01-12).
     - `%d` : Jour (01-31).
     - `%H` : Heure (00-23).
     - `%M` : Minutes (00-59).
     - `%S` : Secondes (00-59).
     ```bash
     [ndesmangles@localhost ~]$ date
     Thu Jan  9 20:42:36 EST 2025
     [ndesmangles@localhost ~]$ date "+%Y-%m-%d %H:%M:%S"
     2025-01-09 20:42:43
     ```

2. **`history`** :
   - Options utiles :
     - `n` : Pour spécifier le nombre de commandes précédentes à afficher.
     - `!` : Pour exécuter une commande spécifique de l'historique, par son numéro.
     - `c` : Pour effacer l'historique de la session.
     ```bash
     [ndesmangles@localhost ~]$ history		# Affiche l'historique complet de la session.
     1  date -R
     2  pwd
     3  cd /etc
     4  cd ..
     5  cd etc
     6  cd ../..
     7  ls
     8  ls -a
     9  ls -l
     10  date
     11  date "+%Y-%m-%d %H:%M:%S"
     12  cd ~
     13  history
     [ndesmangles@localhost ~]$ history 5	# Affiche les 5 dernières commandes effectuées.
     10  date
     11  date "+%Y-%m-%d %H:%M:%S"
     12  cd ~
     13  history
     14  history 5
     [ndesmangles@localhost ~]$ !11		# Exécute la commande #11 dans l'historique
     date "+%Y-%m-%d %H:%M:%S"
     2025-01-09 20:47:03
     [ndesmangles@localhost ~]$ !da		# Exécute la commande la plus récente, dont le nom commence par 'da'.  
     date "+%Y-%m-%d %H:%M:%S"			  
     2025-01-18 20:48:22	 
     [ndesmangles@localhost ~]$ history -c	# Efface l'historique.
     [ndesmangles@localhost ~]$ history
     1  history
     ```

{{% notice style="tip" title="Bon à savoir" %}}
La commande `clear` permet d'effacer l'écran du terminal.
{{% /notice %}}

---

## Commandes utiles

| **Commande** | **Description** |
|--------------|-----------------|
| `echo`       | Affiche un message ou une variable dans le terminal. |
| `man`        | Affiche le manuel d’aide pour une commande.          |


1. **`echo`** :
     ```bash
     [ndesmangles@localhost ~]$ echo "Bonjour, monde!"
     Bonjour, monde!     
     [ndesmangles@localhost ~]$ echo $SHELL
     /bin/bash
     ```

    {{% notice style="note" title="Note" %}}
    **$SHELL** doit être écrit en respectant la casse.
    {{% /notice %}}


2. **`man` (Manual)** :
     ```bash
     [ndesmangles@localhost ~]$ man ls		# Affiche le manuel de la commande `ls`.
     ```

### Structure d'une page de manuel

Une page de manuel typique contient plusieurs sections, telles que :

- **NAME** : Le nom de la commande et une brève description.
- **SYNOPSIS** : La syntaxe de la commande.
- **DESCRIPTION** : Une description détaillée de la commande et de ses options.
- **OPTIONS** : Les options disponibles pour la commande.
- **EXAMPLES** : Des exemples d'utilisation.
- **SEE ALSO** : Des références à d'autres commandes ou documents pertinents.

### Options utiles

- `man -k keyword` : Recherche des pages de manuel contenant le mot-clé spécifié.
- `man -f command` : Affiche une brève description de la commande (équivalent à `whatis command`).

## Autocompletion d'une commande *Bash* 

- La touche `Tab` du clavier, permet de compléter rapidement les commandes et les noms de fichiers après avoir entré un nombre de caractères suffisant pour réduire les possibilités à une seule. 
- Si les caractères saisis ne sont pas uniques, appuyez deux fois sur la touche de tabulation pour afficher toutes les commandes correspondantes.

```bash
[ndesmangles@localhost ~]$ cat /etc/serTab	# `cat /etc/ser` suivi de la touche `Tab` complète le nom du fichier.
[ndesmangles@localhost ~]$ cat /etc/services
[ndesmangles@localhost ~]$ passTabTab		# `pass` suivi de 2 fois la touche `Tab` propose les commande dont le nom commence par `pass`.
passt       passt.avx2  passwd      
[ndesmangles@localhost ~]$ pass
```


[^1]: Nous étudierons comment gérer les droits des différents utilisateurs plus tard dans ce cours.
