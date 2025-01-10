+++
title = "Système de fichiers et le shell BASH"
weight = 22
+++

![Arborescence](filesystem.png?width=100vw)

La structure du système de fichiers Linux est hiérarchique et organisée sous la forme d'un arbre inversé, où la racine (root) est représentée par `/`. 
Tous les fichiers et répertoires sont situés sous cette racine. Comprendre cette structure est essentiel pour naviguer et gérer efficacement un système Linux.

La structure du système de fichiers Linux est conçue pour être logique et organisée, facilitant ainsi la gestion et la navigation. Chaque répertoire a un rôle spécifique et contient des types de fichiers bien définis. Comprendre cette structure est crucial pour tout utilisateur ou administrateur de système Linux.

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
   - Contient les répertoires personnels des utilisateurs. Chaque utilisateur a son propre répertoire sous `/home`, par exemple `/home/utilisateur`.

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

## Le shell BASH

BASH, qui signifie "*Bourne Again SHell*", est une version améliorée du *Bourne Shell*. Il a été développé pour offrir plus de fonctionnalités et une meilleure compatibilité avec les scripts existants. Voici quelques différences clés :

	- **Compatibilité** : BASH est compatible avec les scripts du Bourne Shell, mais il offre également des fonctionnalités supplémentaires.

	- **Fonctionnalités : BASH inclut des fonctionnalités avancées comme l'édition de ligne de commande, l'historique des commandes, et le complétion automatique des noms de fichiers et des commandes.

	- **Portabilité** : BASH est disponible sur de nombreux systèmes d'exploitation, y compris Linux, macOS, et Windows (via WSL).

## Structure de base d'une commande

Une commande dans le shell suit généralement cette structure :
```
commande [options] [arguments]
```
- **commande** : Le programme ou l'outil que vous souhaitez exécuter.
- **options** : Des paramètres supplémentaires qui modifient le comportement de la commande.
- **arguments** : Les cibles sur lesquelles la commande doit agir (fichiers, répertoires, etc.).

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

| Commande | Description | Exemple |
|----------|-------------|---------|
| `pwd`    | Affiche le chemin absolu du répertoire courant | `pwd` -> `/home/utilisateur` |
| `cd`     | Change le répertoire courant | `cd Documents` -> Change au répertoire `Documents` |
| `ls`     | Liste les fichiers et répertoires | `ls` -> Affiche les fichiers et répertoires dans le répertoire courant |
| `cd ..`  | Remonte d'un niveau dans l'arborescence des répertoires | `cd ..` -> Remonte au répertoire parent |
| `cd ~`   | Va au répertoire personnel de l'utilisateur | `cd ~` -> Change au répertoire personnel, par exemple `/home/utilisateur` |

#### Exemples d'utilisation



### Commandes de gestion des fichiers et répertoires

| Commande | Description | Exemple |
|----------|-------------|---------|
| `cp`     | Copie des fichiers ou répertoires | `cp fichier.txt /destination` -> Copie `fichier.txt` vers `/destination` |
| `mv`     | Déplace ou renomme des fichiers ou répertoires | `mv fichier.txt nouveau_nom.txt` -> Renomme `fichier.txt` en `nouveau_nom.txt` |
| `rm`     | Supprime des fichiers | `rm fichier.txt` -> Supprime `fichier.txt` |
| `mkdir`  | Crée un nouveau répertoire | `mkdir nouveau_dossier` -> Crée un répertoire nommé `nouveau_dossier` |
| `rmdir`  | Supprime un répertoire vide | `rmdir dossier_vide` -> Supprime le répertoire `dossier_vide` s'il est vide |

#### Exemples d'utilisation
