+++
title = "ATELIER #4: Le processus de démarrage et le BASH"
weight = 42
+++

## Objectif de l'atelier

Cet atelier a pour but de vous familiariser avec les cibles (niveaux d'exécution) sous Linux. 


# Atelier

## Exercice 1 : Changer de cible

Dans cet exercice, vous allez passer du mode graphique au mode multi-utilisateur sans interface graphique:

   - Utiliser la commande suivante pour passer en mode multi-utilisateur sans interface graphique :
     ```bash
     systemctl isolate <cible>
     ```
   - Vérifier que vous êtes maintenant en mode multi-utilisateur sans interface graphique.

## Exercice 2 : Définir la cible par défaut

Dans cet exercice, vous allez définir le mode multi-utilisateur avec interface graphique comme cible par défaut.

   - Utiliser la commande suivante pour définir la cible par défaut :
     ```bash
     systemctl set-default <cible>
     ```
   - Redémarrer votre système pour vérifier que le mode graphique est bien la cible par défaut.

## Exercice 3 : Activer et désactiver des services

Dans cet exercice, on vous demande d'activer et désactiver des services au démarrage.

   - Utiliser la commande suivante pour activer un service au démarrage (par exemple, `httpd` pour le serveur web Apache) :
     ```bash
     systemctl enable <service>
     ```
   - Utiliser la commande suivante pour désactiver un service au démarrage :
     ```bash
     systemctl disable <service>
     ```

## Exercice 4 : Vérifier l'état des cibles

Dans cet exercice, vous devrez vérifier l'état actuel des cibles et des services.

   - Utiliser la commande suivante pour vérifier l'état actuel de la cible :
     ```bash
     systemctl <completer>
     ```
   - Utiliser la commande suivante pour vérifier l'état d'un service spécifique (par exemple, `httpd`) :
     ```bash
     systemctl status <service>
     ```

## Exercice 5 : Redémarrer et arrêter le système

Cet exercice vous demande de redémarrer et d'arrêter le système en utilisant systemd.

   - Utiliser la commande suivante pour redémarrer le système :
     ```bash
     systemctl <cible>
     ```
   - Utiliser la commande suivante pour arrêter le système :
     ```bash
     systemctl <cible>
     ```