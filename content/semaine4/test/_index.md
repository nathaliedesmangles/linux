+++
title = "Test 1"
weight = 170
draft = true
+++

# Informations générales

- Il y a un total de **18 questions** pour **100 minutes (1h40)**.   
	- **9 questions courtes** (commandes à donner)  
	- **9 questions longues** (explications, différences entre commandes, analyse)
- **Temps pour la relecture**: ~ 19 min   
- **Recommendation pour la gestion du temps par type de question**  
	- **Questions courtes (commandes à donner) :** ~2-3 minutes chacune  
	- **Questions longues (explication, analyse) :** ~5-7 minutes chacune   
---

## Semaine 2

### Navigation et exploration de l’arborescence Linux
 
Exercice 1 : Explorer l’arborescence Linux
- Navigation dans l’arborescence : pwd, cd, cd .., cd ~
- Affichage du contenu d’un répertoire : ls 

#### Contexte
 
Vous êtes un administrateur système débutant et devez naviguer efficacement dans l’arborescence Linux. Répondez aux 4 questions courtes suivantes:


1. Votre répertoire de travail est `/var/log/apache2`. Vous voulez revenir au répertoire `/var`. Quelle commande exécuterez vous ? (utiliser un chemin relatif)
* **Réponse :** `cd ../..`
* **Explication :** Pour remonter de deux niveaux, on utilise deux fois ".." avec la commande `cd`. Chaque ".." nous fait remonter d'un niveau.

2. Votre répertoire de travail est /home/utilisateur. Vous souhaitez accéder au répertoire `Musique` qui se trouve à la racine de votre système de fichiers. Quelle commande exécuterez vous ? (utiliser un chemin absolu)

* **Réponse :** `cd /Musique`
* **Explication :** Le chemin `/Musique` est un chemin absolu, car il commence par la racine ("/"). Cela signifie que nous allons directement au répertoire "Musique" situé à la racine du système, quelle que soit notre position actuelle.

3. Votre répertoire actuel est `/opt/bin`. Vous voulez retourner à votre répertoire personnel /home/utilisateur. Quelle instruction utiliserez vous ? (chemin absolu OU relatif)

* **Réponse :** `cd /home/utilisateur` ou `cd ~`
* **Explication:** Ici aussi, nous utilisons un chemin absolu pour nous rendre directement au répertoire personnel.

4. Vous êtes dans le répertoire `/tmp`. Vous souhaitez accéder au répertoire `Téléchargements` qui se trouve dans votre répertoire personnel. Sachant que votre nom d'utilisateur est user1, quelle commande utiliserez vous ?
* **Réponse :** `cd /home/user1/Téléchargements`
* **Explication:** On utilise encore un chemin absolu pour se rendre au répertoire "Téléchargements" qui est situé dans le répertoire personnel de "user1".
 

---

### Commandes Linux Simples  

Exercice 2 : Commandes Linux simples
Date et heure : date (avec formatage 12 heures)
Affichage de contenu de fichier : head, tail
Utilisation de l’historique des commandes : history, navigation avec flèches du clavier

#### Contexte

Vous travaillez sur un serveur Linux et devez utiliser des commandes essentielles pour afficher l'heure, lire des fichiers et gérer l'historique des commandes. Répondez aux questions suivantes en expliquant les commandes appropriées.  

#### Questions 

1. **Quelle commande permet d’afficher la date et l’heure actuelles du système ?** *(Réponse courte)*  
2. **Comment afficher l’heure actuelle en format 12 heures avec AM/PM ?** *(Réponse courte)*  
3. **Quelle commande permet d’afficher les 10 premières lignes d’un fichier texte ?** *(Réponse courte)*  
4. **Quelle commande permet d’afficher les 15 dernières lignes d’un fichier texte ?** *(Réponse courte)*  
5. **Comment afficher en continu les nouvelles lignes ajoutées à un fichier journal `log.txt` ?** *(Réponse courte)*  
6. **Quelle commande permet d’afficher les 5 premières lignes du fichier `/var/log/syslog` ?** *(Réponse courte)*  
7. **Quelle commande permet de visualiser les 20 dernières lignes d’un fichier `/etc/passwd` ?** *(Réponse courte)*  
8. **Quelle commande permet d'afficher l'historique des commandes exécutées dans le terminal ?** *(Réponse courte)*  
9. **Quelle touche du clavier permet d’afficher rapidement la dernière commande exécutée ?** *(Réponse courte)*  
10. **Expliquez comment utiliser l’historique pour exécuter une commande sans la retaper.** *(Réponse longue)*  
11. **Quelle est la différence entre les commandes `head` et `tail` ? Donnez un exemple d'utilisation pour chaque.** *(Réponse longue)*  
12. **Comment utiliser les flèches du clavier pour naviguer dans l’historique des commandes ?** *(Réponse longue)*  
13. **Expliquez comment exécuter une commande utilisée précédemment en la retrouvant avec `history`.** *(Réponse longue)*  
14. **Quelle est l’utilité de la commande `!100` (où `100` est un numéro de commande) dans l’historique ?** *(Réponse longue)*  

