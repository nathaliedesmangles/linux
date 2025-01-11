+++
title = "Système de fichiers, les commandes de base"
weight = 31
+++

![Arborescence](filesystem.png?width=100vw)

La structure du système de fichiers Linux est hiérarchique et organisée sous la forme d'un arbre inversé, où la racine (root) est représentée par `/`. 
Tous les fichiers et répertoires sont situés sous cette racine. 

{{% notice style=warning title=Attention %}}
Comprendre cette structure est essentiel pour naviguer et gérer efficacement un système Linux.
**Chaque répertoire a un rôle spécifique et contient des types de fichiers bien définis**. 
{{% /notice %}}

La structure du système de fichiers Linux est conçue pour être logique et organisée, facilitant ainsi la gestion et la navigation. 

## Tout est fichier

Sous Linux, TOUT les éléments visibles dans l’arborescence du système de fichiers sont des fichiers.

- Un fichier est un fichier
- Un répertoire est un fichier
- Une clé USB est un fichier
- Une partition est un fichier
- Un disque dur est un fichier
- etc.

## Répertoires principaux

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
   - Contient les répertoires personnels des utilisateurs. Chaque utilisateur a son propre répertoire sous `/home`, par exemple `/home/nathalie`.
```bash
nathalie@Yoda:~$ cd /home
nathalie@Yoda:/home$ ls
nathalie
```

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

### Les chemins absolu et relatifs

#### Chemin absolu

Un chemin absolu est un chemin complet qui commence à la racine du système de fichiers. Il indique l'emplacement exact d'un fichier ou d'un répertoire, peu importe où vous vous trouvez dans le système de fichiers. Par exemple :
```
/home/utilisateur/Documents/fichier.txt
```
Dans cet exemple, le chemin commence par `/`, qui est la racine du système de fichiers, et suit l'arborescence jusqu'au fichier `fichier.txt`.

#### Chemin relatif

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

### Les commandes de navigation dans l'arborescence des fichiers

| Commande | Description |
|----------|-------------|
| `pwd`    | Affiche le chemin absolu du répertoire courant |
| `cd`     | Change le répertoire courant | 
| `cd ..`  | Remonte d'un niveau dans l'arborescence des répertoires. `cd ../.. ` remonte de deux niveaux, etc. |
| `cd ~`   | Va au répertoire personnel de l'utilisateur | 

#### Exemples d'utilisation

```bash
nathalie@Yoda:~$ pwd
/home/nathalie

nathalie@Yoda:~$ cd ..
nathalie@Yoda:/home$

nathalie@Yoda:~$ cd /etc
nathalie@Yoda:/etc$

nathalie@Yoda:/etc$ cd ~
nathalie@Yoda:~$

```

### Commandes de gestion des fichiers et répertoires

| Commande | Description |
|----------|-------------|
| `touch`  | Crée un fichier vide. |
| `cp`     | Copie des fichiers ou répertoires. |
| `mv`     | Déplace ou renomme des fichiers ou répertoires. |
| `rm`     | Supprime des fichiers. L'option `-r` permet de supprimer récursivement un dossier et tout ce qu'il contient. |
| `mkdir`  | Crée un nouveau répertoire. |
| `rmdir`  | Supprime uniquement un répertoire s'il est **vide**. |

{{% notice style=warning title=Attention %}}
- Vous ne pouvez pas supprimer un répertoire qui contient des fichiers, y compris des fichiers masqués ou système. Si vous tentez de le faire, le message suivant s’affiche :
`The directory is not empty`
- Vous ne pouvez pas utiliser la commande **`rmdir`** pour supprimer le répertoire actif. Si vous tentez de supprimer le répertoire actif, le message d’erreur suivant s’affiche :
`The process can't access the file because it is being used by another process.`
Si vous recevez ce message d’erreur, vous devez passer à un autre répertoire (et non à un sous-répertoire du répertoire actif), puis réessayer.
{{% /notice %}} 

#### Exemples d'utilisation

```bash
nathalie@Yoda:~$ touch fichier.txt
nathalie@Yoda:~$ ls
fichier.txt

nathalie@Yoda:~$ mkdir repertoire
nathalie@Yoda:~$ ls
fichier.txt  repertoire

nathalie@Yoda:~$ cp fichier.txt copie_fichier.txt
nathalie@Yoda:~$ ls
copie_fichier.txt  fichier.txt  repertoire

nathalie@Yoda:~$ mv copie_fichier.txt fichier2.txt
nathalie@Yoda:~$ ls
fichier.txt  fichier2.txt  repertoire

nathalie@Yoda:~$ mv fichier2.txt repertoire
nathalie@Yoda:~$ ls
fichier.txt  repertoire

nathalie@Yoda:~$ cd repertoire
nathalie@Yoda:~/repertoire$ ls
fichier2.txt

nathalie@Yoda:~/repertoire$ rm fichier2.txt
nathalie@Yoda:~/repertoire$ ls

nathalie@Yoda:~/repertoire$ cd ..
nathalie@Yoda:~$ ls
fichier.txt  repertoire

nathalie@Yoda:~$ rmdir repertoire
nathalie@Yoda:~$ ls
fichier.txt
```

[^1]: Nous étudierons comment gérer les droits des différents utilisateurs plus tard dans ce cours.