+++
title = "ATELIER #3: Le système de fichiers et les commandes de base"
weight = 32
+++

## Objectif de l'atelier

Cet atelier a pour but de vous familiariser avec les commandes de base pour la gestion des fichiers sous Linux en utilisant la distribution **AlmaLinux** sur votre VM. 
Ces exercices pratiques permettront de renforcer la compréhension et l'utilisation de ces commandes.

# Atelier

## Attention:

Avant de commencer chaque exercice, assurez vous que vous travaillez dans votre répertoire personnel et ne vous déplacez pas que lorsque demandé.

{{% notice style=warning title=Attention %}}
1. À moins d'indication contraire, utiliser TOUJOURS des chemins relatifs.
2. Les questions qui demandent des réponses textuelles, écrivez-les dans un fichier afin de pouvoir les vérifier avec la solution qui vous sera fournie ultérieurement.
{{% /notice %}} 

## Exercice 1 : Explorer l’arborescence Linux

1. Afficher le chemin de votre répertoire courant. 
2. Allez dans le répertoire `/usr/share/doc`, puis vérifiez le chemin de votre répertoire courant.
3. Remontez dans le répertoire parent.
4. Allez dans votre répertoire personnel.
5. Listez les fichiers présents du répertoire courant.
6. Toujours en étant dans votre dossier personnel, listez les fichiers du répertoire `/usr`


## Exercice 2: Commandes de base

### Préparation

Sur votre machine Almalinux, avec votre utilisateur standard, allez sur votre cours sur Moodle, dans la semaine 3. On vous demande de télécharger ce fichier.

![HTTP](atelier3-1.png?height=50)

1. Cliquez sur fichier1. 

![HTTP](atelier3-2.png?height=200)

2. Sur la fenêtre qui s'ouvre, faites un clic droit et choisissez Enregistrez-sous.

![HTTP](atelier3-3.png?height=200)

- Le fichier va être enregistré par défaut dans le dossier **Téléchargements**.

![HTTP](atelier3-4.png?height=300)

3. Fermer la fenêtre.

4. Cliquez sur le bouton Activités sur le bureau.

![HTTP](atelier3-5.png?height=300)

5. Cliquer sur l’icône **Fichiers**.

![HTTP](atelier3-6.png?height=300)

### Commandes

Allez maintenant sur votre terminal. Placez-vous dans votre répertoire personnel et déplacez-vous seulement si c'est demandé. 

1. Créer un répertoire `Atelier2` dans le répertoire courant.
2. Copier le fichier téléchargé `fichier1.txt` dans le répertoire `Atelier2`.
3. Créer un autre répertoire nommé `Rep2`.
4. Déplacer `Atelier2` dans `Rep2`.
5. Déplacez-vous dans `Atelier2`.
6. Via l'interface d'Almalinux, ouvrir le fichier `fichier1.txt` et écrivez votre nom complet dans le fichier. Enregistrer la modification et fermer le fichier.
7. Afficher le contenu du fichier à l’aide de la commande `cat`.
8. Créer un autre fichier nommé `fichier2.txt` dans `Atelier2`. 
9. Avec une seule commande `cat` afficher le contenu de `fichier1.txt` et `fichier2.txt`.
10. Revenir dans votre répertoire personnel.
11. Supprimer le répertoire `Rep2`.
12. Dans quel répertoire vous trouvez-vous? Utiliser une commande pour voir le répertoire courant.
13. Créer un dossier avec le nom `Rep3` dans le dossier `/root`(**en utilisant un chemin absolu**). Avez-vous réussi ? Si non, pourquoi ? 
14. Afficher le contenu du répertoire `/etc` en utilisant l’option `-l`.
15. Par quels caractères, les lignes affichées débutent ? Quelles est leur signification ?
16. Qu’est-ce qui distingue le répertoire `/proc` des autres répertoires de l’arborescence linux ? 
17. Qu’est ce qui distingue le répertoire <code class="gr">/bin</code> et <code class="gr">/sbin</code> ?
18. Quel est le répertoire qui est utilisé pour charger le noyau du système d’exploitation au démarrage ? 
19. Dans Linux, tout est fichier. Si on connecte une clé usb à une machine linux, dans quel répertoire de l’arborescence, on va trouver la référence à cette clé ?
20. Si on installe un serveur web apache sur une machine linux, dans quel répertoire de l’arborescence le dossier contenant les fichiers de configuration du serveur se trouvera-t-il ?