---

### Commandes de Base sous Linux 

#### Contexte

Vous êtes un utilisateur Linux et devez gérer des fichiers et répertoires, afficher leur contenu et comprendre l’arborescence du système. Répondez aux questions suivantes en expliquant les commandes appropriées.  

#### Questions  

1. **Quelle commande permet de créer un répertoire nommé `projet` dans le répertoire courant ?** *(Réponse courte)*  
2. **Quelle commande permet de copier un fichier `notes.txt` dans le répertoire `backup` ?** *(Réponse courte)*  
3. **Quelle commande permet de déplacer le fichier `log.txt` vers le répertoire `/var/logs` ?** *(Réponse courte)*  
4. **Quelle commande permet de supprimer un répertoire `test` et tout son contenu ?** *(Réponse courte)*  
5. **Comment afficher le contenu du fichier `config.txt` dans le terminal ?** *(Réponse courte)*  
6. **Quelle commande permet d’éditer un fichier `document.txt` avec `vim` ?** *(Réponse courte)*  
7. **Quelle séquence de touches permet d’enregistrer et quitter un fichier sous `vim` ?** *(Réponse courte)*  
8. **Quelle option de `ls` permet d’afficher les détails des fichiers (permissions, taille, propriétaire) ?** *(Réponse courte)*  
9. **Quelle est la différence entre les répertoires `/bin` et `/sbin` ?** *(Réponse longue)*  
10. **Quelle est la fonction du répertoire `/proc` dans Linux ?** *(Réponse longue)*  
11. **Quel est le rôle du répertoire `/var/www` et dans quel cas est-il utilisé ?** *(Réponse longue)*  
12. **Quelle est la différence entre un chemin absolu et un chemin relatif ? Donnez un exemple pour chacun.** *(Réponse longue)*  
13. **Expliquez pourquoi un utilisateur standard ne peut pas créer un fichier dans `/root`.** *(Réponse longue)*  
14. **Comment l’utilisateur peut lister tous les fichiers, y compris les fichiers cachés, d’un répertoire `/home/user` ?** *(Réponse courte)*  
15. **Quelle commande permet d'afficher la structure d'un répertoire et de ses sous-répertoires de manière arborescente ?** *(Réponse courte)*  

---

## Semaine 3

### Gestion des Niveaux d’Exécution sous Linux  

Exercice 1 : Niveaux d'exécution
Gestion des niveaux d’exécution (runlevels) avec systemd :
systemctl get-default (vérifier le niveau d’exécution actuel)
systemctl set-default multi-user.target (passer en mode multi-utilisateurs sans interface graphique)
systemctl set-default graphical.target (rétablir l’interface graphique)
Redémarrage du système : shutdown -r now

#### Contexte

Vous êtes un administrateur système et devez configurer les niveaux d’exécution de votre machine Linux avec `systemd`. Répondez aux questions suivantes en expliquant les commandes appropriées.  

#### Questions 

1. **Quelle commande permet de vérifier le niveau d’exécution actuel du système ?** *(Réponse courte)*  
2. **Quelle commande permet de passer en mode multi-utilisateurs sans interface graphique ?** *(Réponse courte)*  
3. **Quelle commande permet de restaurer l’interface graphique comme niveau d’exécution par défaut ?** *(Réponse courte)*  
4. **Quelle commande permet de redémarrer immédiatement le système ?** *(Réponse courte)*  
5. **Quelle est la différence entre `multi-user.target` et `graphical.target` ?** *(Réponse longue)*  
6. **Pourquoi un administrateur système pourrait vouloir désactiver l’interface graphique sur un serveur Linux ?** *(Réponse longue)*  
7. **Comment annuler un redémarrage programmé avec `shutdown` ?** *(Réponse courte)*  
8. **Expliquez la différence entre `shutdown -r now` et `reboot`.** *(Réponse longue)*  
9. **Quelle commande permettrait d’éteindre complètement le système après une minute ?** *(Réponse courte)*  
10. **Que se passe-t-il si vous exécutez `systemctl set-default multi-user.target` sans redémarrer ?** *(Réponse longue)*  

---

### Recherche de fichiers avec `find` et caractères génériques

Exercice 2 : Caractères génériques et commande find
Recherche de fichiers avec find :
find . -name "r*" (fichiers commençant par "r")
find . -name "*rc*" (fichiers contenant "rc")
find / -type f -name "???" (fichiers avec exactement trois caractères dans le nom)
Utilisation des caractères génériques (*, ?) dans la recherche de fichiers

