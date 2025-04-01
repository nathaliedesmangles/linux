+++
title = "Les droits d'accès"
weight = 111
draft = true
+++


## Introduction

Linux étant un système multi-utilisateurs, il peut être nécessaire de donner des droits différents sur les fichiers pour les protéger:

 - Confidentialité

 - Protection contre les erreurs

 - ...

Sur Linux, il existe deux types de droits: les droits standards et les ACL. Nous verrons uniquement les droits standards qui sont les plus utilisés.

De plus, c'est avec les droits que l'on peut rendre un fichier exécutable.

## Description

La commande suivante permet d'afficher les permissions sur les fichiers:

<pre>$ ls -l
total 40
-rwxr-xr-x.  1 axel axel  1767 10 déc 16:52 1895560_2018-12-08_18h59m02s.py
drwxr-xr-x.  3 axel axel    18 21 mar 14:22 Bureau
drwxrwxr-x.  3 axel axel    22  7 mar 17:08 config
drwxrwxr-x.  2 axel axel  4096 10 avr 13:16 correction
drwxrwxr-x.  2 axel axel    69  7 fév 17:10 cours
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Documents
-rw-rw-r--.  1 axel axel   343 27 mar 11:14 expr.txt
drwxrwxr-x.  3 axel axel    93  7 mar 15:22 hugo
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Images
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Modèles
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Musique
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Public
drwxrwxr-x. 13 axel axel  4096 11 avr 18:06 quickstart
-rw-r--r--.  1 axel axel 11459 31 mar 12:53 README.md
drwxrwxr-x.  3 axel axel  4096 17 mar 15:24 scripts
-rwxrw-r--.  1 axel axel    52 25 fév 14:14 script.sh
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Téléchargements
-rw-rw-r--.  1 axel axel     9  3 avr 13:53 total.txt
drwxr-xr-x.  7 axel axel   162 13 mar 21:27 tp01
drwxr-xr-x.  2 axel axel     6 18 nov 21:08 Vidéos
</pre>

![droits](../images/droits.png)

Les permissions s'affichent sous la forme de 3 colonnes de 3 lettres chacune.

 - La première colonne représente les droits pour le propriétaire du fichier (u pour user).

 - La deuxième colonne représente les droits pour le groupe propriétaire du fichier (g pour groupe).

 - La troisième colonne représente les droits pour tous les autres utilisateurs (o pour other).

