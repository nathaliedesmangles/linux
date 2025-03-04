+++
title = "ATELIER #7: VIM et les fichiers de configuration (À MODIFIER)"
weight = 72
draft = true
+++

## Objectif de l'atelier

- Approfondir l’utilisation de VIM pour modifier des fichiers de configuration Linux de manière efficace.
1. **Modifier des fichiers de configuration Linux efficacement** :
   - Utiliser un minimum de touches.
   - Ne pas utiliser la souris.
2. **Compléter les exercices** :
   - 10 exercices de type A (le curseur est déjà placé).
   - 5 exercices de type B (le curseur commence au début du fichier).

---

## Instructions de remise

1. Fournissez les **captures d’écran** des exercices réussis via Moodle.
2. Chaque capture doit montrer :
   - La modification effectuée.
   - Le fichier sauvegardé dans l’état final.
3. Exemple de capture attendue :

   ![Exemple](exemple.png)

4. Une vidéo de démonstration est disponible :

   <video width="50%" src="a01-2.webm" type="video/webm" autoplay loop muted></video>
---


# Atelier

## Préparation

### Installation des outils

1. Créez un fichier `vim.sh` avec le contenu suivant :

   ```bash
   #!/bin/bash

   wget https://linuxh25.netlify.app/semaine7/atelier/vimrc.dot || echo ERREUR
   mv vimrc.dot ~/.vimrc
   sudo yum install -y epel-release
   sudo yum install -y meld
   sudo yum groupinstall -y "Development Tools"
   sudo yum install -y git automake

   mkdir ~/tmp
   cd ~/tmp
   git clone https://github.com/kernc/logkeys.git
   cd logkeys
   ./autogen.sh

   cd build
   ../configure
   make
   sudo make install || echo ERREUR
   ```

2. Exécutez le script pour installer les outils requis :

   ```bash
   $ bash vim.sh
   ```

### Téléchargement des exercices

1. Dans votre répertoire personnel, exécutez les commandes suivantes :

   ```bash
   $ cd ~
   $ wget https://linuxh25.netlify.app/semaine7/atelier/atelier_07.tar.gz || echo ERREUR
   $ tar zxvf atelier_07.tar.gz
   $ cd atelier_07
   ```
---

## Exercices de type A (curseur déjà placé)

### Exercice a01

#### Fichier de configuration

`/etc/default/grub`

#### Modification à apporter

- **Avant** :

  ```php
  GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb quiet"
  ```

- **Après** :

  ```php
  GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap quiet"
  ```

  Supprimez `rhgb` pour désactiver le démarrage graphique.

#### Performances attendues

|   Record à battre   |  Maximum acceptable  |
|---------------------|----------------------|
| 4 touches           | 9 touches            |

#### Commandes pour lancer l’exercice

```bash
$ sh afficher_objectif.sh a01
$ sh exercice_vim.sh a01
```

---

### Exercice a02

#### Fichier de configuration

`/etc/selinux/config`

### Modification à apporter

- **Avant** :

  ```php
  SELINUX=enforcing
  ```

- **Après** :

  ```php
  SELINUX=disabled
  ```

  Désactivez *SELinux*.

#### Performances attendues

| **Record à battre** | **Maximum acceptable** |
|-----------------------|-------------------------|
| 7 touches            | 25 touches             |

#### Commandes pour lancer l’exercice

```bash
$ sh afficher_objectif.sh a02
$ sh exercice_vim.sh a02
```

---

Répétez cette structure pour les autres exercices.

---

## Exercices de type B (curseur au début du fichier)

### Exercice b01

#### Fichier de configuration

`/etc/ssh/sshd_config`

#### Modification à apporter

- **Avant** :

  ```php
  #X11Forwarding yes
  ```

- **Après** :

  ```php
  X11Forwarding yes
  ```

  Décommentez la ligne pour activer la redirection graphique.

#### Performances attendues

| **Record à battre** | **Maximum acceptable** |
|-----------------------|-------------------------|
| 7 touches            | 18 touches             |

#### Commandes pour lancer l’exercice

```bash
$ sh afficher_objectif.sh b01
$ sh exercice_vim.sh b01
```

---

Continuez avec cette structure pour les exercices restants.


