+++
title = "CRON et DNF"
weight = 81
+++


## Planification des tâches avec **cron**

**Cron** est un outil qui permet de planifier et d'automatiser des tâches sur un système Linux. Chaque utilisateur peut définir ses propres tâches planifiées.

### Points essentiels : 
 
- Les tâches planifiées par un utilisateur sont stockées dans le fichier :  
  `/var/spool/cron/<user>`  
- Le démon responsable de l'exécution des tâches planifiées s'appelle : **crond**  
- On peut planifier des tâches complexes grâce aux nombreuses options disponibles.  


## Commandes de base pour gérer les tâches planifiées

1. **Afficher la liste des tâches planifiées** :  
   ```bash
   crontab -l
   ```

2. **Supprimer toutes les tâches planifiées** :  
   ```bash
   crontab -r
   ```

3. **Modifier les tâches d’un autre utilisateur (nécessite les droits root)** :  
   ```bash
   crontab -u <utilisateur>
   ```

4. **Importer un fichier contenant des tâches planifiées** :  
   ```bash
   crontab <fichier>
   ```
   > ⚠️ Chaque import écrase toutes les tâches existantes.

5. **Modifier ou créer des tâches** (commande la plus courante) :  
   ```bash
   crontab -e
   ```

## Syntaxe d’une tâche **cron**

Une tâche dans une crontab se compose de deux parties :  
1. **La planification** : Décrit quand la tâche doit s’exécuter (5 champs).  
2. **La commande ou script à exécuter** :  
   - Peut être une commande bash.  
   - Recommandation : utilisez un script, spécifié avec son **chemin absolu**.

**Exemple d’une crontab** :  
```bash
15 * * * * bash /home/user/monscript.sh
30 0 * * * bash /usr/local/bin/autrescript.sh
0 * * * * echo "Nouvelle heure" >> /home/user/heure.txt
```

Les erreurs de syntaxe dans le fichier crontab sont détectées au moment de l’enregistrement. Si une tâche génère des erreurs lors de l'exécution, elles sont enregistrées dans :  
`/var/mail/<user>`  


## Comprendre la planification

La planification utilise 5 champs :  

|  Minutes  |  Heures  | Jour du mois  |  Mois  |  Jour de la semaine  |
|:---:|:---:|:---:|:---:|:---:|
| 0-59 | 0-23 | 1-31 | 1-12 | 0-7 *(dimanche à dimanche)* |

### Symboles utiles

- **`*`** : Tous les moments possibles (ex. : toutes les heures).  
- **`,`** : Énumération de valeurs (ex. : `1,5,6`).  
- **`-`** : Intervalle de valeurs (ex. : `1-10`).  
- **`*/n`** : Sauts réguliers (ex. : `*/2` toutes les 2 heures).  

### Exemples de planifications
 
- **Tous les jours à 14h30** :  
  ```bash
  30 14 * * * bash /chemin/script.sh
  ```
- **Chaque heure (25ème minute) en mars uniquement** :  
  ```bash
  25 * * 3 * bash /chemin/script.sh
  ```
- **Lundi, mercredi et vendredi à midi** :  
  ```bash
  0 12 * * 1,3,5 bash /chemin/script.sh
  ```

## Gestion des paquets avec **dnf**

**DNF** est un gestionnaire de paquets pour les systèmes basés sur Red Hat (comme AlmaLinux). Il simplifie :  
- L’installation.  
- La mise à jour.  
- La suppression de logiciels.  

Contrairement à l’installation manuelle ou avec des fichiers RPM, **dnf** gère automatiquement les dépendances.

### Commandes de base

#### Rechercher un paquet

- Rechercher un paquet par nom ou description :  
  ```bash
  dnf search <mot-clé>
  ```
  
- Vérifier si un fichier ou commande fait partie d’un paquet :  
  ```bash
  dnf provides <fichier/commande>
  ```

#### Installation d’un paquet

Pour installer un paquet :  
```bash
sudo dnf install <nom_du_paquet>
```

#### Mettre à jour un paquet ou tout le système

- Mettre à jour un paquet spécifique :  
  ```bash
  sudo dnf update <nom_du_paquet>
  ```
- Mettre à jour tous les paquets installés :  
  ```bash
  sudo dnf update
  ```

#### Supprimer un paquet

Pour désinstaller un paquet :  
```bash
sudo dnf remove <nom_du_paquet>
```

### Gestion des dépôts

Les dépôts sont des serveurs qui contiennent des paquets. Ils sont configurés dans :  
`/etc/yum.repos.d`

#### Commandes utiles
 
1. **Lister les dépôts actifs** :  
   ```bash
   dnf repolist
   ```
2. **Lister tous les dépôts (actifs ou non)** :  
   ```bash
   dnf repolist all
   ```

#### Ajouter un nouveau dépôt

Par exemple, pour ajouter le dépôt **remi** :  
```bash
sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
```

### Gestion des groupes de paquets

Certaines applications ou environnements sont regroupés en groupes pour simplifier leur gestion.

#### Commandes importantes
 
1. **Lister les groupes disponibles** :  
   ```bash
   dnf grouplist
   ```

2. **Installer un groupe** :  
   Exemple pour installer l’environnement **Xfce** :  
   ```bash
   sudo dnf groupinstall "Xfce"
   ```

3. **Obtenir des informations sur un groupe** :  
   ```bash
   dnf groupinfo "<nom_du_groupe>"
   ```

### Automatisation avec le shell **dnf**

Le shell **dnf** permet d’exécuter plusieurs commandes à la suite.  

1. **Créer un fichier avec les commandes** (ex. : `installations.txt`) :  
   ```bash
   install nmap
   install zsh
   run
   ```

2. **Exécuter le fichier avec dnf** :  
   ```bash
   dnf shell installations.txt
   ```




