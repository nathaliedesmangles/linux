+++
title = "ATELIER #10a: Utilisateurs et groupes"
weight = 102
+++

## Objectif de l'atelier

- Cet atelier vise à vous familiariser avec les commandes de gestion des utilisateurs et des groupes sous Linux.
---

# Atelier

## Remise

- Vous devez faire des **captures d’écran** pour les commandes que vous tapez pour répondre à la question. 
{{% notice style="red" title="Attention" %}}
Montrez votre **rigueur/professionnalisme** et nommez vos captures d'écran de façon à savoir à quelle question elle se rapporte. Un non respect entrainera la **note de 0** pour la question.
{{% /notice %}}
- Lorsqu'une question est posée, écrivez la réponse dans le **Terminal** ou dans un **fichier texte**, en indiquant **clairement** le numéro de la question.

## Exercice : Création et gestion des utilisateurs

1. **Informations sur les utilisateurs :**
   - Quels sont les deux fichiers qui contiennent les informations sur les utilisateurs, y compris le login, l’UID, le mot de passe crypté et le chemin du répertoire personnel ?

2. **Création de groupes :**
   - Créez deux groupes nommés **dev** et **finance**.
   
3. **Création de comptes utilisateurs :**
   - Créez deux utilisateurs : **fifi** et **didi**.
     - Le groupe principal de **fifi** doit être **finance**.
     - Le groupe principal de **didi** doit être **dev**.
     - Ajoutez un commentaire pour **didi** indiquant "Développeur" et pour **fifi** "Financier".

4. **Changement de mot de passe :**
   - Définissez un mot de passe pour **fifi** et **didi**. Par exemple `pwdfifi` et `pwddidi` respectivement.

5. **Modification du shell :**
   - Affichez la liste des shells disponibles sur votre système (Hint: [Voir cours semaine #2](https://linuxh25.netlify.app/semaine2/cours/#comment-afficher-la-liste-des-shells-disponibles-le-système-).
   - Modifiez le shell par défaut de **didi** avec un autre shell de votre choix.

6. **Affichage des informations utilisateurs :**
   - Affichez les informations de **fifi** et **didi** à partir du fichier **/etc/passwd**.
   - Utilisez la commande `id` pour afficher les détails de **fifi** et **didi**.

7. **Groupes primaires et secondaires :**
   - Quels sont les groupes primaires et secondaires de **fifi** et **didi** ?


