+++
title = "CRON et DNF"
weight = 81
+++

## Planification des tâches avec *Cron*

Le programme **cron** permet de planifier des tâches automatiquement sur un système Linux. Chaque utilisateur peut définir ses propres tâches planifiées, qui sont stockées par défaut dans :

```
/var/spool/cron/
```

### Qu'est-ce qu'une crontab ?

{{% notice style="info" title="Qu'est-ce qu'une Crontab ?" %}}
Une ***crontab*** (abréviation de ***cron table***) est un fichier de configuration utilisé par le planificateur de tâches ***cron*** sous Unix/Linux. Il permet d'exécuter automatiquement des commandes ou des scripts à des moments spécifiés.
{{% /notice %}}

Il est possible d'utiliser un fichier personnalisé pour la planification. Le ***deamon*** responsable de l'exécution des tâches est **crond**.

{{% notice style="info" title="Qu'est-ce qu'un Deamon ?" %}}
Un ***deamon*** est un type de programme informatique, un processus ou un ensemble de processus qui s'exécute en **arrière-plan** plutôt que sous le contrôle direct d'un utilisateur.
{{% /notice %}}


### Commandes principales de *cron*

| Action | Commande | Résultat / Remarque |
|--------|---------|---------------------|
| **Afficher ou lancer les tâches planifiées de l'utilisateur actuel** | `crontab -l` | - Affiche la liste des tâches planifiées.<br>- Si aucune tâche n'est planifiée, affiche ***no crontab for user***. |
| **Supprimer toutes les tâches planifiées de l'utilisateur** | `crontab -r` | **<span style="color:red;">Action irréversible</span>**. Toutes les tâches sont supprimées définitivement. |
| **Gérer la crontab d'un autre utilisateur** (nécessite *root*) | `sudo crontab -u <utilisateur> -l` <br> **Exemple**: `sudo crontab -u ndesmangles -l` | - `-u <utilisateur>` : Spécifie l'utilisateur ciblé.<br>- `-l` : Liste les tâches de cet utilisateur. |
| **Charger ou remplacer une tâche planifiée à partir d'un fichier** | `crontab <fichier>` <br> **Exemple** : `crontab ma_tache.txt` | - Charge les tâches depuis `<fichier>`.<br> **<span style="color:red;">Chaque nouvelle utilisation écrase les tâches précédentes.</span>** |
| **Modifier la crontab existante ou en créer une nouvelle** | `crontab -e` | - Ouvre la crontab dans un éditeur de texte (ex: Vim).<br>- Permet d'ajouter, modifier ou supprimer des tâches. |


<!--

| Action | Commande | Résultat / Remarque |
|--------|---------|---------------------|
| **Afficher ou lancer les tâches planifiées de l'utilisateur actuel** | `crontab -l` | - Affiche la liste des tâches planifiées.<br>- Si aucune tâche n'est planifiée, affiche ***no crontab for user***. |
| **Supprimer toutes les tâches planifiées de l'utilisateur** | `crontab -r` | **<span style="color:red;">Action irréversible**</span>. Toutes les tâches sont supprimées définitivement. |
| **Gérer la crontab d'un autre utilisateur** (nécessite *root*) | `sudo crontab -u <utilisateur> -l` <br> **Exemple**: `sudo crontab -u ndesmangles -l`| - `-u <utilisateur>` : Spécifie l'utilisateur ciblé.<br>- `-l` : Liste les tâches de cet utilisateur. |
| **Charger ou remplacer une tâche planifiée à partir d'un fichier** | `crontab <fichier>` <br> **Exemple** : `crontab ma_tache.txt`| - Charge les tâches depuis `<fichier>`.<br> **<span style="color:red;">Chaque nouvelle utilisation **écrase** les tâches précédentes.</span>** |
| **Modifier la crontab existante ou en créer une nouvelle** | `crontab -e` | - Ouvre la crontab dans un éditeur de texte (ex: Vim).<br>- Permet d'ajouter, modifier ou supprimer des tâches. |


#### Afficher les tâches planifiées de l'utilisateur actuel
```bash
crontab -l
```
**Résultat** : 
- Si aucune tâche n'est planifiée, le message ***no crontab for user*** s'affiche.
- Sinon, la liste des tâches planifiées s'affiche (voir un exemple ICI)

#### Supprimer toutes les tâches planifiées de l'utilisateur
```bash
crontab -r
```
{{% notice style="warning" title="Attention" icon="skull-crossbones" %}}
**Cette action est irréversible**.
{{% /notice %}}


#### Gérer la crontab d'un autre utilisateur (nécessite d'être *root*)
```bash
sudo crontab -u <utilisateur> -l
```

`-u <utilisateur>` : Spécifie l'utilisateur dont on veut voir les tâches cron 
`-l` : Liste les entrées de la crontab de cet utilisateur

