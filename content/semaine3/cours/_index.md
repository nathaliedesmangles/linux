+++
title = "Processus de démarrage, cibles, variables et boucle For"
weight = 31
+++

## Séquence de démarrage de Linux

Le processus de démarrage de Linux est une série d'étapes qui se déroulent depuis l'allumage de l'ordinateur jusqu'à l'affichage de l'invite de commande ou de l'interface graphique. Comprendre ce processus est essentiel pour diagnostiquer et résoudre les problèmes de démarrage. 

Lorsqu’un système Linux démarre, plusieurs étapes se succèdent de manière ordonnée pour préparer la machine et le système d’exploitation à fonctionner. Voici les étapes principales :

1. **BIOS/UEFI** : Initialise le matériel et recherche un périphérique amorçable.
2. **Bootloader (GRUB)** : Charge le noyau Linux et transfère le contrôle au système d’exploitation.
3. **Noyau Linux** : Configure le matériel, monte le système de fichiers racine, et démarre le processus d’initialisation.
4. **Init/Systemd** : Gère le lancement des services et des processus utilisateur.

![Schema séquence](boot_process.jpeg)

---

## Étape 1 : BIOS/UEFI

### Rôle du BIOS/UEFI

- Le BIOS (*Basic Input/Output System*) ou l’UEFI (*Unified Extensible Firmware Interface*) est le premier programme exécuté lorsqu’une machine est allumée.
- Il effectue des tests matériels (POST) et localise le *bootloader* sur un disque amorçable, et charge le MBR en mémoire
- Le BIOS transfère alors le contrôle au code du *Master Boot Record* (**MBR**). Le MBR se trouve dans le premier secteur du disque dur (secteur 0), c’est-à-dire les premiers 512 octets de l’espace de stockage.
- Le MBR contient un programme minimal d’amorçage (bootloader primaire) qui localise et charge le ***bootloader*** secondaire (ex. GRUB ou LILO) depuis une partition active.

### Modes de démarrage

- **Legacy (BIOS)** : Mode traditionnel compatible avec les anciens systèmes.
- **UEFI** : Plus moderne, prend en charge des fonctionnalités avancées comme le *Secure Boot*.

{{% notice style="orange" title="BIOS ou UEFI ?" groupid="notice-toggle" expanded="false" %}}
- Avec l’essor de l’UEFI, le MBR est remplacé par le schéma GPT (***GUID Partition Table***), qui offre plus de flexibilité (gestion de disques de grande taille et partitions multiples).
- Les systèmes UEFI n’utilisent pas de *MBR* classique mais démarrent directement via un fichier exécutable dans une partition EFI (ESP).
- Le MBR est une étape initiale critique dans les systèmes ***BIOS/MBR***, mais il est remplacé dans les environnements modernes utilisant UEFI.
{{% /notice %}}

---

## Étape 2 : *Bootloader* (*GRUB*)

### Rôle de GRUB

- Le ***bootloader*** (**GRUB** : *GRand Unified Bootloader*) est responsable de charger le noyau Linux en mémoire.
- Il peut proposer plusieurs options de démarrage, comme des versions différentes du noyau ou un mode de récupération.

---

## Étape 3 : Le noyau Linux (*Kernel*)

### Fonctionnalités du noyau au démarrage

1. **Détection matérielle** : Identifie et initialise les composants matériels.
2. **Chargement des modules** : Ajoute des pilotes pour des périphériques spécifiques.
3. **Montage du système de fichiers racine** : Prépare l’environnement pour le reste du système.
4. **Lancement du processus d’initialisation** : Appelle le gestionnaire d’initialisation (PID 1).

{{% notice style="info" title="Définition" %}}
- ***PID*** : *Processus ID* est l'identifiant d'un processus.
{{% /notice %}}

---

## Étape 4 : *Init* et *Systemd*

### Gestionnaires d’initialisation

- **SysVinit** : Ancien gestionnaire basé sur des scripts shell.
- **Systemd** : Gestionnaire moderne basé sur des unités (units) qui remplacent les scripts traditionnels.


