+++
title = "Test 2"
weight = 172
draft = true
+++

## Critères de correction appliqués

Étant donné que vous aviez droit à une feuille de note, la correction est sévère au niveau de la syntaxe et du rôle des commandes.

| Erreur                            | Pénalité (%)  | Exemple                           |  
|-----------------------------------|:-------------:|-----------------------------------|
| Ne répond pas à la question       | -100%         | `cd ../../home/user` qui retourne à `var` au lieu de `cd ~`     |
| Syntaxe de base erronée           | -100%         | Inversion commande et chemin (`/home/user ls` au lieu de `ls /home/user`) | 
| Mauvaise commande                 | -100%         | `find` au lieu de `ls` <br> `cat` au lieu de `echo` <br> `mkdir` au lieu de `touch` |
| Commande absente                  | -100%         | Action attendue non écrite.       |
| Option manquante                  | -75%          | `mkdir` au lieu de `mkdir -p`     |  
| Mauvaise commande (si complexe) <br> mais bon chemin/structure | -50%          | `mv backup_20{00...25}.tar /mnt/archives/` au lieu de `cp backup_20{00...25}.tar /mnt/archives/` <br> `ls /home/user/scripts/*.sh` au lieu de `find /home/user/scripts/ -name "*.sh"` |           
| Commande pas optimale             | -50%          | `tail -n 10` au lieu de `tail`; <br> utilisation de `{2000,2001,2002,...}` au lieu de `{2000..2025}` <br> `ls *.log *.txt *.csv` au lieu de `ls *.{log,txt,csv}` |
| Commande de trop                  | -25%          | `history !sudo` au lieu de `!sudo` |
| --------------------------------- | ------------- | ---------------------------------- |    
| Erreur majeure pour le chemin     | -100%         | Commence par `/`, mais fausse le chemin <br> ou dans une boucle `for`, le mauvaise chemin |  
| Extension manquante               | -75%          | `rapport2025` au lieu de `rapport2025.txt`     |     
| Chemin non optimal                | -50%          | Utiliser un chemin absolu inutilement, ou `../` inutilement | 
| Erreur mineure vs énoncé          | -25%          | Nombres impairs `{1,3,5,7,9}` au lieu de pairs `{2,4,6,8,10}` |


## Rappels des notions de base importantes non réussies

1. **Notion**
