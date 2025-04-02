+++
title = "Système de fichiers, Shell et commandes de base et VIM"
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
[ndesmangles@localhost ~]$ date +%R
20:19 
```

{{% notice style="orange" title="Vous avez perdu la ligne de commande ?"  %}}
Si vous appuyer 'Entrée' avant d'avoir terminé d'écrire une commande, vous perdrez la ligne de commande. Le symbole `>` s'affichera à la place.
Pour retrouver la ligne de commande, faites `Ctrl+C`.
```bash
[ndesmangles@localhost ~]$ commande_incomplète
> ^C
[ndesmangles@localhost ~]$ 
```
{{% /notice %}}


Pour exécuter une commande avec des privilèges de **super-utilisateur (`root`)**, on la précède de `sudo`:

```bash
[ndesmangles@localhost ~]$ sudo ls /root
```

#### Comment afficher la liste des shells disponibles le système ?

L'information se trouve dans le fichier `/etc/shells`.

```bash
$ cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
```

## Commandes de base en *Bash*

Bash propose une variété de commandes puissantes pour interagir avec le système. Ces commandes de base sont essentielles pour naviguer, gérer des fichiers, et interagir avec votre système sous Bash.

---

## Navigation dans le système de fichiers

**Les commandes** :
1. **`pwd` (Print Working Directory)**
2. **`cd` (Change Directory)**
3. **`ls` (List)**
  

| Commande    | Description                                              | Exemple |
|-------------|----------------------------------------------------------|---------|
| `pwd`       | Affiche le chemin absolu du répertoire courant.          | /home/user  <br> `$ pwd`  <br> /home/user |
| `cd`        | Change le répertoire courant pour Documents.             | /home/user  <br> `$ cd Documents`  <br> /home/user/Documents |
| `cd ~`      | Change vers le répertoire personnel de l'utilisateur.    | /home/user/Documents  <br> `$ cd ~`  <br> /home/user |
| `cd ..`     | Remonte d'un niveau dans l'arborescence des répertoires. | /home/user/Documents  <br> `$ cd ..`  <br> /home/user |
| `cd ../../` | Remonte de deux niveaux dans l'arborescence.             | /home/user/Documents/Projects  <br> `$ cd ../../`  <br> /home/user |
| `ls`        | Affiche le contenu d'un répertoire.                      | /home/user/Documents  <br> `$ ls`  <br> fichier.txt dossier |
| `ls -l`     | Affiche la liste des fichiers dans un répertoire. <br> L'option `-l` affiche les détails des fichiers dans un répertoire.     | /home/user/Documents  <br> `$ ls -l`  <br> `-rw-r--r-- 1 user user 1234 Jan 1 12:00 fichier.txt` |


### Quelques explications du résultat de **ls -l**

1. **Premier caractère**: `-`, `d` ou `l` représente le type de fichier (fichier standard, répertoire ou lien symbolique respectivement)
2. **Neuf caractères suivants**: par exemple `rwxr-xr-x` représentent les droits d’accès au fichier/répertoire (abordés en détail dans un prochain cours).

{{% notice style="tip" title="Bon à savoir" %}}
La commande `clear` permet d'effacer l'écran du terminal.
{{% /notice %}}

---

## Manipulation de fichiers et répertoires

**Les commandes** :
1. **`touch`** 
2. **`mkdir` (Make Directory)**
3. **`rm` (Remove)** :
4. **`rmdir` (Remove Directory)**
5. **`cp` (Copy)**
6. **`mv` (Move)**


| Commande  | Description                                                                             | Exemple |
|-----------|-----------------------------------------------------------------------------------------|---------|
| `touch`   | Crée un fichier vide ou met à jour la date de modification d’un fichier existant.      |  /home/user <br> `$ touch fichier.txt` <br> `$ ls` <br> fichier.txt |
| `mkdir`   | Crée un nouveau répertoire.                                                            |  /home/user <br> `$ mkdir mon_dossier` <br> `$ ls` <br> mon_dossier |
| `rm`      | Supprime des fichiers. Utilisez `-r` pour supprimer des répertoires et leur contenu.   |  /home/user <br> `$ rm fichier.txt` <br> `$ rm -r mon_dossier` |
| `rmdir`   | Supprime un répertoire vide (ne fonctionne pas s'il contient des fichiers).            |  `$ rmdir mon_dossier`|
| `cp`      | Copie des fichiers ou des répertoires (avec `-r` pour copier des dossiers entiers).    |  `$ cp fichier.txt copie.txt` <br> `$ ls` <br> fichier.txt copie.txt <br> `$ cp -r mon_dossier copie_dossier` <br>  `$ ls` <br> mon_dossier copie_dossier |
| `mv`      | Déplace ou renomme des fichiers et des répertoires.                                    |  `$ mv fichier.txt nouveau_nom.txt`  <br> `$ ls` <br>  nouveau_nom.txt |


---

## Affichage et lecture de fichiers  

**Les commandes** :
1. **`cat`**
2. **`less`**
3. **`head`**
4. **`tail`** 


|  Commande    | Description     | Exemple                  |  
|--------------|-----------------|--------------------------|  
| `cat`        | Affiche le contenu complet d'un ou de plusieurs fichiers.   | `$ cat fichier.txt` <br> `$ cat fichier1.txt fichier2.txt`|  
| `less`       | Permet de lire un fichier page par page.   <br> Contrôles : <br> `Espace` : Page suivante <br> `q` : Quitter| `$ less fichier.txt` |  
| `head`       | Affiche les premières lignes d'un fichier. **10 lignes par défaut**. <br> L'option `-n` permet de spécifier le nombre de lignes | `$ head fichier.txt` <br> `$ head -n 5 fichier.txt` |  
| `tail`       | Affiche les dernières lignes d'un fichier. **10 lignes par défaut**. <br> L'option `-n` permet de spécifier le nombre de lignes | `$ tail fichier.txt` <br> `$ tail -n 5 fichier.txt` |  

---

## Informations système et historique

|  Commande  | Description           | Exemple              |
|------------|-----------------------|----------------------|
| `date`     | Affiche la date et l'heure actuelles.        | `$ date` <br> Thu Jan  9 20:42:36 EST 2025 <br> `$ date "+%Y-%m-%d %H:%M:%S"` <br> 2025-01-09 20:42:43 |
| `history`  | Liste les commandes précédemment exécutées.  <br> Options utiles : <br> `n` : Pour spécifier le nombre de commandes précédentes à afficher. <br> `!` : Pour exécuter une commande spécifique de l'historique, par son numéro. <br> `c` : Pour effacer l'historique de la session.| `$ history` <br> `$ history 5` <br> `$ history -c` |


1. **Commande date quelques options utiles** :
     - `+` : Il faut précéder l'option du symbole `+` pour spécifier un format personnalisé.
   - Formats: 
     - `%Y` : Année complète (ex. 2025).
     - `%m` : Mois (01-12).
     - `%d` : Jour (01-31).
     - `%H` : Heure (00-23).
     - `%M` : Minutes (00-59).
     - `%S` : Secondes (00-59).
     - `%r` : Heure au format 12h (ex. 11:11:04 PM) 
     - `%R` : Heure au format 24h (ex. 23:11 sans les secondes) 
     - `%p` : Heure avec AM ou PM 


2. **Exemples avec la commande history** :
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

---

## Commandes utiles

1. **`echo`** 
2. **`man` (Manual)**


|  Commande  | Description     | Exemple  |
|------------|-----------------|-----------|
| `echo`     | Affiche un message ou une variable dans le terminal. <br> $SHELL doit être écrit en respectant la casse. | `$ echo "Bonjour, monde!"` <br> Bonjour, monde! <br> `$ echo $SHELL` <br> /bin/bash    
| `man`      | Affiche le manuel d’aide pour une commande.          | `$ man ls`


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

## Introduction à l'éditeur de texte VIM

**VIM** (Vi IMproved) est un éditeur de texte, souvent utilisé dans les environnements Unix/Linux. Bien qu’il puisse sembler intimidant au premier abord, il devient très efficace une fois maîtrisé.  

#### Pourquoi utiliser **vim** ?

- **Disponibilité** : Installé par défaut sur presque tous les systèmes Unix/Linux.  
- **Léger et rapide** : Idéal pour éditer des fichiers même sur des systèmes limités en ressources.   
- **Puissant** : Supporte des fonctionnalités avancées comme la recherche, la substitution, et l'édition de plusieurs fichiers simultanément.  

---

### Premiers pas avec **vim**

Pour ouvrir un fichier avec **vim**, utilisez la commande suivante :  
```bash
$ vim nom_du_fichier
```
Si le fichier n'existe pas, **vim** le créera.

Lorsque vous ouvrez **vim**, il commence en **mode commande**. Vous ne pouvez pas directement écrire du texte. Vous devez d'abord passer au **mode insertion** en tapant la lettre `i`. En bas de la fenêtre Vim, le mot **INSERTION** s'affichera. 

![Mode insertion](./mode_insertion.png?width=100vw)

{{% notice style="tip" title="Revenir au mode Normal" %}}
Si avant de taper `i` ou n'importe quel autre mode, vous n'êtes plus dans le mode **Normal**, il suffit de tapper la touche `ESC` pour revenir au mode **Normal**.
{{% /notice %}}

---

### Modes principaux de **vim**

Ces modes sont les bases du fonctionnement de **vim**. Vous pouvez basculer entre eux selon vos besoins pour éditer et manipuler vos fichiers.


| Mode | Description | Action | Commande |
|------|------|------|:--------:|
| **Normal** | Mode par défaut lorsque vous ouvrez **vim**. | Appuyez sur `Esc` pour revenir à ce mode. | `ESC` |
| **Insertion** | Permet d'insérer ou de modifier du texte. | Passer en mode insertion où se trouve le curseur. | `i` |
| **Commande** | Permet de sauvegarder un fichier. | Sauvegarde| `:w` |
|              | Permet de quitter Vim, si aucun changement n'a été effectué dans le fichier en cours. | Quitter | `:q` |
|              | Permet de forcer la fermeture de vim sans sauvegarder les modifications. | Quitter sans sauvegarder les modifications. | `:q!`  | 
|              | Permet de sauvegarder et fermer le fichier. | Sauvegarde et quitter.| `:wq` |

---

### Exercices pratiques

1. **Ouvrez un fichier** nommé `test.txt` avec la commande :  
   ```bash
   $ vim test.txt
   ```  
   Passez en mode insertion (`i`), écrivez quelques lignes, puis sauvegardez et quittez avec `:wq`.

2. **Recherchez du texte** : Ouvrez un fichier existant, cherchez un mot avec `/mot`, puis naviguez entre les occurrences avec `n`.

3. **Testez l'annulation** : Modifiez une ligne, annulez avec `u`, puis rétablissez avec `Ctrl+r`.


[^1]: Nous étudierons comment gérer les droits des différents utilisateurs plus tard dans ce cours.