=====================================================
# Atelier 7b: vim avancé
Cet atelier et l'atelier précédent forment l'atelier 7.
## Objectif

1. Effectuer efficacement des modifications à des fichiers de configuration Linux
    1. NOTE: *efficacement* veut dire *en moins de X touches*, **sans utiliser la souris**
1. Vous devez réussir:
    * **10 exercices** de type A (curseur déjà placé)
    * **5 exercices** de type B (curseur au début du fichier)

## Remise

* À remettre sur Moodle: **Les captures d'écran**:
* Chaque capture d'écran correspond à un exercice réussi, p.ex:
    * Voici un exemple d'exercice réussi:


    <center>
    <img width="500px" src="exemple.png">
    </center>

* Voici comment l'exercice ci-haut s'est déroulé:

<center>
<video width="50%" src="a01-2.webm" type="video/webm" autoplay loop muted>
</center>


<!--


## Théorie *vim*

### Modes: normal, insertion, visuel

### Mouvements

### Modification en mode normal

### Entrer en mode insertion

### Combinaisons: mouvement et modifications

### Combinaisons: mouvement et insertion

### Répétitions

### Copier-coller

### Auto-complétion (CTRL+N et CTRL+P)

-->


## Astuces:

Utilisez ZZ pour sauvegarder et quitter dans vim.

Utilisez les commandes données dans les images Aide mémoire en fin du cours pour avoir le record.


# Travail à effectuer

## Préambule

### Installation des outils nécessaires

Copiez le texte suivant dans un script nommé <code class="gr">vim.sh</code>

{{< highlight bash >}}
#!/bin/bash

wget http://gyoukou.ca/vimrc.dot || echo ERREUR
mv vimrc.dot ~/.vimrc
sudo yum install -y epel-release
sudo yum install -y meld
sudo yum groupinstall -y "Development Tools"
sudo yum install -y git automake 

mkdir ~/tmp
cd ~/tmp
git clone https://github.com/kernc/logkeys.git
cd logkeys
./autogen.sh

cd build
../configure
make
sudo make install || echo ERREUR
{{< / highlight >}}

Exécutez le script :

<pre>
$ bash vim.sh
</pre>

### Télécharger et décompresser les exercices

<pre>
# IMPORTANT: cd ~ pour aller dans votre répertoire ~

$ cd ~

$ wget http://gyoukou.ca/atelier_06.tar.gz || echo ERREUR
$ tar zxvf atelier_06.tar.gz
$ cd atelier_06
</pre>

## Exercices A: le curseur est déjà placé

<b style="color:red">IMPORTANT: ne pas éditer directement les vrais fichiers de configuration. Editer plutôt la copie qui se trouve dans le dossier atelier téléchargé </b>

## Exercice a01


### Fichier de configuration

<code class="gr">/etc/default/grub</code>


* Configuration de `grub` (outil de démarrage)
* En particulier: options à donner au noyau Linux au démarrage


### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb quiet"
{{< / highlight >}}


APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap quiet"
{{< / highlight >}}


* Enlever `rhgb` désactive le démarrage graphique au profit de l'affichage d'un log
* (`rhgb` signifie *Red Hat Graphical Boot*)


### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>4 touches</td><td>9
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a01
$ sh exercice_vim.sh a01
</pre>

## Exercice a02


### Fichier de configuration

<code class="gr">/etc/selinux/config</code>


* *selinux* est un pare-feu d'application qui permet de contrôler ou limiter un grand nombre d'opérations sur un serveur Linux
* (*selinux* veut dire *Security Enhanced Linux*)


### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
SELINUX=enforcing
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
SELINUX=disabled
{{< / highlight >}}


* On déscative *selinux* (généralement préférable sur une machine usager)


### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>7 touches</td><td>25
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a02
$ sh exercice_vim.sh a02
</pre>

## Exercice a03


### Fichier de configuration

<code class="gr">/etc/fstab</code>

1. Liste des partitions utilisées dans le système
1. Par défaut, chaque partition est montée au démarrage

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
/dev/mapper/centos-tmp /tmp                     xfs     defaults        0 0
{{< / highlight >}}

APRÈS:

1. En retirant une ligne, on efface la définition d'une partition
1. Le répertoire `/tmp` devient un sous-répertoire de `/` (partition `centos-root`)


### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>4 touches</td><td>6
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a03
$ sh exercice_vim.sh a03
</pre>

## Exercice a04


### Fichier de configuration

<code class="gr">/etc/locale.conf</code>


1. Régionalisation du système: langue, date, etc.


### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
LC_TIME=""
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
LC_TIME="fr_CA.UTF-8"
{{< / highlight >}}

1. On veut copier `fr_CA.UTF-8` entre les `"` afin de définir aussi le format de date

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>8 touches</td><td>18
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a04
$ sh exercice_vim.sh a04
</pre>

## Exercice a05

### Fichier de configuration

<code class="gr">/etc/mime.types</code>

1. Définition des types de fichier et de leur extensions
1. NOTE: la commande `file` affiche le type d'un fichier

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
application/3gpp-ims+xml
application/activemessage
application/andrew-inset
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
application/3gpp-ims+xml			inconnu
application/activemessage			inconnu
application/andrew-inset			inconnu
{{< / highlight >}}

1. On ajoute l'extension `inconnu` pour les trois premiers types de fichier
1. NOTE: il y a trois tabulations entre le type et l'extension

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>18 touches</td><td>40
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a05
$ sh exercice_vim.sh a05
</pre>

## Exercice a06

### Fichier de configuration

<code class="gr">/etc/hosts</code>

1. Associe un nom réseau à son adresse
1. Pour ces noms, le système ne fera pas de requête DNS
1. (aussi avantageux pour faire des tests)
1. NOTE: ce fichier existe aussi en Windows

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
206.167.24.30    ciboulot.ca
#172.17.0.30      ciboulot.ca
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
#206.167.24.30    ciboulot.ca
172.17.0.30      ciboulot.ca
{{< / highlight >}}

1. On met en commentaire l'adresse publique de `ciboulot.ca`
1. On active l'adresse locale (seulement valide au Collège)

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>6 touches</td><td>12
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a06
$ sh exercice_vim.sh a06
</pre>

## Exercice a07

### Fichier de configuration

<code class="gr">/etc/firewalld/direct.xml</code>

1. Règles de pare-feu directes (écrites à la main)
1. NOTE: l'autre option est de générer les règles via la commande `firewall-cmd`

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
  <rule priority="0" table="filter" ipv="ipv4" chain="FORWARD">-i PRIVE -o PUBLIC -j ACCEPT</rule>
  <rule priority="0" table="filter" ipv="ipv4" chain="FORWARD">-i PUBLIC -o PRIVE -m state --state RELATED,ESTABLISHED -j ACCEPT</rule>
  <rule priority="0" table="nat" ipv="ipv4" chain="POSTROUTING">-o PUBLIC -j MASQUERADE</rule>
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
  <rule priority="0" table="filter" ipv="ipv4" chain="FORWARD">-i 192.168.1.4 -o 10.33.50.3 -j ACCEPT</rule>
  <rule priority="0" table="filter" ipv="ipv4" chain="FORWARD">-i 10.33.50.3 -o 192.168.1.4 -m state --state RELATED,ESTABLISHED -j ACCEPT</rule>
  <rule priority="0" table="nat" ipv="ipv4" chain="POSTROUTING">-o 10.33.50.3 -j MASQUERADE</rule>
{{< / highlight >}}


1. On insère des vraies adresses IP à partir d'un patron
1. NOTE: ces règles indique au système de faire du NAT


### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>37 touches</td><td>120
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a07
$ sh exercice_vim.sh a07
</pre>

## Exercice a08

### Fichier de configuration

<code class="gr">~/.bashrc</code>

1. Personnalisation du SHELL
1. Fichier lu à chaque ouverture du SHEL

### Modification à apporter

AVANT:


APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
alias la="ls -a"
{{< / highlight >}}

1. On ajoute la ligne pour créer un alias
1. NOTE: un alias est un raccourci pour une commande fréquemment utilisée.

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>12 touches</td><td>22
 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a08
$ sh exercice_vim.sh a08
</pre>

## Exercice a09

### Fichier de configuration

<code class="gr">/etc/resolv.conf</code>

1. Le ou les serveur DNS à utiliser

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
nameserver 10.33.50.1
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
nameserver 192.168.1.1
{{< / highlight >}}

