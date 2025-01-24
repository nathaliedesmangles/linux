 
+++
title = "ATELIER #2: Commandes Linux de base"
weight = 22
+++

## Objectifs de l'atelier

- Se familiariser avec la ligne de commandes.
- Naviguer dans l'arborescence Linux à l'aide de commandes.
- Gerer des fichiers et répertoires à l'aide de commandes.

## Format de la remise sur Moodle

{{% notice style="warning" title="Attention" %}}
- Pour chaque exercice, vous devrez prendre une **capture d'écran**. Sur les captures, on doit pouvoir voir :
  1. Votre nom d'utilisateur (Ne travaillez donc **pas** avec l'utilisateur `root`, ni la commande `sudo`).
  2. La ligne de commande et la commande.
  3. Le résultat de la commande. Si le résultat fait plus de 10 lignes, capturer juste les 10 premières lignes.
  4. Nommer les fichiers image, tel qu'indiqué pour chaque question.
  5. Remettre toutes vos images dans **1 seul fichier compressé (ex:.zip)**. 
	**Tout autre format ne sera pas corrigé**.
- Pour l'exercice #3, quelques questions devront ètre répondues dans un fichier texte à remettre sur Moodle en plus du .zip.
{{% /notice %}}

---

# Atelier

### Préparation

Sur votre machine Almalinux, avec votre utilisateur standard, allez sur votre cours sur Moodle, dans la semaine 2. On vous demande de télécharger le fichier **fichier.txt**. Vous en aurez besoin pour l'exercice #3.

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

{{% notice style="warning" title="Attention" %}}
1. Avant de commencer chaque exercice, assurez vous que vous travaillez dans votre répertoire personnel et ne vous déplacez pas que lorsque demandé.
2. À moins d'indication contraire, utiliser **TOUJOURS des chemins relatifs**.
{{% /notice %}}

Allez maintenant sur votre terminal. Placez-vous dans votre répertoire personnel. 

## Exercice 1 : Explorer l’arborescence Linux

1. Afficher le chemin de votre répertoire courant. Prendre une capture d'écran et nommez-la `1-1.png`.
2. Allez dans le répertoire `/usr/share/doc`, puis vérifiez le chemin de votre répertoire courant. Prendre une capture d'écran et nommez-la `1-2.png`.
3. Remontez dans le répertoire parent. Prendre une capture d'écran et nommez-la `1-3.png`.
4. Allez dans votre répertoire personnel. Prendre une capture d'écran et nommez-la `1-4.png`.
5. Listez les fichiers présents du répertoire courant. Prendre une capture d'écran et nommez-la `1-5.png`.
6. Toujours en étant dans votre dossier personnel, listez les fichiers du répertoire `/usr`. Prendre une capture d'écran et nommez-la `1-6.png`.

## Exercice 2: Commandes Linux simples

1. **Commande `date`**
   - Afficher la date et l'heure actuelles du système.
   - Afficher l’heure actuelle sur une horloge de douze heures (par exemple, 11:42:11 AM). 
   - Prendre une capture d'écran et nommez-la `2-1.png`.

2. **Commande `head`**
   - Affichez les 10 premières lignes du fichier /etc/services
   - Prendre une capture d'écran et nommez-la `2-2.png`.

3. **Commande `tail`**
   - Affichez les 10 dernières lignes du fichier /etc/services.
   - Prendre une capture d'écran et nommez-la `2-3.png`.

4. **Commande `tail` et la flèche vers le haut**
   - Répéter la commande précédente avec exactement trois frappes de touches.
   - Prendre une capture d'écran et nommez-la `2-4.png`.

5. **Commande `tail` et les flèches vers le haut et vers la gauche**
   - Répéter la commande précédente, mais afficher les 20 dernières lignes du fichier.
   - Prendre une capture d'écran et nommez-la `2-5.png`.

6. **Commande `history`**
   - Utiliser l’historique du shell pour exécuter à nouveau la commande effectuée pour la question #3 (heure sur 12h)
   - Prendre une capture d'écran et nommez-la `2-6.png`.

## Exercice 3: Commandes de base

{{% notice style="caution" title="Important" %}}
- Utilisez pas l'interface graphique d'Almalinux QUE LORSQUE demandé (#6). Autrement, utilisez uniquement des commandes pour répondre aux questions.
- Après chaque question (**sauf** #6, #12a, #15 à #20), n'oubliez pas de prendre une capture d'écran et de la nommer `3-X.png` où `X` est le numéro de la question.
{{% /notice %}}

1. Créer un répertoire `Atelier2` dans le répertoire courant.
2. Copier le fichier téléchargé `fichier.txt` dans le répertoire `Atelier2`.
3. Créer un autre répertoire nommé `Rep2`.
4. Déplacer `Atelier2` dans `Rep2`.
5. Déplacez-vous dans `Atelier2`.
6. Avec vim, ouvrez le fichier `fichier.txt` et écrivez écrivez votre nom complet dans le fichier. Enregistrer la modification et fermer le fichier.
7. Afficher le contenu du fichier à l’aide de la commande `cat`.
8. Créer un autre fichier nommé `fichier2.txt` dans `Atelier2`. 
9. Avec une seule commande `cat` afficher le contenu de `fichier.txt` et `fichier2.txt`.
10. Revenir dans votre répertoire personnel.
11. Supprimer le répertoire `Rep2`.
12. a) Dans quel répertoire vous trouvez-vous? b) Utiliser une commande pour voir le répertoire courant.
13. Créer un dossier avec le nom `Rep3` dans le dossier `/root`(**en utilisant un chemin absolu**). Avez-vous réussi ? Si non, pourquoi ? 
14. Afficher le contenu du répertoire `/etc` en utilisant l’option `-l`.
15. Par quels caractères, les lignes affichées débutent ? Quelles est leur signification ?
16. Qu’est-ce qui distingue le répertoire `/proc` des autres répertoires de l’arborescence linux ? 
17. Qu’est ce qui distingue le répertoire `/bin` et `/sbin` ?
18. Quel est le répertoire qui est utilisé pour charger le noyau du système d’exploitation au démarrage ? 
19. Dans Linux, tout est fichier. Si on connecte une clé usb à une machine linux, dans quel répertoire de l’arborescence, on va trouver la référence à cette clé ?
20. Si on installe un serveur web apache sur une machine linux, dans quel répertoire de l’arborescence le dossier contenant les fichiers de configuration du serveur se trouvera-t-il ?



