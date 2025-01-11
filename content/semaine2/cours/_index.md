+++
title = "Introduction au shell et la ligne de commande"
weight = 21
+++

## Qu'est-ce que le SHELL?

Le terme "Shell" désigne un programme qui interprète les commandes que vous tapez et les exécute. Il existe plusieurs types de shells, comme le ***Bourne Shell (sh)***, le ***C Shell (csh)***, le ***Korn Shell (ksh)***, et bien d'autres.

## La ligne de commande

Une commande dans le shell suit généralement cette structure :
```
commande [options] [arguments]
```
- **commande** : Le programme ou l'outil que vous souhaitez exécuter.
- **options** : Des paramètres supplémentaires qui modifient le comportement de la commande.
- **arguments** : Les cibles sur lesquelles la commande doit agir (fichiers, répertoires, etc.).


- La ligne de commande est l'interface où vous tapez vos commandes. Elle est souvent représentée par un symbole `$` ou `#` pour les utilisateurs root (administrateur).
	- `$` signifie que vous êtes un utilisateur standard
	- `#` signifie que vous êtes le super-utilisateur `root` (administrateur du système).
	- `~` signifie le répertoire personnel, les symboles `$` et `#` seront précédés du symbole tilde: `~$` ou `~#`.
- Lorsque vous êtes prêt à exécuter une commande, appuyez sur la touche Entrée. Tapez chaque commande sur une ligne séparée. Le résultat de la commande est affiché avant l’invite du shell suivante.

**Exemple**:
```plaintext
nathalie@Yoda:~$ whoami
nathalie
nathalie@Yoda:~$ 
```

Pour exécuter une commande avec des privilèges de super-utilisateur (`root`) la précède de `sudo`:

```bash
nathalie@Yoda:~$ sudo ls /root
```

## Commandes simples

Ces commandes simples sont essentielles pour naviguer et gérer efficacement un système Linux à l'aide du shell Bash. La maîtrise de ces commandes vous permettra d'effectuer des tâches courantes de manière plus efficace et de mieux comprendre le fonctionnement de votre système.


| **Commande** | **Description** | **Options** |
|--------------|-----------------|-------------|
| `date`       | Affiche la date et l'heure du système. | `+FORMAT` pour formater la sortie. |
| `passwd`     | Change le mot de passe utilisateur. | `-l` pour verrouiller un compte. |
| `file`       | Détermine le type de fichier.   Un fichier ASCII sera lisible/compréhensible | `-i` pour afficher le type MIME. |
| `cat`        | Affiche le contenu d'un fichier. | `-n` pour numéroter les lignes. |
| `less`       | Affiche le contenu d'un fichier page par page. | `-N` pour numéroter les lignes. |
| `head`       | Affiche par défaut, les **10** premières lignes d'un fichier. | `-n` pour spécifier le nombre de lignes. |
| `tail`       | Affiche par défaut, les **10** dernières lignes d'un fichier. | `-n` pour spécifier le nombre de lignes. |
| `wc`         | Compte les lignes, mots et donne la taille du fichier en octets. | `-l` pour les lignes, `-w` pour les mots et `-c` pour la taille. |
| `ls`         | Liste les fichiers et répertoires. | `-l` pour un format détaillé. |
| `history`    | Affiche l'historique des commandes. | `-c` pour effacer l'historique. Le point d’exclamation (!) rappelle les commandes précédentes sans avoir à les retaper. La commande **`!nombre`** rappelle la commande correspondant au nombre spécifié. La commande **`!string`** rappelle la commande la plus récente qui commence par la chaîne spécifiée.|


### Exemples

#### 1. Commande `date` pour la date et l'heure courantes

| Option | Description |
|--------|-------------|
| `%a`   | Nom abrégé du jour de la semaine (par exemple, Mon) |
| `%A`   | Nom complet du jour de la semaine (par exemple, Monday) |
| `%b`   | Nom abrégé du mois (par exemple, Jan) |
| `%B`   | Nom complet du mois (par exemple, January) |
| `%c`   | Date et heure locale (par exemple, Thu Mar 3 23:05:25 2005) |
| `%d`   | Jour du mois (01 à 31) |
| `%H`   | Heure (00 à 23) |
| `%I`   | Heure (01 à 12) |
| `%j`   | Jour de l'année (001 à 366) |
| `%m`   | Mois (01 à 12) |
| `%M`   | Minutes (00 à 59) |
| `%p`   | AM ou PM |
| `%S`   | Secondes (00 à 60) |
| `%U`   | Numéro de la semaine de l'année, avec le dimanche comme premier jour de la semaine (00 à 53) |
| `%w`   | Jour de la semaine (0 à 6, avec dimanche = 0) |
| `%y`   | Année sans le siècle (00 à 99) |
| `%Y`   | Année avec le siècle (par exemple, 2025) |
| `%Z`   | Fuseau horaire (par exemple, EST) |

