+++
title = "Processus de démarrage, cibles, variables et boucle For"
weight = 31
+++

## Le processus de démarrage

Le processus de démarrage d'un système Linux suit plusieurs étapes essentielles, impliquant différents composants du système :

![Schema séquence](boot_process.jpeg)

1. **Activation du BIOS/UEFI**
   - Lorsque vous allumez votre ordinateur, le **BIOS** (*Basic Input Output System*) ou l'**UEFI** (*Unified Extensible Firmware Interface*) s'active.
   - Il vérifie le matériel et cherche le secteur de démarrage sur le disque (MBR ou GPT).

2. **Chargement du chargeur d'amorçage**
   - Le **MBR** (*Master Boot Record*) définit le chargeur de démarrage, comme **GRUB** (*GRand Unified Bootloader*).
   - **GRUB** affiche un menu permettant de choisir le système à démarrer.

3. **Chargement du noyau Linux (*Kernel*)**
   - Après la sélection de Linux, **GRUB** charge le noyau (kernel), qui est le cœur du système.
   - Le noyau initialise les pilotes, périphériques et la gestion de la mémoire.
   - Il charge aussi un disque temporaire (`initrd` ou `initramfs`) contenant les modules nécessaires au démarrage.

4. **Lancement du processus d'initialisation (`init` ou `systemd`)**
   - Le noyau lance le premier processus du système : `init` ou `systemd` (selon la distribution Linux).
   - Ce processus démarre les services et scripts de configuration (réseau, interface graphique, gestion des utilisateurs, etc.).

5. **Affichage de l'écran de connexion**
   - Une fois les services chargés, l'écran de connexion s'affiche, demandant un nom d'utilisateur et un mot de passe.

6. **Utilisation du système**
   - Après authentification, vous pouvez utiliser Linux, lancer des applications et exécuter des commandes.
   - Vous pouvez aussi arrêter ou redémarrer votre système avec `shutdown`, `reboot` ou `halt`.

---

## Les niveaux d'exécution (*Runlevels*) et cibles (*Targets*)

Autrefois, Linux utilisait des niveaux d'exécution (`runlevels`), qui définissaient les services actifs selon le mode de fonctionnement.
Avec `systemd`, ces niveaux sont remplacés par des **cibles** (`targets`). Cependant, la compatibilité avec les anciens niveaux est conservée.

### Changer temporairement le niveau d'exécution

Utilisez la commande suivante pour modifier le niveau d'exécution temporairement :
```bash
$ systemctl isolate <nom_niveau>
```

### Correspondance entre les niveaux d'exécution et les cibles *systemd*

| Niveau d'exécution | Cible systemd        | Description                           | Commande associée                   |
|--------------------|---------------------|-------------------------------------|----------------------------------|
| 0                | poweroff            | Arrêt du système                  | `$ systemctl isolate poweroff`  |
| 1                | rescue              | Mode utilisateur unique (maintenance) | `$ systemctl isolate rescue`    |
| 3                | multi-user          | Mode multi-utilisateur (ligne de commande) | `$ systemctl isolate multi-user` |
| 5                | graphical           | Mode graphique complet              | `$ systemctl isolate graphical` |
| 6                | reboot              | Redémarrage du système             | `$ systemctl isolate reboot`    |

### Afficher et modifier le niveau d'exécution

Pour lister les processus s’exécutant sur une machine :
```bash
$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  2 16:18 ?        00:00:01 /usr/lib/systemd/systemd --s
```

Pour afficher le niveau d'exécution actuel :
```bash
$ who -r
niveau d'exécution 5 2025-02-01 10:09
$ runlevel
N 5
```

{{% notice style="info" title="À propos de Runlevel"  %}}
La commande `runlevel` affiche deux valeurs : le niveau précédent et le niveau d’exécution actuel. Ici, **N** indique qu'il n'y avait pas de niveau précédent (au démarrage), et **5** est le niveau actuel graphique.
{{% /notice %}}


Pour connaître le niveau par défaut :
```bash
$ systemctl get-default
graphical.target
```

Pour modifier le niveau d'exécution par défaut :
```bash
$ systemctl set-default <nom_niveau>
```

**Exemple** : fixer le mode multi-utilisateur sans interface graphique comme niveau d'exécution par défaut :
```bash
$ systemctl set-default multi-user
```

Pour revenir au niveau d'exécution par défaut :
```bash
$ systemctl default
$ systemctl isolate default
```

