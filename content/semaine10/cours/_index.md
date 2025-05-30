+++
title = "Utilisateurs et groupes"
weight = 101
+++

## Qu'est-ce qu'un utilisateur qu'est-ce qu'un groupe ?

- **Utilisateur** : Une entité (**personne ou processus**) ayant un compte sur le système, identifiée par un ***UID*** (*User ID*). Chaque utilisateur possède des **permissions** et des **droits spécifiques**.

- **Groupe** : Un **ensemble d’utilisateurs qui partagent les mêmes permissions** sur des fichiers, dossiers ou ressources du système. Cela permet d’accorder des droits de manière collective plutôt qu’individuellement. Chaque groupe possède un ***GUID*** (*Group ID*).

**Groupe principal**

- Chaque utilisateur appartient à **un groupe principal** (défini dans `/etc/passwd`).
- Par défaut, tous les fichiers créés par un utilisateur appartiennent à ce groupe.

**Groupes secondaires**

- Un utilisateur peut appartenir à **plusieurs groupes secondaires**, ce qui lui permet d’hériter d’autres permissions.

## Les utilisateurs

### Types de comptes

Il existe quatre types de comptes sous Linux :

- **root** : Le super-utilisateur qui possède tous les droits (***UID 0***).
- **nobody** : Un compte très restreint utilisé pour les personnes non authentifiées (***UID 65534***).
- **Comptes systèmes et d'application** : Utilisés pour exécuter certaines applications et services (démons) avec des permissions limitées. Cela réduit les risques si une faille de sécurité est exploitée. Leurs ***UID*** se situent **entre 1 et 999**.
- **Comptes standards** : Destinés aux utilisateurs humains (***UID*** **supérieur à 1000**).

### Création d'un utilisateur (commande *useradd*)

- La commande de création d'un utilisateur est **`useradd`**.
- Vous devez disposer des **droits d'administrateur** pour exécuter cette commande.
- Elle prend au moins un paramètre : le nom de l'utilisateur à créer.

**Exemple :** création de l'utilisateur `bob` :

```bash
$ useradd bob
```

#### Opérations effectuées par *useradd*

- **Ajout de l'utilisateur** dans le fichier **`/etc/passwd`**.
- Attribution d'un ***UID*** généré automatiquement et stockage dans **`/etc/passwd`**.
- **Création d'un groupe** du même nom que l'utilisateur, qui deviendra son **groupe principal**. Le <span style="color:red;">**groupe principal d’un utilisateur**</span> sera aussi le <span style="color:red;">**groupe propriétaire des fichiers**</span> créés par cet utilisateur.
- **Création du **répertoire personnel** `/home/user`** avec les permissions adéquates.
- **Copie du contenu de `/etc/skel`** dans le répertoire personnel de l'utilisateur.
{{% notice style="green" title="Qu'est-ce que /etc/skel ?" groupid="notice-toggle" expanded="false" %}}
`/etc/skel` est un dossier qui contient des **fichiers et dossiers modèles** utilisés lors de la création d'un nouvel utilisateur.
{{% /notice %}}
- **Création d'un dossier de messagerie** dans **`/var/spool/mail`**.
{{% notice style="green" title="Qu'est-ce que /var/spool/mail ?" groupid="notice-toggle" expanded="false" %}}
`/var/spool/mail` (`/var/mail` sur certaines distributions comme **Ubuntu**) est utilisé pour **stocker les courriels locaux** (générés par le système ou des services internes) des utilisateurs. 
{{% /notice %}}


{{% notice style="note" title="Sachez que" %}}
Aucun mot de passe n'est créé automatiquement.
Lorsque vous ajoutez un mot de passe, il sera stocké sous forme chiffrée dans le fichier `/etc/shadow`.
{{% /notice %}}

Vous pouvez ensuite vérifier l'utilisateur ajouté dans le fichier `/etc/passwd` :
<!--
![passwd useradd](passwd_file.png)
-->

```bash
$ tail -1 /etc/passwd
bob:x:1002:1002::/home/bob:/bin/bash
```

**Explication** 
```bash
user:x:uid:gid:commentaire:repertoire personnel:shell par défaut
```

#### Options de la commande *useradd*