**Quelques exemples:**

```bash
nathalie@Yoda:~$ date
Thu Jan  9 20:42:36 EST 2025

nathalie@Yoda:~$ date "+%Y-%m-%d %H:%M:%S"
2025-01-09 20:42:46

nathalie@Yoda:~$ date +%r
08:44:38 PM

nathalie@Yoda:~$ date +%R
20:44

nathalie@Yoda:~$ date +%x
01/09/25

nathalie@Yoda:~$ date +%X
20:44:00

nathalie@Yoda:~$ date +%h
Jan
```

#### 2. commande `passwd` pour changer le mot de passe de l'utilisateur

```bash
nathalie@Yoda ~$ passwd
Changing password for user nathalie.
Current password: ancien_mot_de_passe
New password: nouveau_mot_de_passe
Retype new password: nouveau_mot_de_passe
passwd: all authentication tokens updated successfully.
```

#### 3. Commande `file` pour obtenir le type d'un fichier
 
```bash
nathalie@Yoda:~$ file /etc/services
/etc/services: ASCII text

nathalie@Yoda:~$ file /home
/home: directory
```

#### 4. Commande `cat` pour afficher le contenu d'un fichier

**Un fichier à la fois**:
```bash
nathalie@Yoda:~$ cat /etc/services
# Network services, Internet style
#
# Updated from https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml .
#
# New ports will be added on request if they have been officially assigned
# by IANA and used in the real-world or are needed by a debian package.
# If you need a huge list of used numbers please install the nmap package.

tcpmux          1/tcp                           # TCP port service multiplexer
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
systat          11/tcp          users
daytime         13/tcp
daytime         13/udp
netstat         15/tcp

```

**Deux fichiers à la fois**:
```bash
nathalie@Yoda:~$ cat fichier1 fichier2
Hello World!!
Introduction aux commandes Linux.
```

**Déterminer les shells installés et utilisé**

Vous pouvez voir la liste des Shells présents dans votre distribution avec la commande `cat` et celui utilisé avec la commande `echo`:
```bash
nathalie@Yoda:~$ cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/usr/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/dash
/usr/bin/tmux
```
Vous pouvez voir le shell que vous utilisez (**$SHELL** doit être écrit en respectant la casse):
```bash
nathalie@Yoda:~$ echo $SHELL
/bin/bash
```
- Le shell qui vous est attribué est défini dans le fichier `/etc/passwd`..
- Pour visualiser ce fichier SANS risquer de la modifier, utilisez la commande `cat`.
```bash
nathalie@Yoda:~$ cat /etc/passwd
landscape:x:104:105::/var/lib/landscape:/usr/sbin/nologin
polkitd:x:990:990:User for polkitd:/:/usr/sbin/nologin
nathalie:x:1000:1000:,,,:/home/nathalie:/bin/bash
nathalie@Yoda:~$
```

- Trouvez la ligne commençant par votre nom d'utilisateur. La dernière partie correspond à votre shell par défaut. Dans mon cas `/bin/bash`.
- Bash est le shell le plus utilisé. Nous en reparlerons plus tard.

#### 5. Commande `less` pour afficher le contenu d'un fichier page par page

```bash
nathalie@Yoda:~$ less /etc/services
# Network services, Internet style
#
# Updated from https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml .
#
# New ports will be added on request if they have been officially assigned
# by IANA and used in the real-world or are needed by a debian package.
# If you need a huge list of used numbers please install the nmap package.

tcpmux          1/tcp                           # TCP port service multiplexer
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
systat          11/tcp          users
daytime         13/tcp
daytime         13/udp
netstat         15/tcp
qotd            17/tcp          quote
chargen         19/tcp          ttytst source
chargen         19/udp          ttytst source
ftp-data        20/tcp
ftp             21/tcp
fsp             21/udp          fspd
ssh             22/tcp                          # SSH Remote Login Protocol
telnet          23/tcp
smtp            25/tcp          mail
time            37/tcp          timserver
time            37/udp          timserver
whois           43/tcp          nicname
tacacs          49/tcp                          # Login Host Protocol (TACACS)
tacacs          49/udp
domain          53/tcp                          # Domain Name Server
domain          53/udp
bootps          67/udp
bootpc          68/udp
tftp            69/udp
/etc/services
```