{{% notice style="info" title="Difference entre isolate et set-default"  %}}
La différence entre les commandes est que la commande avec ***"isolate"*** est **exécutée immédiatement**, tandis que la commande avec ***"set-default"*** spécifie la cible obtenue **après le redémarrage**.
{{% /notice %}}


## Substitution de commande

La substitution de commande permet d'exécuter une commande et d'utiliser directement son résultat dans une autre commande.

### Syntaxe :
```
$(<commande>)
```

**Exemple 1** :

Bash exécute d'abord la commande `whoami` pour obtenir le nom de l'utilisateur, remplace `$(whoami)` par ce résultat, puis exécute `touch` pour créer un fichier portant ce nom.
```bash
$ touch $(whoami).txt
$ ls
bonjour.txt  Documents    groupe4  Images   Musique       ndesmangles.txt  Téléchargements  titi      toto      tutu      Vidéos
Bureau       fichier.txt  groupe6  Modèles  nathalie.txt  Public           test             titi.txt  toto.txt  tutu.txt

```

**Exemple 2** :

L'exemple ci-dessous affiche les fichiers du dossier personnel :
```bash
$ echo "Les fichiers de mon dossier personnel sont : $(ls)"
Les fichiers de mon dossier personnel sont : bonjour.txt
Bureau
Documents
Images
Modèles
Musique
ndesmangles.txt
Public
Téléchargements
titi
titi.txt
toto
toto.txt
tutu
tutu.txt
Vidéos
```

---

## Les variables

En Bash, il est possible de définir des variables. Certaines sont définies par le système au démarrage ou à l’ouverture de la session ; ce sont les **variables d’environnement** (ex: SHELL). Nous pouvons aussi créer nos propres variables (**variables utilisateur**). 

### Définir une variable utilisateur

Un utilisateur peut créer ou modifier ses propres variables. 

{{% notice style="warning" title="Attention"  %}}
Il ne faut pas mettre d’espace autour du `=`.
Les noms sont sensibles à la casse: `VAR1` ≠ `var1`
{{% /notice %}}

```bash
$ variable=valeur
```

**Exemples** :

Une variable peut contenir un booléen, une chaîne de caractères ou une valeur numérique :
```bash
$ variable=true
$ variable="Ceci est un texte"
$ variable=45
```

### Accéder au contenu d’une variable

Pour afficher la valeur d’une variable, il faut la préfixer avec `$` :
```bash
$ echo $variable
45
```

---

## Expansion des variables

L'expansion des variables permet d'utiliser une variable dans une commande en remplaçant son nom par sa valeur réelle avant l'exécution de la commande.


**Exemple**: Imaginons que nous souhaitons lister trois fichiers : `toto`, `titi`, `tutu`. Nous pouvons stocker ces noms dans une variable :

```bash
$ fichiers="toto titi tutu"
```

Ensuite, nous pouvons utiliser cette variable dans une commande :

```bash
$ ls -l $fichiers
-rw-r--r--. 1 ndesmangles ndesmangles 0  1 fév 10:37 titi
-rw-r--r--. 1 ndesmangles ndesmangles 0  1 fév 10:37 toto
-rw-r--r--. 1 ndesmangles ndesmangles 0  1 fév 10:37 tutu

```

**Que se passe-t-il ?**

Avant d'exécuter la commande, Bash remplace `$fichiers` par sa valeur réelle, puis exécute la commande résultante :

```bash
$ ls -l toto titi tutu
```

---

## Stocker le résultat d'une commande dans une variable

Il est possible d'affecter à une variable le résultat d'une commande :

```bash
$ ma_variable=$(ls /home)
```

**Exemple 1** : Stocker la date actuelle

```bash
$ x="La date est : $(date)"
$ echo $x
La date est : ven 31 jan 2025 15:39:37 EST
```

**Exemple 2** : Stocker le contenu d'un fichier

```bash
$ x=$(cat /etc/passwd)
$ echo $x
root:x:0:0:root:/root:/bin/bash bin:x:1:1:bin:/bin:/sbin/nologin daemon:x:2:2:daemon:/sbin:/sbin/nologin ...
```

{{% notice style="info" title="À savoir"  %}}
Le résultat d'une commande stocké dans une variable est retourné sur **une seule ligne**, ce qui peut poser problème pour les fichiers avec plusieurs lignes.
{{% /notice %}}

---

## Expansion de noms de fichiers à l'aide de caractères génériques

