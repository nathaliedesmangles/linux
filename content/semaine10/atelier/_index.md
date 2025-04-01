+++
title = "ATELIER #10a: Utilisateurs et groupes"
weight = 102
+++

## Objectif de l'atelier

- Cet atelier vise à vous familiariser avec les commandes de gestion des utilisateurs et des groupes sous Linux.
---

# Atelier

## Remise

- Vous devez faire une/des captures d’écran pour chaque commande que vous tapez pour répondre à la question. 
- Lorsqu'une question est posée, écrivez la réponse dans le Terminal Ou dans un fichier texte.

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
   - Définissez un mot de passe pour **fifi** et **didi**.

5. **Modification du shell :**
   - Affichez la liste des shells disponibles sur votre système.
   - Modifiez le shell par défaut de **didi** avec un autre shell de votre choix.

6. **Affichage des informations utilisateurs :**
   - Affichez les informations de **fifi** et **didi** à partir du fichier **/etc/passwd**.
   - Utilisez la commande `id` pour afficher les détails de **fifi** et **didi**.

7. **Groupes primaires et secondaires :**
   - Quels sont les groupes primaires et secondaires de **fifi** et **didi** ?