>[!TIP]
**NB**: Pour revenir à la ligne de commande, taper la lettre `q`.


#### 6. Commande `head` pour afficher les premières lignes d'un fichier

```bash
nathalie@Yoda:~$ head /etc/services
# Network services, Internet style
#
# Updated from https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml .
#
# New ports will be added on request if they have been officially assigned
# by IANA and used in the real-world or are needed by a debian package.
# If you need a huge list of used numbers please install the nmap package.

tcpmux          1/tcp                           # TCP port service multiplexer
echo            7/tcp

nathalie@Yoda:~$ head -n 5 /etc/services
Network services, Internet style
#
# Updated from https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml .
#
# New ports will be added on request if they have been officially assigned

```

#### 7. Commande `tail` pour afficher les dernières lignes d'un fichier

```bash
nathalie@Yoda:~$ tail /etc/services
sgi-cad         17004/tcp                       # Cluster Admin daemon
binkp           24554/tcp                       # binkp fidonet protocol
asp             27374/tcp                       # Address Search Protocol
asp             27374/udp
csync2          30865/tcp                       # cluster synchronization tool
dircproxy       57000/tcp                       # Detachable IRC Proxy
tfido           60177/tcp                       # fidonet EMSI over telnet
fido            60179/tcp                       # fidonet EMSI over TCP

# Local services

nathalie@Yoda:~$ tail -n 5 /etc/services
dircproxy       57000/tcp                       # Detachable IRC Proxy
tfido           60177/tcp                       # fidonet EMSI over telnet
fido            60179/tcp                       # fidonet EMSI over TCP

# Local services
```

#### 8. Commande `wc` pour obtenir le nombre de **lignes**, de **mots** et la **taille** en octets dans un fichier

```bash
nathalie@Yoda:~$ wc /etc/services
361  1773 12813 /etc/services

nathalie@Yoda:~$ wc -l /etc/services
361 /etc/services

nathalie@Yoda:~$ wc -w /etc/services
1773 /etc/services

nathalie@Yoda:~$ wc -c /etc/services
12813 /etc/services

```
#### 9. Commande `ls` pour lister les détails d'un fichier

En premier, allons dans le répertoire `/etc` à l'aide de la commande `cd`[^1]
```bash
nathalie@Yoda:~$ cd /etc
```
Utilisons la commande `ls`
```bash
nathalie@Yoda:/etc$ ls
PackageKit              cron.weekly     groff          locale.conf          nsswitch.conf  rmt                supercat
X11                     cron.yearly     group          locale.gen           opt            rpc                sysctl.conf
adduser.conf            crontab         group-         localtime            os-release     rsyslog.conf       sysctl.d
```
Pour afficher la liste de tous les attributs d’un fichier on utilise l'option `-l` :
```bash
nathalie@Yoda:/etc$ ls -l
total 340
drwxr-xr-x 1 root root       4096 Apr 23  2024 PackageKit
drwxr-xr-x 1 root root       4096 Apr 23  2024 X11
-rw-r--r-- 1 root root       3444 Jul  5  2023 adduser.conf
drwxr-xr-x 1 root root       4096 Apr 23  2024 alternatives
drwxr-xr-x 1 root root       4096 Apr 23  2024 apparmor
```

**Quelques explications**:

- La **première colonne**: `-rwxr-xr-x` par exemple représente le type de fichier et les droits d’accès (abordés en détail dans un prochain cours) qui lui sont associés.
	- Les 3 premiers sont les plus fréquents, les suivants sont des fichiers spéciaux qui seront principalement manipulés par l'utilisateur `root`.
- La **deuxième colonne** : ce qu’elle représente dépend du type de fichier:
	- **Répertoire**: indique le nombre de sous-répertoires (+2 pour . et ..).
	- **Fichier**: nombre de lien physiques (vu plus loin dans ce cours).