Lorsque l'on ne connaît pas précisément le nom d'un fichier ou que l'on veut rechercher plusieurs fichiers ayant un point commun, il est possible d'utiliser des caractères génériques.
L'expansion des caractères génériques permet de manipuler facilement plusieurs fichiers sans avoir à taper leurs noms en entier.

### Les principaux caractères génériques

| Caractère | Signification |
|-----------|--------------|
| `*` | Remplace n'importe quelle chaîne de caractères de n'importe quelle longueur |
| `?` | Remplace un seul caractère |

Le shell effectue une **expansion des noms de fichiers** en remplaçant les caractères génériques avant d'exécuter la commande.

**Exemple 1** : Lister tous les fichiers **.txt**

```bash
$ ls *.txt
```

Si les fichiers `toto.txt`, `titi.txt` et `tutu.txt` existent, la commande devient :

```bash
$ ls toto.txt titi.txt tutu.txt
titi.txt  toto.txt  tutu.txt
```

{{% notice style="info" title="Sachez que..."  %}}
Si lors de la création des fichiers, l'extension (**.txt**) était absente, la commande précédente `ls` retournera une erreur:
```bash
ls: impossible d'accéder à 'toto.txt': Aucun fichier ou dossier de ce type
ls: impossible d'accéder à 'titi.txt': Aucun fichier ou dossier de ce type
ls: impossible d'accéder à 'tutu.txt': Aucun fichier ou dossier de ce type
```
{{% /notice %}}

**Exemple 2** : Lister les fichiers avec un format spécifique

```bash
$ ls t?t?.txt
```

Le `?` remplace **un seul caractère**, donc cette commande affichera tous les fichiers du répertoire courant correspondant à ce modèle, par exemple : `tata.txt`, `titi.txt`, mais pas `tututu.txt`.

---

## L'expansion d'accolades

L'expansion d'accolades est une fonctionnalité de Bash qui permet de créer plusieurs chaînes de caractères en utilisant une syntaxe abrégée. Elle est particulièrement utile pour la création de fichiers, de répertoires ou pour l'exécution de commandes répétitives.

L'expansion d'accolades utilise la syntaxe suivante :

```
{élément1,élément2,...}
```

où **élément1**, **élément2**, etc. sont les différentes chaînes de caractères que vous souhaitez combiner. Bash va alors générer toutes les combinaisons possibles de ces éléments.

{{% notice style="warning" title="Attention"  %}}
Ne mettez aucun espace à l'intérieur des accolades.
{{% /notice %}}

## Exemples concrets

**Exemple 1** : Création de fichiers multiples

Supposons que vous souhaitez créer les fichiers **patata**, **patate**, **patati** et **patatu**. Sans l'expansion d'accolades, vous devriez exécuter la commande `touch` quatre fois ou écrire au complet tous les noms des fichiers :

```bash
$ touch patata
$ touch patate
$ touch patati
$ touch patatu
```
ou

```bash
$ touch patata patate patati patatu
```
Avec l'expansion d'accolades, vous pouvez faire tout cela en une seule ligne :

```bash
$ touch patat{a,e,i,u}
```

Bash va alors générer les chaînes **patata**, **patate**, **patati** et **patatu**, puis exécuter la commande `touch` pour chaque chaîne.

**Exemple 2** : Création de séquences numériques

Vous pouvez également utiliser l'expansion d'accolades pour créer des séquences numériques. Par exemple, si vous souhaitez créer les fichiers **test1.txt**, **test2.txt**, **test3.txt**, ..., **test12.txt**, vous pouvez utiliser la commande suivante :

```bash
$ touch test{1..12}.txt
```

Bash va générer les nombres de **1 à 12**, puis créer les fichiers correspondants.

## Autres exemples d'utilisation

**Exemple 1** : Création de fichiers dans un dossier spécifique

Pour créer 3 fichiers **test1.txt**, **test2.txt** et **test3.txt** dans le dossier **dossier1**, vous pouvez utiliser la commande suivante :

```bash
$ touch dossier1/test{1..3}.txt
```

**Exemple 2** : Combinaison de chaînes et de séquences

Pour créer les fichiers **patate**, **patati** et **patata** dans les dossiers **boite1** et **boite2**, vous pouvez utiliser la commande suivante :

```bash
$ touch boite{1,2}/patat{a,e,i}
```

## Protection contre l'expansion