**Exemple** :
```bash
sudo crontab -u ndesmangles -l
```


#### Charger ou remplacer une tâche planifiée à partir d'un fichier
```bash
crontab <fichier>
```
**Exemple** :
```bash
crontab ma_tache.txt
```

{{% notice style="note" title="À savoir..." %}}
- Chaque nouvelle utilisation de `crontab <fichier>` écrase toutes les tâches planifiées précédentes.
{{% /notice %}}

#### Modifier la *crontab* existante ou en créer une nouvelle
```bash
crontab -e
```

**Résultat** : La crontab s'ouvre dans l'éditeur de texte (ex: Vim)
-->

### Syntaxe d'une tâche ***cron***

Une tâche ***cron*** est définie selon le format suivant :

```bash
* * * * * tâche_à_exécuter
```

Chaque ligne contient :
- **Planification** (Les cinq étoiles représentent 5 champs)
- **Tâche** (une commande *Bash* ou de préférence un script)

**Exemple :**
```bash
15 * * * * bash /home/ndesmangles/monscript.sh
30 0 * * * bash /usr/local/bin/autrescript.sh
0 * * * * echo "Nouvelle heure" >> /home/ndesmangles/heure.txt
```

{{% notice style="warning" title="Important" %}}
Les scripts doivent être spécifiés avec leur **chemin absolu**.
{{% /notice %}}


### Explication des champs de planification (le moment auquel la tâche doit s'exécuter)

| No du champ *  | Rôle du champ       | Valeurs possibles |
|:--------------:|---------------------|:-----------------:|
|**1<sup>er</sup>**            | **Minute**          | 0 à 59            |
|**2<sup>e</sup>**             | **Heure**           | 0 à 23            |
|**3<sup>e</sup>**            | **Jour du mois**    | 1 à 31            |
|**4<sup>e</sup>**            | **Mois de l'année** | 1 à 12            |
|**5<sup>e</sup>**            | **Jour de semaine** | 0 et 7 = dimanche <br> 1 = lundi<br> 2 = mardi, etc. |

#### Opérateurs utiles
- `*` : chaque unité de temps.
- `,` : énumération de valeurs (`1,5,10`).
- `-` : intervalle (`1-10`).
- `*/n` : exécution périodique (`*/2` signifie toutes les 2 unités).

### Exemples d'utilisation

Exécuter un script **chaque jour à 14h30** :
```bash
30 14 * * * bash /chemin_absolu/script.sh
```

Exécuter un script **chaque heure (à la 25e minute) en mars** :
```bash
25 * * 3 * bash /chemin_absolu/script.sh
```

Exécuter un script **une fois par heure entre 9h et 17h (9h15, 10h15, ..., 17h15)** :
```bash
15 9-17 * * * bash /chemin_absolu/script.sh
```

Exécuter un script **à midi les lundis, mercredis et vendredis** :
```bash
0 12 * * 1,3,5 bash /chemin_absolu/script.sh
```

Exécuter un script **toutes les deux heures** :
```bash
0 */2 * * * bash /chemin_absolu/script.sh
```

---

## Gestion des paquets avec *dnf*

Sur Linux, il existe plusieurs façons d'installer une application :
1. **Compiler manuellement** à partir des sources (long et complexe).
2. **Utiliser un paquet RPM** (résolution des dépendances nécessaire).
3. **Utiliser** ***dnf*** (méthode **recommandée**, gère les dépendances automatiquement).

### Les dépôts

{{% notice style="info" title="Définition" %}}
Les dépôts sont des **serveurs où `dnf` télécharge les paquets et leurs dépendances**. Ils sont configurés dans le répertoire :

```
/etc/yum.repos.d/
```
{{% /notice %}}


### Affichage des dépôts de l'utilisateur

| Action                       | Commande            | 
|------------------------------|---------------------|
|**Afficher les dépôts actifs**| `dnf repolist`      |
|**Afficher tous les dépôts (actifs et inactifs)**| `dnf repolist all`      |

Si un paquet n'est pas disponible, il peut être nécessaire d'ajouter son dépôt.

{{% notice style="info" title="Information" %}}
Sur Ubuntu, la commande ***dnf*** n'est pas disponible par défaut, car Ubuntu utilise ***apt*** (*Advanced Package Tool*) pour la gestion des paquets et non ***dnf*** qui est utilisé par des distributions comme **Fedora** ou **AlmaLinux**.
Pour installer ***dnf*** sur Ubuntu:
```bash
sudo apt install dnf
```
{{% /notice %}}

#### Exemple d'installation d'un dépôt sur Ubuntu

{{% notice style="red" title="Installer le dépôt Universe" groupid="notice-toggle" expanded="false" %}}