- Les **troisième et quatrième colonnes** représentent l’utilisateur propriétaire du fichier et le groupe propriétaire du fichier.
- La **cinquième colonne** indique la taille du fichier (notez qu’un répertoire a une taille qui correspond à la taille du fichier répertoire sur le disque).
- La **sixième colonne** indique la date de dernière modification.
- La **septième colonne** est le nom du fichier.

#### 10. Commande `history` pour afficher les commandes effectuées précédemment

Pour revenir au dossier personnel
```bash
nathalie@Yoda:/etc$ cd ~
```

```bash
nathalie@Yoda:~$ history
 exit
    2  date
    3  date +Y%
    4  date -%m
    5  date help
    6  man date
    7  date -d
    8  exit
    9  date "+%Y-%m-%d %H:%M:%S"
   10  date
   11  date %r
   12  date +%R
   13  date +%x
   14  date +%Y
   15  date +%m
   16  date +%s
   17  date +%M
   18  date +%d
   19  date +%D
   20  date +%h
   21  date +%r
   22  date +%X
   23  date +%S
   24  file etc/services
   25  ls
   26  file /etc/services
   27  cat /etc/services
   28  less /etc/services
   29  file /home
   30  less /etc/services
   31  head /etc/services
   32  head -n 5 /etc/services
   33  tail /etc/services
   34  tail -n 5 /etc/services
   35  wc /etc/services
   36  wc -l /etc/services
   37  wc -c /etc/services
   38  wc -w /etc/services
   39  ls
   40  ls -l
   41  cd /etc
   42  ls
   43  ls -l
   44  cd ..
   45  cd ~
   46  history
```
**Rappel d'une commande précédente par son numéro dans l'historique (#34) à l'aide de la commande `!nombre`**
```bash
nathalie@Yoda:~$ !34
tail -n 5 /etc/services
dircproxy       57000/tcp                       # Detachable IRC Proxy
tfido           60177/tcp                       # fidonet EMSI over telnet
fido            60179/tcp                       # fidonet EMSI over TCP

# Local services
```

**Rappel d'une commande précédente par une partie de son nom, à l'aide de la commande `!string`**. Dans l'exemple ci-dessous, c'est la commande **#29** et non la **#26** qui sera exécutée.
```bash
nathalie@Yoda:~$ !fi
file /home
/home: directory
```

**Effacer l'historique**
```bash
nathalie@Yoda:~$ history -c
nathalie@Yoda:~$ history
    1  history
nathalie@Yoda:~$
```

>[!TIP]
La commande `clear` permet d'effacer l'écran du terminal.

## La touche `tab` pour auto-compléter une commande et le nom d'un fichier

- La touche `Tab` du clavier, permet de compléter rapidement les commandes et les noms de fichiers après avoir entré un nombre de caractères suffisant pour réduire les possibilités à une seule. 
- Si les caractères saisis ne sont pas uniques, appuyez deux fois sur la touche de tabulation pour afficher toutes les commandes correspondantes.

Exemple: Tapez `cat /etc/ser` puis appuyez sur la touche `Tab` pour auto-compléter le nom du fichier.


```bash
nathalie@Yoda ~$ pas Tab+Tab
passwd       paste        pasuspender
nathalie@Yoda ~$ pass Tab
nathalie@Yoda ~$ passwd 
Changing password for user nathalie.
Current password: 
```
- **Exemple** :
```bash
nathalie@Yoda ~$ ls /etc/pas1Tab
nathalie@Yoda ~$ ls /etc/passwd2Tab
passwd   passwd-
```
- **Résultat** :
```plaintext
passwd
passwd-
```

## La commande man

La commande `man` (abréviation de "manual") est utilisée pour afficher le manuel d'utilisation des commandes et programmes sous Linux. Elle fournit des informations détaillées sur la syntaxe, les options et les exemples d'utilisation des commandes.

### Utilisation de la commande `man`

Pour utiliser la commande `man`, il suffit de taper `man` suivi du nom de la commande ou du programme dont vous souhaitez consulter le manuel. Par exemple :

```bash
man ls
```

Cela affichera le manuel de la commande `ls`.

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

### Exemple

Pour afficher le manuel de la commande `cat`, vous pouvez utiliser :

```bash
man cat
```

[^1]: Nous étudierons cette commande la semaine prochaine.