### Rôle de l’init (PID 1)

- L’init est le premier processus utilisateur démarré par le noyau.
- Il gère le lancement des services essentiels et assure la transition vers un état prêt pour les utilisateurs.
- Les services sont des processus en arrière-plan qui effectuent des tâches spécifiques (ex. serveur SSH, journalisation).
- Quand tous les services sont lancés, le programme init affiche l’écran de connexion, qui vous demande votre nom d’utilisateur et votre mot de passe.

## 5. Les cibles / niveaux d'exécution (*Runlevels*)

- Les cibles (niveaux d'exécution) définissent l'état du système et les services qui doivent être exécutés.
- Dans le passé, les modes de fonctionnement étaient connus sous le nom de **niveaux d'exécution**, chacun permettant l'accès à un ensemble spécifique de services. Le concept de niveaux d'exécution a été remplacé par celui de **cibles** (*target*). 
- L'ensemble des services associés aux anciens niveaux d'exécution ont été conservés dans le système de cibles de `systemd`, afin de maintenir la compatibilité avec les scripts et les configurations existantes.

{{% notice style="info" title="Information" %}}
- Les distributions modernes comme Fedora, Ubuntu et Almalinux utilisent donc `Systemd`.
{{% /notice %}}

Voici les cibles les plus courantes et leur correspondance:

| Niveau d'exécution  | Description                        | *Target* Systemd                  |
|---------------------|------------------------------------|-----------------------------------|
| 0                   | Arrêt du système.                  | poweroff.target                   |
| 1                   | Mode monoutilisateur (maintenance).| rescue.target ou emergency.target |
| 3                   | Multi-utilisateur (texte)          | multi-user.target                 |
| 5                   | Multi-utilisateur (graphique)      | graphical.target                  |
| 6                   | Redémarrage                        | reboot.target                     |

### Différence entre *emergency.target* et *rescue.target*

- `emergency.target` : Le mode le plus minimal, aucun système de fichiers supplémentaire n’est monté, pas de réseau, pas de services. C’est vraiment pour les urgences critiques.
- `rescue.target` : Similaire au mode monoutilisateur (niveau d’exécution 1). Il monte certains systèmes de fichiers et démarre un ensemble limité de services, mais pas de services réseau.

## Commandes liées aux cibles *Systemd* ou *init*.

{{% notice style="note" title="Note" %}}
- Les commandes `systemctl` qui modifient l’état du système ou des services touchent des fichiers et des processus sous contrôle strict, souvent localisés dans des répertoires comme `/etc/systemd/system` ou `/lib/systemd/system`. Ces zones sont protégées pour éviter des modifications accidentelles ou malveillantes.
- Dans la plupart des cas, vous devez avoir des privilèges `sudo` ou être connecté en tant qu'utilisateur root pour utiliser la commande `systemctl`, car elle est conçue pour gérer des services, des cibles (*targets*), et d'autres composants système qui nécessitent des autorisations élevées.
{{% /notice %}}


### Pour lister les processus s’exécutant sur une machine

**Avec `ps`** : 
- Affiche tous les processus s'exécutant sur la machine.
```bash
$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  2 16:18 ?        00:00:01 /usr/lib/systemd/systemd --s

```
### Pour connaître le niveau d’exécution actuel

1. **Avec `Systemd`** :
   ```bash
   $ systemctl get-default
   graphical.target
   ```

2. **Avec `runlevel` (SysVinit)** :
   ```bash
   $ runlevel
   N 5
   ```
   - Cette commande affiche deux valeurs : le précédent et l’actuel niveau d’exécution. Ici, `N` indique qu'il n'y avait pas de niveau précédent (au démarrage), et `5` est le niveau actuel.

---

### Pour se placer temporairement dans un niveau d’exécution

1. **Avec `systemctl isolate reboot` :**
   - Cette commande met immédiatement le système en état de redémarrage. Elle isole le *target* associé à l’action de redémarrage (souvent **reboot.target**).
   - **Effet** : Redémarrage immédiat, tous les services et processus actifs sont arrêtés proprement.

2. **Avec `systemctl isolate poweroff` :**
   - Cette commande met immédiatement le système hors tension (extinction complète). Elle isole le *target* associé à l’arrêt (**poweroff.target**).
   - **Effet** : Extinction immédiate, tous les services et processus actifs sont arrêtés proprement.

---

### Pour voir quel est le niveau d’exécution par défaut

1. **Avec Systemd** :
   ```bash
   $ systemctl get-default		# Renvoie le *target* par défaut.
   ```

2. **Avec `runlevel` (SysVinit)** :
   - Vous pouvez également utiliser `runlevel` comme décrit précédemment.
---

### Pour modifier le niveau par défaut

1. **Avec Systemd** :
   - Changez le *target* par défaut avec :
     ```bash
     $ sudo systemctl set-default multi-user.target	# Niveau d’exécution 3 (mode texte multi-utilisateur).
     ```

2. **Avec SysVinit** :
   - Modifiez le fichier `/etc/inittab` (pour les systèmes utilisant encore SysVinit) :
     ```bash
     $ id:5:initdefault:		# Définit le niveau 5 (mode graphique) comme niveau d’exécution par défaut.
     ```
---

### Pour se rendre directement au niveau d’exécution par défaut

- Utilisez la commande suivante pour forcer le système à se placer dans le niveau d’exécution ou *target* par défaut :
  ```bash
  $ sudo systemctl isolate default.target
  ```
---

**Question**: Suite aux commandes suivantes, que se passe-t-il ?

1. **`$ init 0` :**
{{% notice style="green" title="Réponse" groupid="notice-toggle" expanded="false" %}}
   - Envoie le système au niveau d’exécution 0, qui correspond à l’**extinction**.
   - **Effet** : Éteint immédiatement la machine, tout comme la commande `systemctl poweroff`.
{{% /notice %}}


2. **`$ init 6` :**
{{% notice style="green" title="Réponse" groupid="notice-toggle" expanded="false" %}}
   - Envoie le système au niveau d’exécution 6, qui correspond au **redémarrage**.
   - **Effet** : Redémarre immédiatement la machine, tout comme la commande `systemctl reboot`.
{{% /notice %}}

---

## Les variables utilisateur en *Bash*

### Nomenclature, assignation et affichage des variables

1. Lors de la création d'une variable, **toujours** utiliser des noms descriptifs. 
Exemple:  `nombre_utilisateurs` au lieu de `nombre`.

{{% notice style="warning" title="Attention"  %}}
- Les caractères spéciaux ou espaces dans les noms peuvent causer des erreurs.
{{% /notice %}}

2. Les noms sont sensible à la casse.
Exemple: `VAR1` ≠ `var1` 

3. Pas besoin de déclaration explicite, pour affecter une valeur on utilise `=` **sans espace** autour de `=`.
Exemple:
```bash
$ ma_variable="Bonjour, Linux!"
```

4. Pour afficher la valeur d'une variable, on utilise le symbole `$` devant le nom.
Exemple: 
```bash
$ echo $ma_variable
```

5. Pour supprimer une variable, on utilise `unset` suivi du nom de la variable (**sans `$`**).
Exemple: 
```bash
$ unset ma_variable
```

### Stocker le résultat d’une commande dans une variable

En Bash, vous pouvez capturer la sortie d’une commande dans une variable en utilisant la syntaxe `$(...)`. 

**Exemple 1** : Stocker la date courante
```bash
$ date_courante=$(date +%Y-%m-%d)	# La date sera stockée dans date_courante aaaa-mm-jj
$ echo $date_courante			# Affiche la valeur de date_courante
2025-01-09
```

**Exemple 2** : Compter et stocker le nombre de fichiers dans le répertoire courant
```bash
$  nombre_fichiers=$(ls | wc -l)
$  echo $nombre_fichiers
8
```
- **`ls`** : Liste les fichiers et répertoires dans le répertoire courant.
- **`wc -l`** : Compte le nombre de lignes de la sortie de `ls`, correspondant au nombre d'entrées.[^1]


## Expansion des variables en *Bash*

L'expansion des variables consiste à remplacer le nom d'une variable par sa valeur lors de l'exécution d'une commande, permettant ainsi d'utiliser dynamiquement des données dans des scripts ou des commandes.
 
**Exemple 1:** Remplacement de la variable par sa valeur  
```bash
$ fichiers="toto titi tutu"
$ ls -l $fichiers
```
Commande exécutée :  
```bash
$ ls -l toto titi tutu
```

**Exemple 2:** Une variable peut inclure des options :  
```bash
$ fichiers="-l toto titi tutu"
$ ls $fichiers
```
Commande équivalente :  
```bash
$ ls -l toto titi tutu
```

## Stocker le résultat d'une commande dans une variable

Stocker le résultat d'une commande dans une variable consiste à capturer la sortie d'une commande en utilisant la syntaxe `$(commande)` afin de la réutiliser ultérieurement dans un script ou une commande.
 
```bash
$ fichiers=$(ls)
$ ls "$fichiers"  # Toujours utiliser des guillemets pour gérer les espaces.
```

## Expansion de noms de fichiers (* et ?)

Dans *Bash* on peut utiliser des **caractères génériques** pour étendre des motifs en liste de fichiers existants.

| Caractère     | Description                                    | Exemple               | Résultat                               |
|---------------|------------------------------------------------|-----------------------|----------------------------------------|
| `*`           | Remplace une chaîne de longueur variable       | `ls *.txt`            | Fichiers comme `toto.txt`, `titi.txt`  |
| `?`           | Remplace un seul caractère                     | `ls t?t?.txt`         | Fichiers comme `toto.txt`, `titi.txt`  |

## Expansion d’accolades

L'expansion d'accolades en Bash permet de générer rapidement des séries de chaînes ou de motifs en factorisant des éléments variables, comme dans `{a,b,c}` pour produire `a`, `b`, `c`, ou `{1..5}` pour générer `1`, `2`, `3`, `4`, `5`.

|  But                     | Commande                      | Résultat                      |
|--------------------------|-------------------------------|-------------------------------|
| Générer des variations   | `touch patat{a,e,i,o,u,y}`    | `patata`, `patate`, ...       |
| Générer une séquence     | `touch test{1..12}.txt`       | `test1.txt`, `test2.txt`, ... |

{{% notice style="warning" title="Attention" %}}
- Pas d’espace dans les accolades
{{% /notice %}}


## Protéger contre l’expansion

Protéger contre l’expansion en Bash consiste à empêcher l’interprétation des caractères spéciaux, des variables ou des commandes en utilisant des guillemets simples, doubles ou le caractère d’échappement `\`.

| Méthode               | Commande                           | Effet                                       |
|-----------------------|------------------------------------|---------------------------------------------|
| Échappement `\`       | `echo Je veux afficher \* et \$x`  | Affiche `*` et `$x` sans expansion.         |
| Guillemets simples `'`| `echo 'Voici * et $x'`             | Aucun remplacement, affiche littéralement.  |
| Guillemets doubles `"`| `echo "Valeur : $x"`               | Permet l’expansion des variables.           |

---

## Commandes spéciales et expansions

Certaines commandes comme `find`[^1] nécessitent une attention particulière concernant l'expansion.

### Exemple : Recherche avec **find**
Pour rechercher tous les fichiers `.txt` :
```bash
$ find / -name "*.txt"
```
Ici, les guillemets protègent `*.txt` pour empêcher Bash d’expandre le motif avant de passer à `find`. Cela garantit que `find` traite correctement le motif.

---

## Bonnes pratiques avec les variables

1. **Toujours utiliser des guillemets pour éviter les problèmes avec les espaces ou caractères spéciaux :**
   ```bash
   $ ls "$fichiers"
   ```

2. **Protégez les motifs pour les commandes comme `find`:**
   ```bash
   $ find / -name "*.txt"
   ```

3. **Utilisez les accolades pour générer des séquences et factoriser vos commandes :**
   ```bash
   $ touch fichier{1..10}.txt
   ```

## Itération sur les résultats de commandes

La boucle `for` est un élément fondamental qui permet de répéter une action pour chaque élément d'une liste ou d'un ensemble de valeurs. Elle est particulièrement utile pour automatiser des tâches répétitives.


### Structure générale

```bash
for variable in liste
do
    commande1
    commande2
    ...
done
```

- **`variable`** : Une variable temporaire qui prend successivement chaque valeur de la liste.
- **`liste`** : Un ensemble de valeurs, qui peut être défini explicitement ou généré dynamiquement.
- Les commandes entre `do` et `done` sont exécutées pour chaque valeur de la liste.

---

### Exemple 1 : Parcourir une liste statique

```bash
for animal in chat chien oiseau
do
    echo "Je suis un $animal"
done
```

**Sortie :**
```
Je suis un chat
Je suis un chien
Je suis un oiseau
```

---

### Exemple 2 : Parcourir des fichiers d’un répertoire

```bash
for fichier in *.txt
do
    echo "Traitement de $fichier"
done
```

- Ici, `*.txt` est un motif de fichier.
- Bash remplace `*.txt` par la liste des fichiers correspondants dans le répertoire courant.

**Sortie :** (si le répertoire contient `file1.txt` et `file2.txt`)
```
Traitement de file1.txt
Traitement de file2.txt
```

---

### Exemple 3 : Générer une liste avec une séquence

Vous pouvez utiliser une séquence avec `{debut..fin}` pour générer des nombres ou des caractères :

```bash
for i in {1..5}
do
    echo "Nombre : $i"
done
```

**Sortie :**
```
Nombre : 1
Nombre : 2
Nombre : 3
Nombre : 4
Nombre : 5
```

---

### Exemple 4 : Ajouter des pas dans une séquence

Pour parcourir une séquence avec un pas spécifique, utilisez `{debut..fin..pas}` :

```bash
for i in {1..10..2}
do
    echo "Nombre impair : $i"
done
```

**Sortie :**
```
Nombre impair : 1
Nombre impair : 3
Nombre impair : 5
Nombre impair : 7
Nombre impair : 9
```

---

### Exemple 5 : Lire des entrées à partir d’une commande

Vous pouvez parcourir les fichiers dans un répertoire pour lister les utilisateurs disposant d'un répertoire personnel sur le système :

```bash
for user in $(ls /home)
do
    echo "Utilisateur avec un répertoire : $user"
done
```

**Explication** :
- `ls /home` liste les répertoires dans `/home`, où chaque répertoire correspond généralement à un utilisateur ayant un compte sur le système.
- La boucle `for` parcourt chaque nom de répertoire et l'associe à la variable `user`.
- La commande `echo` affiche ensuite le nom de chaque utilisateur. 

---

### Utiliser des guillemets pour protéger les valeurs

Si les éléments de la liste contiennent des espaces, utilisez des guillemets pour éviter des erreurs :

```bash
for fichier in "Fichier 1.txt" "Fichier 2.txt"
do
    echo "Traitement de $fichier"
done
```

---

## Bonnes pratiques avec la boucle *for*

1. **Liste explicite** : Utilisez une liste statique ou une séquence simple :
   ```bash
   for i in {1..10}
   ```

2. **Motifs et fichiers** : Parcourez les fichiers d’un répertoire avec des motifs :
   ```bash
   for fichier in *.txt
   ```

3. **Commandes dynamiques** : Créez une liste à partir du résultat d'une commande :
   ```bash
   for utilisateur in $(who | awk '{print $1}')
   ```

4. **Guillemets** : Protégez les éléments avec des espaces :
   ```bash
   for fichier in "file 1" "file 2"
   ```



[^1]: Nous verrons cette commande plus en détails au prochain cours.