1. On change l'adresse DNS à `192.168.1.1`

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>14 touches</td><td>35 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a09
$ sh exercice_vim.sh a09
</pre>

## Exercice a10

### Fichier de configuration

<code class="gr">/etc/ssh/sshd_config</code>

1. Configuration du serveur *SSH*

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
#X11Forwarding yes
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
X11Forwarding yes
{{< / highlight >}}

1. Certaines options sont déjà inscrites au fichier.
    * Pour les activer, il suffit de les décommenter
1. Ici, on active la redirection graphique

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>3 touches</td><td>8 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif.sh a10
$ sh exercice_vim.sh a10
</pre>

## Exercices B: le curseur est au début du fichier

<b style="color:red">IMPORTANT: ne pas éditer directement le fichier</b>

## Exercice b01

### Fichier de configuration

<code class="gr">/etc/ssh/sshd_config</code>

1. Configuration du serveur *SSH*

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
#X11Forwarding yes
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
X11Forwarding yes
{{< / highlight >}}

1. Même modification que `a10`, sauf que cette fois-ci le curseur n'est pas déjà placé

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>7 touches</td><td>18 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif b01
$ sh exercice_vim.sh b01
</pre>

## Exercice b02

### Fichier de configuration

<code class="gr">/etc/default/grub</code>

* Configuration de `grub` (outil de démarrage)
* En particulier: options à donner au noyau Linux au démarrage

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb quiet"
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
GRUB_CMDLINE_LINUX="rd.lvm.lv=centos/root rd.lvm.lv=centos/swap quiet"
{{< / highlight >}}

1. Même modification que `a01`, sauf que le curseur n'est pas déjà placé

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>8 touches</td><td>20 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif b02
$ sh exercice_vim.sh b02
</pre>

## Exercice b03

### Fichier de configuration

<code class="gr">/etc/services</code>

1. Liste des services réseau, protocoles et ports

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
systat          11/tcp          users
systat          11/udp          users
daytime         13/tcp
daytime         13/udp
qotd            17/tcp          quote
qotd            17/udp          quote
msp             18/tcp                          # message send protocol (historic)
msp             18/udp                          # message send protocol (historic)
chargen         19/tcp          ttytst source
chargen         19/udp          ttytst source
ftp-data        20/tcp
{{< / highlight >}}

APRÈS:

1. Effacer les services du ports 11 jusqu'au port 20 (inclusif)

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>11 touches</td><td>28 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif b03
$ sh exercice_vim.sh b03
</pre>

## Exercice b04

### Fichier de configuration

<code class="gr">/etc/passwd</code>

1. Information sur les usagers Linux

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
gnome-initial-setup:x:984:977::/run/gnome-initial-setup/:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
avahi:x:70:70:Avahi mDNS/DNS-SD Stack:/var/run/avahi-daemon:/sbin/nologin
apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
{{< / highlight >}}

APRÈS:

1. On efface les 4 dernières lignes
1. NOTE: habituellement, ces lignes sont effacées par la commande `userdel`

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>6 touches</td><td>15 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif b04
$ sh exercice_vim.sh b04
</pre>

## Exercice b05

### Fichier de configuration

<code class="gr">/etc/group</code>

1. Liste des groupes d'usagers Linux
1. Chaque usager est membre de son propre groupe
1. Un usager membre d'un autre groupe obtient des droits supplémentaires

### Modification à apporter

AVANT:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
wheel:x:10:
{{< / highlight >}}

APRÈS:

{{< highlight php "linenos=true,linenumbersintable=false"  >}}
wheel:x:10:mbergeron
{{< / highlight >}}

1. On ajoute l'usager `mbergeron` au groupe `wheel`
1. Le groupe `wheel` est le groupe qui peut faire la commande `sudo`

### Nombre de touches

<table><tr><th>Record à battre</th><th>Maximum acceptable</th></tr><tr><td>10 touches</td><td>25 touches</td></tr></table>

### Pour visualiser avec meld et lancer l'exercice

<pre>
$ sh afficher_objectif b05
$ sh exercice_vim.sh b05
</pre>
<!--
## Après la remise

### Restaurer votre configuration de *vim* (s'il y a lieu)

<pre>
$ mv ~/.vimrc.bak ~/.vimrc