Dans certains cas, vous pouvez souhaiter empêcher l'expansion d'accolades. Pour cela, vous pouvez utiliser le caractère d'échappement `\` ou les guillemets simples (`'`).

### Utilisation du caractère d'échappement

Le caractère `\` est un caractère d'échappement dans le shell Bash. Il permet de protéger le caractère qui le suit de son expansion. Par exemple :

```bash
$ echo je veux afficher \* et afficher \$x
je veux afficher * et afficher $x
```

### Utilisation des guillemets simples

Les guillemets simples (`'`) arrêtent tous les types d'expansion. Par exemple :

```bash
$ echo 'je veux afficher * et afficher $x'
je veux afficher * et afficher $x
```

### Utilisation des guillemets doubles

Les guillemets doubles (`"`) permettent uniquement l'expansion de variables et la substitution de commandes. Par exemple :

```bash
$ x=5
$ echo "je veux afficher * et afficher la valeur de $x"
je veux afficher * et afficher la valeur de 5
```
---

## La commande ***find***

La commande `find` est un outil essentiel pour naviguer dans le système de fichiers et localiser des fichiers ou répertoires spécifiques. Elle suit la structure générale suivante :

```
find <répertoire_de_départ> <options>
```

- <**répertoire_de_départ**>: Indique le répertoire où la recherche doit commencer. La commande explorera ce répertoire et tous ses sous-répertoires.
- <**options**>: Définissent les critères de recherche, tels que le nom du fichier, le type, la date de modification, etc.

### Recherche par nom

L'option `-name` est la plus courante pour rechercher des fichiers par leur nom.

- Rechercher un fichier nommé `services` dans tout le système (i.e. à partir de la racine):

```bash
$ find / -name services
```

- Rechercher tous les fichiers se terminant par `.txt` dans le répertoire courant :

```bash
$ find . -name "*.txt"
```

- Rechercher tous les fichiers commençant par `p` dans le répertoire courant :

```bash
$ find . -name "p*"
```

- Rechercher tous les fichiers de 4 caractères se terminant par `n` dans `/var/log` :

```bash
$ find /var/log -name "???n"
```

### Pièges à éviter

Lors de l'utilisation de `find`, il est crucial de comprendre comment Bash gère l'expansion des variables et les guillemets. Voici quelques points importants :

- **Expansion des variables**: Bash n'effectue pas d'expansion de noms de fichiers pour la commande `find`. Cela permet à `find` d'interpréter correctement les motifs avec des caractères génériques comme `*.txt`.
- **Utilisation de guillemets**: Il est souvent nécessaire d'utiliser des guillemets pour protéger les caractères spéciaux et éviter des erreurs d'interprétation.

Le tableau suivant illustre les différences de comportement :

| Commande                                  | Résultat                                                                                                                                                                                                                                                        |
| :---------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ls *.txt`                                | Affiche tous les fichiers se terminant par `.txt`. Si aucun fichier `.txt` n'est trouvé, la commande s'exécute comme si les guillemets étaient présents.                                                                                                            |
| `ls "*.txt"`                              | Affiche le fichier nommé exactement `*.txt`.                                                                                                                                                                                                                            |
| `find . -name *.txt`                      | L'expansion a lieu avant la recherche. Trois cas sont possibles :<br/>- Aucun fichier `.txt` : La commande s'exécute comme si les guillemets étaient présents.<br/>- Un fichier `.txt` : Seul ce fichier est recherché.<br/>- Plusieurs fichiers `.txt` : La commande échoue. |
| `find . -name "*.txt"`                    | Recherche tous les fichiers `.txt` à partir du répertoire courant.                                                                                                                                                                                                   |

### Exercices

1.  **Manipulation de variables et de `ls` :**
    - Créez une variable `variable_etc` contenant la liste des fichiers de `/etc` et affichez-la.
    - Observez le résultat et évaluez sa lisibilité.
    - Essayez d'exécuter `ls` suivi du nom de votre variable. Expliquez le comportement observé.

2.  **Recherche de fichiers de configuration :**
    - Trouvez tous les fichiers se terminant par `.conf` et stockez leurs noms dans une variable.
    - Essayez d'exécuter `ls` suivi du nom de votre variable.
    - Utilisez la commande `du -sh <fichier>` pour afficher la taille de chaque fichier de configuration.

3.  **Création de fichiers avec factorisation :**
    - Créez un répertoire et utilisez la commande `touch` avec la syntaxe de factorisation pour créer les fichiers suivants : `test1.txt`, `test2.txt`, `test3.txt`, `test1.doc`, `test2.doc`, `test3.doc`, `test1.tot`, `test2.tot`, `test3.tot`.

4.  **Utilisation de caractères génériques :**
    - Affichez uniquement les fichiers `.txt` commençant par `test` (trouvez plusieurs solutions).
    - Affichez tous les fichiers `.txt` et `.tot`.
    - Affichez tous les fichiers `test1`.

{{% notice style="green" title="Solution à venir..." groupid="notice-toggle" expanded="false" %}}
<!--

1.  **Manipulation de variables et de `ls` :**
```bash
variable_etc=$(ls /etc)
echo $variable_etc
ls $variable_etc # Affiche les fichiers séparés par des espaces
```

2.  **Recherche de fichiers de configuration :**
```bash
fichiers_conf=$(find /etc -name "*.conf")
ls $fichiers_conf # Affiche les fichiers séparés par des espaces
for fichier in $fichiers_conf; do
  du -sh $fichier