#### Contexte  
Vous devez rechercher des fichiers spécifiques sur un système Linux en utilisant la commande `find` et les caractères génériques. Répondez aux questions suivantes en expliquant les commandes appropriées.  

#### Questions

1. **Quelle commande permet de rechercher tous les fichiers du répertoire courant dont le nom commence par la lettre "r" ?** *(Réponse courte)*  
2. **Quelle commande permet de rechercher dans le répertoire courant tous les fichiers contenant la chaîne "rc" dans leur nom ?** *(Réponse courte)*  
3. **Quelle commande permet de rechercher dans tout le système les fichiers dont le nom comporte exactement trois caractères ?** *(Réponse courte)*  
4. **Quelle option de la commande `find` permet de rechercher uniquement des répertoires au lieu de fichiers ?** *(Réponse courte)*  
5. **Quelle est la différence entre les caractères génériques `*` et `?` dans la recherche de fichiers ? Donnez un exemple d’utilisation pour chaque.** *(Réponse longue)*  
6. **Pourquoi l’exécution de `find / -name "*.conf"` peut nécessiter des privilèges root ?** *(Réponse longue)*  
7. **Comment rechercher tous les fichiers `.log` dans le répertoire `/var/logs` ?** *(Réponse courte)*  
8. **Quelle commande permet de rechercher les fichiers vides dans le répertoire `/home/user` ?** *(Réponse courte)*  
9. **Comment modifier la commande `find` pour rechercher uniquement les fichiers modifiés au cours des 7 derniers jours ?** *(Réponse longue)*  
10. **Expliquez pourquoi l’utilisation de `find / -type f -name "r*"` peut être longue et comment l’optimiser.** *(Réponse longue)*  

---

### Expansion d’Accolades et Boucle `for` sous Linux

Exercice 3 : Expansion d'accolades et boucle for
Création d’arborescence avec mkdir et expansion d’accolades :
mkdir -p semaine{1..4}/{lab,lecon} (création de l’arborescence)
Création de fichiers avec touch et expansion d’accolades :
touch semaine{1..4}/lab/priseNote (création des fichiers)
Boucle for pour renommer des fichiers :
for file in semaine{1..4}/lab/priseNote; do mv "$file" "$file.txt"; done
Boucle for pour déplacer des fichiers :
for i in {1..4}; do mv semaine$i/lab/priseNote.txt semaine$i/lecon/; done
Vérification de l’arborescence avec tree

#### Contexte 
Vous devez automatiser la création et la gestion de fichiers et répertoires sous Linux en utilisant l’expansion d’accolades et les boucles `for`. Répondez aux questions suivantes en expliquant les commandes appropriées.  

### Questions 

1. **Quelle commande permet de créer les répertoires `semaine1`, `semaine2`, `semaine3`, et `semaine4` avec les sous-dossiers `lab` et `lecon` en une seule ligne ?** *(Réponse courte)*  
2. **Quelle commande permet de créer un fichier `priseNote` dans chaque répertoire `lab` des semaines 1 à 4 en une seule ligne ?** *(Réponse courte)*  
3. **Comment renommer tous les fichiers `priseNote` en `priseNote.txt` dans les répertoires `lab` des semaines 1 à 4 à l’aide d’une boucle `for` ?** *(Réponse courte)*  
4. **Quelle commande permet de déplacer tous les fichiers `priseNote.txt` des répertoires `lab` vers les répertoires `lecon` correspondants en utilisant une boucle `for` ?** *(Réponse courte)*  
5. **Pourquoi utilise-t-on les accolades `{}` dans les commandes `mkdir` et `touch` pour créer plusieurs fichiers et répertoires à la fois ?** *(Réponse longue)*  
6. **Expliquez ce que fait la commande `tree` et comment elle peut être utilisée pour vérifier la structure d’un répertoire.** *(Réponse longue)*  
7. **Que se passe-t-il si un fichier `priseNote` existe déjà avant d’exécuter la boucle `for` de renommage ? Comment éviter d’écraser un fichier existant ?** *(Réponse longue)*  
8. **Comment modifier la boucle `for` de déplacement des fichiers `priseNote.txt` pour s’assurer qu’elle affiche un message après chaque déplacement réussi ?** *(Réponse longue)*  
9. **Quelle est la différence entre les commandes `mv` et `cp` lorsqu’on les utilise dans une boucle `for` ?** *(Réponse longue)*  
10. **Quelle commande unique pourrait-on utiliser pour lister uniquement les fichiers `priseNote.txt` situés dans tous les répertoires `lecon` ?** *(Réponse courte)*  


