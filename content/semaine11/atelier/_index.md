+++
title = "ATELIER #10b: Gestion des droits d’accès aux fichiers"
weight = 112
+++

## Objectif de l'atelier

Cet exercice vise à vous familiariser avec les commandes pour la configuration des droits d'accès aux fichiers. 

---

# Atelier

{{% notice style="note" title="Prérequis" %}}
L'atelier #10a doit être fait pour pouvoir faire celui-ci.
{{% /notice %}}

## Remise

- Vous devez faire une/des captures d’écran pour chaque commande que vous tapez pour répondre à la question. 
- Lorsqu'une question est posée, écrivez la réponse dans le Terminal Ou dans un fichier texte.

## Exercice : Gestion des droits d’accès aux fichiers

1. **Connexion avec l’utilisateur didi :**
   - Connectez-vous en tant que **didi** avec la commande suivante :
     ```bash
     su - didi
     ```

2. **Gestion des permissions de fichier :**
   - **didi** crée un fichier nommé **fichierCommun.txt**.
   - Donnez la commande permettant à **fifi** de rejoindre le groupe propriétaire de ce fichier.
   - Utilisez la méthode symbolique pour donner les droits de lecture et d’écriture au groupe propriétaire.

3. **Vérification des droits :**
    - Affichez les droits de **fichierCommun.txt** pour vérifier les permissions accordées.

4. **Modification des droits avec deux méthodes :**
    - On souhaite que :
      - Le propriétaire ait tous les droits.
      - Le groupe propriétaire ait uniquement les droits de lecture.
      - Les autres utilisateurs n’aient aucun droit.
    - Effectuez cette modification avec :
      - La méthode symbolique.
      - La méthode octale.

5. **Vérification finale des droits :**
    - Affichez les droits de **fichierCommun.txt** pour confirmer les modifications.

6. **Reconnexion à votre compte habituel :**
    - Utilisez la commande suivante pour revenir à votre compte :
      ```bash
      su - votreLogin
      ```