| Option | Description | Exemple |
|--------|------------|---------|
| **-u UID** | Spécifier un UID personnalisé | `useradd -u 1502 user2` |
| **-g groupe** | Définir un groupe principal | `useradd -g vboxfs user3` |
| **-G groupes** | Ajouter des groupes secondaires | `useradd -G wheel,users user3` |
| **-c commentaire** | Ajouter une description | `useradd -c "Mon commentaire" user4` |
| **-e date** | Définir une date d'expiration | `useradd -e 2026-07-15 user5` |
| **-s shell** | Changer le shell par défaut | `useradd -s /bin/tcsh user6` |
| **-d répertoire** | Choisir un répertoire personnel | `useradd -d /home/toto user7` |

{{% notice style="Warning" title="L'ajout d'un commentaire" %}}
- L'ajout d'un commentaire doit se faire **en même temps** que la création de l'utilisateur
- L’information est stockée dans le fichier `/etc/passwd` :
  ```bash
  $ grep <utilisateur> /etc/passwd
  ```
{{% /notice %}}

### Afficher les *UID* et *GID* (commande *id*)

La commande **`id`** permet d'afficher ces informations :

| Commande | Description |
|----------|------------|
| `id -u <utilisateur>` | Afficher uniquement l'UID. |
| `id <utilisateur>`    | Afficher les détails de l'utilisateur. |
| `id -g <utilisateur>` | Afficher uniquement le GID principal. |
| `id -G <utilisateur>` | Afficher tous les groupes (principal et secondaires) de l'utilisateur (par GID). |
| `id -Gn <utilisateur>` | Afficher les groupes avec leurs noms. |

{{% notice style="note" title="À savoir" %}}
Si on ne précise pas l'utilisateur, la commande `id` s'applique à l'utilisateur connecté. Par exemple:
```bash
[julien@localhost ~]$ id -g
```
affiche le groupe principal de julien
{{% /notice %}}

### Changer de mot de passe (commande *passwd*)

Pour modifier son mot de passe, utilisez la commande **`passwd`** :

```bash
$ passwd bob
```

{{% notice style="warning" title="Attention" %}}
Seul **root** peut changer le mot de passe d'un autre utilisateur. Aucun mot de passe oublié ne peut être récupéré.
Le mot de passe est stocké sous forme chiffrée dans **`/etc/shadow`**.
{{% /notice %}}


### Suppression d'un utilisateur (commande *userdel*)

La commande **`userdel`** permet de supprimer un utilisateur :

| Commande | Description |
|----------|------------|
| `userdel <utilisateur>` | Supprimer un utilisateur **sans** supprimer son dossier personnel |
| `userdel -r <utilisateur>` | Supprimer un utilisateur **et** son répertoire personnel |

### Modifier un utilisateur (commande *usermod*)

La commande **`usermod`** permet de modifier un utilisateur existant.

| Commande | Description | Exemple |
|----------|------------|---------|
| `usermod -d /nouveau_repertoire_personnel <utilisateur>` | Changer le répertoire personnel | `usermod -d /home/ndesmangles bob` |
| `usermod -s /chemin_shell <utilisateur>` | Modifier le shell par défaut | `usermod -s /bin/tcsh bob` |
| `usermod -g nouveauGroupe <utilisateur>` | Modifier le groupe principal | `usermod -g root bob` |
| `usermod -L <utilisateur>` | Désactiver un utilisateur | `usermod -L bob` |
| `usermod -U <utilisateur>` | Réactiver un utilisateur | `usermod -U bob` |

{{% notice style="note" title="Notez..." %}}
- Les **chemins absolus** (`/`) pour les options `-d` et `-s` de la commande `usermod`.
- La commande `usermod -d` **ne déplace pas** le contenu de l’ancien répertoire personnel vers le nouveau.
{{% /notice %}} 

### Ajouter un utilisateur à un groupe

| Commande | Description | Exemple |
|----------|------------|---------|
| `usermod -aG <groupe1, groupe2> <utilisateur>` | **Ajouter** un utilisateur à un groupe secondaire, tout en **conservant** les groupes secondaires existants. | `usermod -aG sudo, wheel bob` |
| `usermod -G <groupe1, groupe2> <utilisateur>` | Ajouter un utilisateur à un groupe secondaire, mais **supprime** les groupes secondaires existants. | `usermod -G sudo, wheel bob` |
| `groups <utilisateur>` | Voir les groupes d'un utilisateur. | `groups bob` |
| `newgrp <groupe>` | Appliquer immédiatement les changements de groupe. | `newgrp sudo` |