Les 3 lettres représentent les droits:
 
 - <code class="gr">r</code>: pour la lecture (Read)

 - <code class="gr">w</code>: pour l'écriture (Write)

 - <code class="gr">x</code>: pour l'exécution (eXecute). Est l'exécution pour un fichier, le droit de parcourir pour un répertoire (sans possibilité de voir le contenu si le droit Read n'a pas été donné.

Les permissions s'appliquent à une personne et un groupe:

 - La première colonne représente la personne qui est propriétaire du fichier ou du répertoire.

 - La deuxième colonne représente le groupe qui est propriétaire du fichier ou du répertoire.

## Modification des permissions

Deux personnes peuvent modifier les permissions:

 - Le propriétaire du fichier ou du répertoire

 - root

La commande pour modifier les droits est <code class="gr">chmod</code>.

Il existe 2 méthodes pour modifier les droits:

 - La méthode symbolique

 - La méthode octale

### La méthode symbolique

Elle utilise les symboles des droits:

 - <code class="gr">r</code> : lecture

 - <code class="gr">w</code> : écriture

 - <code class="gr">x</code> : exécution

Elle utilise les symboles des utilisateurs:

 - <code class="gr">u</code> : l'utilisateur propriétaire

 - <code class="gr">g</code> : le groupe propriétaire

 - <code class="gr">o</code> : les autres

 - <code class="gr">a</code> : tous (utilisateur, groupe et autres)

Elle utilise les symboles d'ajout, de suppression ou de définition pour spécifier les droits:

 - <code class="gr">+</code> : pour ajouter un ou plusieurs droits à une catégorie

 - <code class="gr">-</code> : pour retirer un ou plusieurs droits à une catégorie

 - <code class="gr">=</code> : pour définir les droits d'une ou plusieurs ctégories.

Voici des exemples:

- Pour donner tous les droits à tous les utilisateurs:

<pre>$ chmod a+rwx fichier
$ chmod ugo=rwx fichier</pre>

- Pour enlever le droit d'écriture aux autres:

<pre>$ chmod o-w fichier</pre>

- Pour enlever le droit d'écriture aux autres et au groupe:

<pre>$ chmod go-w fichier</pre>

- Pour affecter les droits à toute l'arborescence en dessous:

<pre>$ chmod -R u-x directory</pre>

### La méthode octale

En binaire, les droits sont les suivants:

|r|w|x|
|:---:|:---:|:---:|
|1|1|1|
|4|2|1|

Pour connaître la valeur des droits que l'on souhaite attribuer, il suffit d'additionner la valeur des droits individuels.

Ainsi, si on veut donner les droits de lecture seulement, ce sera 4, écriture seulement ce sera 2 et exécution seulement ce sera 1.

Si on veut donner les droits de lecture et écriture ce sera 6, lecture et exécutionce sera 5...

Avec la méthode octale, il faut obligatoirement définir les droits pour les trois catégories : le propriétaire, le groupe propriétaire et les autres.

Voici des exemples:

- Pour donner tous les droits à tous les utilisateurs:

<pre>$ chmod 777 fichier</pre>

- Pour enlever le droit d'écriture aux autres:

<pre>$ chmod 775 fichier</pre>

- Pour enlever le droit d'écriture aux autres et au groupe:

<pre>$ chmod 755 fichier</pre>

- Pour affecter les droits à toute l'arborescence en dessous:

<pre>$ chmod -R 644 directory</pre>

## Modification de l'utilisteur propriétaire

Il est possible de modifier le propriétaire d'un fichier ou d'un répertoire.

Seul root peut effectuer cette action.

La commande est <code class="gr">chown</code>.

<pre>$ chown user fichier</pre>

Pour changer à la fois le groupe propriétaire et l'utilisateur:

<pre>$ chown user:group fichier</pre>

Pour changer toute l'arborescence:

<pre>$ chown -R user directory</pre>

## Modification du groupe propriétaire

De même qu'il est possible de changer le propriétaire, il est possible de changer le groupe propriétaire.

Deux utilisateurs ont le droit de modifier le groupe propriétaire:

 - root

 - Le propriétaire actuel s'il appartient au groupe auquel on va donner le fichier.

<pre>$ chgrp group fichier</pre>

Pour changer le groupe pour toute une arborescence:

<pre>$ chgrp -R group directory</pre>

Il est possible de modifier d'un seul coup l'utilisteur propriétaire et le groupe propriétaire:

<pre>$ chmod user:group fichier</pre>

## Le droit d'exécution

Pour un répertoire elle donne le droit de parcourir le répertoire mais pas d'afficher son contenu.

Pour un fichier c'est elle qui lui permettra de s'exécuter (programmes, scripts).

La permission exécuter sur les fichiers, joue un peu le même rôle l'extension .exe sous Windows.

Un script ou un programme ne pourra pas s'exécuter sans la permission d'exécution.

Pour que vos script puissent s'exécuter sans les précéder de la commande bash, il faut leur donner la permission d'exécution.

On pourra alors exécuter le script:

<pre>$ ./script.sh</pre>

Le <code class="gr">./</code> permet de dire où se trouve le fichier à exécuter.

Le système cherche les exécutables dans les répertoires contenus dans la variable d'environnement <code class="gr">$PATH</code>.

Si l'exécutable n'est pas dans un de ces répertoires, il faudra spécifier son chemin (soit absolu, soit relatif).

Pour voir le contenu de la variable <code class="gr">$PATH</code>:

<pre>$ echo $PATH</pre>

Pour la modifier, la variable, deux possibilités:

<pre>$ export PATH=$PATH:&lt;nouveau chemin&gt;</pre>

Ou en mettant cette ligne dans <code class="gr">.bashrc</code> ou <code class="gr">.bash_profile</code> pour que ce soit permanent.

La dernière chose à faire pour pouvoir exécuter un script est de spécifier l'interprèteur à utiliser lors de lexécution. Pour ceci, il faudra ajouter la ligne suivante tout en haut du fichier:

{{< highlight bash>}}
#!/bin/bash
{{< / highlight >}}

---

## Exercices

1. Trouvez les permissions suivantes :

 - Quelles sont les permissions octales pour -w-r-----?

 - Quelles sont les permissions octales pour rw-r---w-?

 - Quelles sont les permissions symboliques pour 755?

 - Quelles sont les autorisations symboliques pour 426?

 - Quelle est la commande pour ajouter la permission exécution à l'utilisateur (mode symbolique)?

 - Quelle est la commande pour supprimer la lecture aux autres sur toute une arborescence?

2. Tests de permissions :

Créer une arborescence telle que celle ci-dessous:

<pre>
Cours11
├── fic1.txt
└── rep1
    └── fic2.txt
</pre>

En faisant varier les droits (pour l'utilisateur propriétaire) sur le répertoire rep1 et sur le fichier fic1.txt, essayez les commandes comme touch, cd, ls sur le répertoire rep1 et cat ou ajout de texte sur les fichiers à l'intérieur (fic1.txt et fic2.txt).

Remplissez les tableaux suivant avec les résultats.

<u>Concernant le répertoire rep1 et ses permissions</u>

||r|w|x|rw|wx|rx|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|
|Je peux afficher le contenu avec <code class="gr">ls</code>| | | | | | |
|Je peux créer un fichier avec <code class="gr">touch</code>| | | | | | |
|Je peux traverser le répertoire avec <code class="gr">cd</code>| | | | | | |

<u>Concernant le fichier fic1.txt ses permisssions</u>

||r|w|x|rw|wx|rx|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|
|Je peux afficher le contenu avec <code class="gr">cat</code>| | | | | | |
|Je peux ajouter du texte| | | | | | |

<u>Concernant le fichier fic2.txt et les permissions du répertoire rep1</u>

||r|w|x|rw|wx|rx|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|
|Je peux voir le fichier| | | | | | |
|Je peux afficher le contenu avec <code class="gr">cat</code>| | | | | | |
|Je peux ajouter du texte| | | | | | |