Le dépôt **"Universe"** contient une grande variété de logiciels open-source et de communautés, souvent plus expérimentaux ou non pris en charge officiellement par Ubuntu. Il inclut des outils amusants, des jeux et des utilitaires utiles qui ne sont pas présents dans les dépôts principaux.

### Exemple d'installation :
1. Pour ajouter le dépôt **"Universe"** :
   ```bash
   sudo add-apt-repository universe
   sudo apt update
   ```

2. Après, on peut installer un jeu amusant ou un utilitaire amusant comme **`cowsay`**  :
   ```bash
   sudo apt install cowsay
   ```

3. Pour tester ce logiciel avec :
   ```bash
   cowsay "Bonjour, Ubuntu!"
   ```
{{% /notice %}}


### Installation d'un paquet

| Action                       | Commande            |
|------------------------------|---------------------|
|**Installer un paquet**| `sudo dnf install -y <paquet>` <br> **Exemple :** <br> `sudo dnf install -y php-jsonlint`|


{{% notice style="info" title="Information" %}}
L'option `-y` permet de valider automatiquement l'installation, sans avoir à taper ***Yes*** (Oui) à chaque demande de validation pendant l'installation.
{{% /notice %}}


### Mettre à jour le système

| Action                       | Commande            |
|------------------------------|---------------------|
|**Mettre à jour tous les paquets installés**| `sudo dnf update`|
|**Lister les mises à jour disponibles sans les installer** | `dnf check-update` |
|**Mettre à jour un seul paquet** | `sudo dnf update httpd` |


### Recherche de paquets

| Action                       | Commande            | Exemple |
|------------------------------|---------------------|-----------------|
|**Trouver un paquet par son nom**| `dnf list <nom_paquet>`| `dnf list httpd` |
|**Rechercher un paquet en fonction de son nom ou description**| `dnf search <nom_paquet>` | `dnf search httpd` |
|**Obtenir des informations sur un paquet**| `dnf info <nom_paquet>*`| `dnf info httpd` |
|**Affiche la liste des paquets installés et/ou disponibles dans les dépôts.**| `dnf list installed` <br> `dnf list "*"` |
|**Trouver le paquet qui fourni une commande** | `dnf provides <commande>` | `dnf provides /bin/cat`|

#### Quand utiliser ***dnf list*** ou ***dnf search***


| Commande | Fonction | Affichage | Utilisation typique | Exemples |
|----------|---------|-----------|---------------------|----------|
| **`dnf list`** | Liste les paquets **installés et/ou disponibles** | Nom du paquet, version, dépôt | Vérifier si un paquet est installé ou disponible | `dnf list installed` <br> `dnf list available` <br> `dnf list --installed nano` |
| **`dnf search`** | Recherche les paquets par mot-clé dans le **nom** et la **description** | Liste des paquets correspondants | Trouver un paquet dont on ne connaît pas le nom exact | `dnf search text editor` <br> `dnf search network` |

- Si vous connaissez **le nom exact** du paquet ➝ `dnf list`  
- Si vous cherchez **un paquet correspondant à un mot-clé** ➝ `dnf search`

### Désinstaller un paquet

| Action                     | Commande            |
|----------------------------|---------------------|
| **Désinstaller un paquet** | `sudo dnf remove <paquet>`|


### Gestion des groupes de paquets  

| Action                  | Commande |
|-------------------------|----------|
| **Lister les groupes de paquets disponibles** | `dnf grouplist` |
| **Afficher des informations sur un groupe** | `dnf groupinfo "<nom_du_groupe>"` <br>**Exemple** : <br> `dnf groupinfo "Outils internet de la console"` |
| **Installer un groupe de paquets** | `sudo dnf groupinstall "<nom_du_groupe>"` <br>**Exemple** : <br> `sudo dnf groupinstall "Xfce"` |  

**Astuce :** Utilisez `dnf grouplist --hidden` pour voir aussi les groupes cachés.


### Utiliser le shell *dnf*

Le shell `dnf` permet d'automatiser des installations. 

| Action | Commande | Description | Exemple |
|--------|---------|-------------|---------|
| **Lancer le shell** | `dnf shell` | Lance un shell interactif pour exécuter des commandes dnf. | `dnf shell` |
| **Créer un fichier d'installation automatique** | ```bash install <paquet> ```<br>```bash run``` | Crée un fichier d’installation automatique contenant des commandes dnf à exécuter. | ```bash install nmap```<br>```bash install zsh```<br>```bash run``` |
| **Exécuter ce fichier avec dnf** | `dnf shell <fichier>` | Exécute un fichier d’installation automatique dans le shell dnf. | `dnf shell installation.txt` |
| **Exécuter sans confirmation** | `dnf -y shell <fichier>` | Exécute un fichier d'installation automatique sans demander de confirmation. | `dnf -y shell installation.txt` |