{{% notice style="info" title="Information" %}}
- Les groupes peuvent être spécifiés par leur **nom** ou leur ***GID***.
{{% /notice %}}

---

## Les groupes

- Le **groupe principal** d'un utilisateur est utilisé lorsqu'il crée des fichiers : <span style="color:red;">ce groupe devient propriétaire des fichiers créés</span> par l'utilisateur.
- L'appartenance à d'autres groupes **définit les permissions** d'accès aux fichiers.
- Les groupes sont enregistrés dans **`/etc/group`**.

### Types de groupes

- **root** (***GID 0***)
- **Groupes système**: utilisés pour les services/*deamons*(***GID 1 - 999***)
- **nobody** (***GID 65534***)
- **Groupes standards** (***GID >= 1000***)

### Création et gestion des groupes

| Commande | Description | Exemple |
|----------|------------|---------|
| `groupadd nomGroupe` | Créer un groupe. | `groupadd principal1` |
| `groupadd -g GID nomGroupe` | Créer un groupe avec un GID spécifique. | `groupadd -g 1560 monGroupe` |
| `groupdel nomGroupe` | Supprimer un groupe. | `groupdel principal1` |
| `groupmod -n nouveauNom ancienNom` | Changer le nom d'un groupe. | `groupmod -n principal2 principal1` |
| `groupmod -g nouveauGID nomGroupe` | Changer le GID d'un groupe. | `groupmod -g 2000 nomGroupe` |


## Le groupe *wheel*

- Le groupe ***wheel*** permet à ses membres d'utiliser des commandes avec des **privilèges administratifs** grâce à `sudo`. 
- L'utilisateur est ajouté à ce groupe par ***root*** s'il souhaite lui donner ces droits 

---

## Exercices

### Utilisateurs

1. Créez un utilisateur nommé **exercice1**.
2. Quel est son groupe principal ?
3. Modifiez son groupe principal pour qu'il appartienne au groupe **root**.
4. Ajoutez-le au groupe secondaire **wheel**.
5. Affichez la liste des groupes auxquels appartient l'utilisateur.
6. Ajoutez le groupe **exercice1** aux groupes secondaires de l'utilisateur.

{{% notice style="green" title="Solution" groupid="notice-toggle" expanded="false" %}}
```bash
#1. Créez un utilisateur nommé exercice1
$ sudo useradd exercice1
[sudo] Mot de passe de <user>: 

#2. Quel est son groupe principal ?
$ id -g exercice1
1001
$ groups exercice1
exercice1 : exercice1

#3. Modifiez son groupe principal pour qu'il appartienne au groupe **root**.
$ udo usermod -g root exercice1
[sudo] Mot de passe de <user>: 

#4. Ajoutez-le au groupe secondaire **wheel**.
$ sudo usermod -aG wheel exercice1

#5. Affichez la liste des groupes auxquels appartient l'utilisateur.
$ groups exercice1
exercice1 : root wheel
 
#6. Ajoutez le groupe exercice1 aux groupes secondaires de l'utilisateur.
sudo usermod -aG exercice1 exercice1
```
{{% /notice %}}

### Groupes

1. Comment ajouter un utilisateur à un groupe ?
2. Créez un groupe nommé **principal1**.
3. Placez **exercice1** dans ce groupe comme groupe principal.
4. Supprimez le groupe **principal1**.
5. Quel est maintenant le groupe principal de **exercice1** ?

{{% notice style="green" title="Solution" groupid="notice-toggle" expanded="false" %}}
```bash
#1. Comment ajouter un utilisateur à un groupe
$ sudo usermod -aG nom_groupe nom_utilisateur

#2. Créez un groupe nommé principal1
$ sudo groupadd principal1

#3. Placez **exercice1** dans ce groupe comme groupe principal.
$ sudo usermod -g principal1 exercice1

#4. Supprimer le groupe principal1
$ sudo groupdel principal1
groupdel: cannot remove the primary group of user 'exercice1'

#5. Quel est maintenant le groupe principal de **exercice1** ?
id -g exercice1
1002
```
{{% /notice %}}