done
```

3.  **Création de fichiers avec factorisation :**
```bash
mkdir repertoire_test
touch repertoire_test/test{1..3}.{txt,doc,tot}
```

4.  **Utilisation de caractères génériques :**
```bash
ls repertoire_test/test*.txt # Solution 1
ls repertoire_test/test[1-3].txt # Solution 2
ls repertoire_test/*.{txt,tot}
ls repertoire_test/test1*
```
-->
{{% /notice %}}

## Itération sur le résultat d'une commande avec la boucle ***for***

La syntaxe de base d'une boucle ***for*** est la suivante :
```bash
for i in arg1 arg2 ...; do commande; done
```

-   `i` : Variable qui prendra successivement la valeur de chaque argument.
-   `arg1 arg2 ...` : Liste des éléments sur lesquels itérer.
-   `commande` : Commande à exécuter pour chaque élément de la liste.

### Exemples d'utilisation

**Exemple 1** : Affichage du contenu de fichiers .txt

Supposons que vous ayez les fichiers suivants :

```
fichier1.txt	# contient le mot 'Bonjour'
fichier2.txt	# contient le mot 'tout'
fichier3.txt	# contient le mot 'le'
fichier4.txt	# contient le mot 'monde'
```

Pour afficher le contenu de chaque fichier, vous pouvez utiliser une boucle `for` :
```bash
$ for i in fichier1.txt fichier2.txt fichier3.txt fichier4.txt; do cat $i; done
Bonjour
tout
le
monde
```

**Exemple 2** : Utilisation d'une variable pour stocker le résultat d'une commande

Vous pouvez stocker le résultat d'une commande dans une variable, puis itérer sur cette variable :
```bash
$ fichiers=$(ls fichier*.txt)
$ for i in $fichiers; do cat $i; done
Bonjour
tout
le
monde
```

**Exemple 3** : Passage direct de la commande à la boucle `for`

Il est également possible de passer directement la commande à la boucle `for` :
```bash
$ for i in $(ls fichier*.txt) ; do cat $i; done
Bonjour
tout
le
monde
```

**Exemple 4** : Utilisation de l'expansion de noms de fichiers

Pour simplifier l'itération sur des fichiers, vous pouvez utiliser l'expansion de noms de fichiers :
```bash
$ for i in fichier*.txt; do cat $i; done
Bonjour
tout
le
monde
```

### Formatage de la boucle ***for*** dans un script

Dans un script, il est recommandé d'écrire la boucle `for` sur plusieurs lignes pour une meilleure lisibilité. Les sauts de ligne remplacent le `;` dans ce cas :

```bash
for i in $var
do
  echo $i
done
```

### Exercices

1.  **Liste des fichiers de `/bin` :**
    - Créez une variable contenant la liste des fichiers du répertoire `/bin`.

2.  **Affichage des fichiers :**
    - Parcourez cette variable à l'aide d'une boucle `for` et affichez chaque fichier sur une ligne différente.

3.  **Taille des fichiers :**
    - Sachant que vous pouvez concaténer des chaînes de caractères comme ceci :

    ```bash
    echo /bin/$i
    ```

    - Essayez d'afficher la taille des fichiers du répertoire `/bin`. Utilisez la commande `du -sh <fichier>` pour afficher la taille d'un fichier.


{{% notice style="green" title="Solution à venir..." groupid="notice-toggle" expanded="false" %}}
<!--
1.  **Liste des fichiers de `/bin` :**
```bash
fichiers_bin=$(ls /bin)
```

2.  **Affichage des fichiers :**
```bash
for i in $fichiers_bin; do
  echo $i
done
```

3.  **Taille des fichiers :**
```bash
for i in $fichiers_bin; do
  echo /bin/$i
  du -sh /bin/$i
done
```
-->
{{% /notice %}}

