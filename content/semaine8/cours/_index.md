+++
title = "CRON et DNF"
weight = 81
+++

## Planification des tâches avec *Cron*

Le programme **cron** permet de planifier des tâches automatiquement sur un système Linux. Chaque utilisateur peut définir ses propres tâches planifiées, qui sont stockées par défaut dans :

```
/var/spool/cron/<user>
```

Il est possible d'utiliser un fichier personnalisé pour la planification. Le ***deamon*** responsable de l'exécution des tâches est **crond**.

{{% notice style="info" title="Qu'est-ce qu'un Deamon ?" %}}
Un ***deamon*** est un type de programme informatique, un processus ou un ensemble de processus qui s'exécute en **arrière-plan** plutôt que sous le contrôle direct d'un utilisateur.
{{% /notice %}}


### Commandes principales

#### Afficher les tâches planifiées
```bash
crontab -l
```

#### Supprimer toutes les tâches planifiées
```bash
crontab -r
```

#### Gérer la crontab d'un autre utilisateur (nécessite d'être *root*)
```bash
sudo crontab -u <utilisateur>
```

#### Enregistrer un fichier de tâches planifiées dans la crontab
```bash
crontab <fichier>
```

#### Modifier la *crontab* existante ou en créer une nouvelle
```bash
crontab -e
```

Chaque nouvelle utilisation de `crontab <fichier>` écrase toutes les tâches planifiées précédentes.

### Syntaxe d'une tâche cron

Une tâche cron est définie selon le format suivant :

```bash
* * * * * commande_à_exécuter
```

Chaque ligne contient :
- **Planification** (5 champs)
- **Tâche** (une commande Bash ou un script, recommandé)

**Exemple :**
```bash
15 * * * * bash /home/<user>/monscript.sh
30 0 * * * bash /usr/local/bin/autrescript.sh
0 * * * * echo "Nouvelle heure" >> /home/<user>/heure.txt
```

{{% notice style="warning" title="Important" %}}
Les scripts doivent être spécifiés avec leur **chemin absolu**.
{{% /notice %}}


### Explication des champs de planification

| Champ        | Valeurs possibles         | Description |
|-------------|--------------------------|-------------|
| **Minute**   | 0-59                      | Minute d'exécution |
| **Heure**    | 0-23                      | Heure d'exécution |
| **Jour**     | 1-31                      | Jour du mois |
| **Mois**     | 1-12                      | Mois de l'année |
| **Jour de semaine** | 0-7 (0 et 7 = dimanche) | Jour de la semaine |

#### Opérateurs utiles
- `*` : chaque unité de temps.
- `,` : énumération de valeurs (`1,5,10`).
- `-` : intervalle (`1-10`).
- `*/n` : exécution périodique (`*/2` signifie toutes les 2 unités).

### Exemples d'utilisation

Exécuter un script chaque jour à 14h30 :
```bash
30 14 * * * bash /chemin/script.sh
```

Exécuter un script chaque heure (à la 25e minute) en mars :
```bash
25 * * 3 * bash /chemin/script.sh
```

Exécuter un script une fois par heure entre 9h et 17h :
```bash
15 9-17 * * * bash /chemin/script.sh
```

Exécuter un script à midi les lundis, mercredis et vendredis :
```bash
0 12 * * 1,3,5 bash /chemin/script.sh
```

Exécuter un script toutes les deux heures :
```bash
0 */2 * * * bash /chemin/script.sh
```

---

## Gestion des paquets avec *dnf*

Sur AlmaLinux, il existe plusieurs façons d'installer une application :
1. **Compiler manuellement** à partir des sources (long et complexe).
2. **Utiliser un paquet RPM** (résolution des dépendances nécessaire).
3. **Utiliser `dnf`** (méthode recommandée, gère les dépendances automatiquement).

### Les dépôts

Les dépôts sont des serveurs où `dnf` télécharge les paquets et leurs dépendances. Ils sont configurés dans :

```
/etc/yum.repos.d/
```

#### Afficher les dépôts actifs
```bash
dnf repolist
```

#### Afficher tous les dépôts (actifs et inactifs)
```bash
dnf repolist all
```

Si un paquet n'est pas disponible, il peut être nécessaire d'ajouter un dépôt.

**Exemple :** Installer le dépôt Remi pour `php-jsonlint` :
```bash
sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
```

Vérifier si le paquet est maintenant disponible :
```bash
dnf search php-jsonlint
```

### Installation d'un paquet

```bash
sudo dnf install <paquet>
```

**Exemple :**
```bash
sudo dnf install -y php-jsonlint
```

L'option `-y` permet de valider automatiquement l'installation.

### Mettre à jour le système

Mettre à jour tous les paquets installés :
```bash
sudo dnf update
```

Lister les mises à jour disponibles sans les installer :
```bash
dnf check-update
```

Mettre à jour un seul paquet :
```bash
sudo dnf update httpd
```

### Recherche de paquets

Trouver un paquet par son nom :
```bash
dnf list httpd
```

Lister tous les paquets disponibles et installés :
```bash
dnf list "*"
```

Rechercher un paquet par son nom ou sa description :
```bash
dnf search httpd
```

Obtenir des informations sur un paquet :
```bash
dnf info httpd*
```

Trouver le paquet fournissant une commande :
```bash
dnf provides <commande>
```

**Exemple :**
```bash
dnf provides /bin/cat
```

### Désinstaller un paquet

```bash
sudo dnf remove <paquet>
```

### Gestion des groupes de paquets

Lister les groupes de paquets disponibles :
```bash
dnf grouplist
```

Afficher des informations sur un groupe :
```bash
dnf groupinfo "Outils internet de la console"
```

Installer un environnement graphique (ex : Xfce) :
```bash
sudo dnf groupinstall "Xfce"
```

### Utiliser le shell *dnf*

Le shell `dnf` permet d'automatiser des installations.

Lancer le shell :
```bash
dnf shell
```

Créer un fichier d'installation automatique :
```bash
install nmap
install zsh
run
```

Exécuter ce fichier avec *dnf* :
```bash
dnf shell installation.txt
```

Exécuter sans confirmation :
```bash
dnf -y shell installation.txt
```


