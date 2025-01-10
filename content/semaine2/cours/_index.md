+++
title = "Shell et la ligne de commande"
weight = 21
+++

## Qu'est-ce que le SHELL?

Le terme "Shell" désigne un programme qui interprète les commandes que vous tapez et les exécute. Il existe plusieurs types de shells, comme le ***Bourne Shell (sh)***, le ***C Shell (csh)***, le ***Korn Shell (ksh)***, et bien d'autres.

## La ligne de commande

1. **Ligne de commande**:
   - La ligne de commande est l'interface où vous tapez vos commandes. Elle est souvent représentée par un symbole `$` ou `#` pour les utilisateurs root (administrateur).
   - Lorsque vous êtes prêt à exécuter une commande, appuyez sur la touche Entrée. Tapez chaque commande sur une ligne séparée. Le résultat de la commande est affiché avant l’invite du shell suivante.

**Exemple**:
```plaintext
[user@host]$ whoami
user
[user@host]$ 
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
| `wc`         | Compte les lignes, mots et caractères. | `-l` pour les lignes, `-w` pour les mots. |
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

#### 2. commande `` pour changer le mot de passe de l'utilisateur

```bash
[nathalie@Yoda ~]$ passwd
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
**NB**: Pour revenir à la ligne de commande, taper la lettre 'q'

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

En premier, allons dans le répertoire /etc à l'aide de la commande `cd`
```bash
nathalie@Yoda:~$ cd /etc
```
Utilisons la commande `ls`
```bash
nathalie@Yoda:/etc$ ls
PackageKit              cron.weekly     groff          locale.conf          nsswitch.conf  rmt                supercat
X11                     cron.yearly     group          locale.gen           opt            rpc                sysctl.conf
adduser.conf            crontab         group-         localtime            os-release     rsyslog.conf       sysctl.d

nathalie@Yoda:/etc$ ls -l
total 340
drwxr-xr-x 1 root root       4096 Apr 23  2024 PackageKit
drwxr-xr-x 1 root root       4096 Apr 23  2024 X11
-rw-r--r-- 1 root root       3444 Jul  5  2023 adduser.conf
drwxr-xr-x 1 root root       4096 Apr 23  2024 alternatives
drwxr-xr-x 1 root root       4096 Apr 23  2024 apparmor
```

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
````

## La touche `tab` pour auto-compléter une commande et le nom d'un fichier

| `Tab`        | Tapez `cat /etc/ser` puis appuyez sur `Tab` pour auto-compléter le nom du fichier. |

   - **Description** : Permet de compléter rapidement les commandes et les noms de fichiers après avoir entré un nombre de caractères suffisant pour réduire les possibilités à une seule. Si les caractères saisis ne sont pas uniques, appuyez deux fois sur la touche de tabulation pour afficher toutes les commandes correspondantes.
     ```bash
     [user@host ~]$ pas Tab+Tab
     passwd       paste        pasuspender
     [user@host ~]$ pass Tab
     [user@host ~]$ passwd 
     Changing password for user user.
     Current password: 
     ```
   - **Exemple** :
     ```bash
     [user@host ~]$ ls /etc/pas1Tab
     [user@host ~]$ ls /etc/passwd2Tab
     passwd   passwd-
     ```
   - **Résultat** :
     ```plaintext
     passwd
     passwd-
     ```

10. **history**
   - **Description** : Affiche la liste des commandes précédemment exécutées, précédées d’un numéro de commande. 
     ```bash
     [user@host ~]$ history
     ...output omitted...
     23  clear
     24  who
     25  pwd
     26  ls /etc
     27  uptime
     28  ls -l
     29  date
     30  history
     ```
   - **Exemple** :
     ```bash
     [user@host ~]$ !ls
     ls -l
     total 0
     drwxr-xr-x. 2 user user 6 Mar 29 21:16 Desktop
     ...output omitted...
     [user@host ~]$ !26
     ls /etc
     abrt                     hosts                     pulse
     adjtime                  hosts.allow               purple
     aliases                  hosts.deny                qemu-ga
     ...output omitted...
     ```
   - **Résultat** :
     ```plaintext
     ls -l
     total 0
     drwxr-xr-x. 2 user user 6 Mar 29 21:16 Desktop
     ls /etc
     abrt                     hosts                     pulse
     adjtime                  hosts.allow               purple
     aliases                  hosts.deny                qemu-ga
     ```
====


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