+++
title = "Grilles de correction"
weight = 1791
draft = true
+++

## **Exercice 1** : Manipulation de valeurs numériques

| Critères d’évaluation                                 | Excellent (5)              | Satisfaisant (3)         | Insuffisant (0)          |
|-------------------------------------------------------|----------------------------|--------------------------|--------------------------|
| **Test sur le nombre de paramètres**                  | Validation correcte avec message d’erreur approprié en cas d’absence. | Validation partielle ou imprécise. | Pas de vérification effectuée. |
| **Détermination du plus grand et du plus petit**      | Détermination précise avec prise en compte des valeurs égales. | Comparaison correcte mais simpliste. | Comparaison incorrecte ou manquante. |
| **Utilisation des variables $1, $2 et $3 (1er cas)** <br> --- <br> **Utilisation de variables pour stocker les entrées (2e cas)** | Utilisation correcte et efficace des paramètres positionnels. <br> --- <br> Utilisation de trois variables locales nommées correctement.| Utilisation partielle ou incorrecte. <br> --- <br> Utilisation de variables mais sans clarté. | Paramètres non utilisés ou mal manipulés. <br> --- <br> Variables non utilisées ou mal nommées. |
| **Calcul avec `let`**                                  | Calcul effectué correctement avec `let` dans les deux cas. | Utilisation correcte mais syntaxe perfectible. | Calcul incorrect ou usage de `let` absent. |
| **Respect de l’affichage**                           | Affichage conforme au format demandé avec mise en forme soignée. | Affichage correct mais imprécis ou incomplet. | Affichage incorrect ou absent. |
| **Résultat final attendu**                           | Résultat précis. | Résultat correct mais manque de précision. | Résultat incorrect ou non affiché. |

**Total des points : /30** 

---

## **Exercice 2** : Tests sur les fichiers 

| Critères d'évaluation                                     | Points attribués    | 
|-----------------------------------------------------------|:-------------------:|
| **1. Vérification du type de fichier**                    |                     |                
| - Utilisation de `-f` pour vérifier si c’est un fichier standard   | **2**      |          
| - Message affiché correctement si c'est un fichier standard        | **1**      |               
| - Message affiché correctement si ce n’est pas un fichier standard | **1**      |        
| **2. Vérification des droits d'accès**                    |                     |                 
| - Utilisation de `-r` pour vérifier les droits de lecture | **2**               |                 
| - Message affiché correctement pour la lecture            | **1**               |                 
| - Utilisation de `-w` pour vérifier les droits d’écriture | **2**               |                 
| - Message affiché correctement pour l’écriture            | **1**               |                 
| - Utilisation de `-x` pour vérifier les droits d’exécution| **2**               |                
| - Message affiché correctement pour l’exécution           | **1**               |                 
| **3. Qualité du script**                                  |                     |                  
| - Script fonctionne correctement dans tous les cas (fichier absent, fichier non standard, etc.) | **2**  |  
| **Total**                                                 | **15**              |                  

---

## **Exercice 3** : Partie 1 (calcul.sh)   

Voici la grille de correction remaniée avec trois niveaux :  

| **Critères**   | **Excellent (5 pts)**  | **Satisfaisant (3 pts)**    | **Insuffisant (0 pt)**     |
|----------------|------------------------|-----------------------------|----------------------------|
| **Utilisation des variables de paramètres $1, $2 et $3**  | Utilisation correcte et complète des variables de paramètres | Utilisation partielle ou comportant des erreurs mineures  | Absence d’utilisation ou utilisation incorrecte des variables  |
| **Vérification du nombre de paramètres avec message d'erreur et exit 1** | Vérification complète avec message d’erreur clair et exit 1 | Vérification partielle ou gestion d’erreur incomplète | Aucune vérification des paramètres | **Utilisation de let pour les calculs**                                                       | Utilisation complète et correcte de `let` pour les calculs | Utilisation de `let` avec erreurs mineures ou omissions | Aucune utilisation de `let` ou utilisation incorrecte |
| **Traitement des opérateurs +, - et ^** | Tous les opérateurs gérés correctement avec un comportement attendu | Un opérateur mal géré ou gestion partiellement incorrecte | Plusieurs opérateurs mal gérés ou gestion inexistante |
| **Affichage du résultat** | Affichage précis et conforme au format demandé | Affichage avec un format légèrement incorrect ou incomplet | Aucun affichage ou résultat incorrect |

**Total des points : /25** 


## **Exercice 3** : Partie 2 (calculV2.sh)   

| **Critères**  | **Excellent (6 pts)**   | **Passable (3 pts)**   | **Insuffisant (0 pt)**                                                                                                                      |
|---------------|-------------------------|--------------------|----------------------|
| **Structure générale du script** | Le script est bien organisé, clair et respecte les bonnes pratiques de script Bash.  | Le script est fonctionnel et bien structuré, avec quelques améliorations possibles. | Le script est désorganisé, difficile à lire ou ne fonctionne pas correctement. |
| **Vérification du nombre de paramètres**   | La vérification du nombre de paramètres se fait correctement. | La vérification est logique mais mal structurée. | Absence de vérification ou vérification incorrecte. |
| **Saisie des valeurs en cas de paramètres insuffisants** | La saisie des valeurs manquantes est demandée avec un message explicite et convivial. | La saisie fonctionne mais le message manque de clarté ou de convivialité. | La saisie ne fonctionne pas ou n’est pas implémentée. |
| **Calcul et affichage du résultat** | Le calcul s'effectue correctement avec `let` | Le calcul fonctionne mais pas fait avec `let`. | Le calcul échoue ou donne des résultats incorrects. |


**Total des points : /30** 
