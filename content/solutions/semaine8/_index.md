+++
title = "Atelier 8"
weight = 178
+++

# Solution des exercices

## Partie 1 : Utilisation de dnf

{{% notice style="secondary" title="Information" %}}
La commande `history` peut être exécutée après chaque installation ou 1 fois à la fin
{{% /notice %}}

Voici comment identifier et installer les paquets demandés à l’aide de `dnf` :  

### Paquet 01 : Utilitaire ***ifconfig***  
**Recherche du paquet**  
```bash
$ dnf provides */ifconfig
```
**Installation**  
```bash
$ sudo dnf install -y net-tools
```

### Paquet 02 : ***kmouth***  
**Recherche du nom du paquet**  
```bash
$ dnf search kmouth
==================== Nom correspond exactement à : kmouth =====================
kmouth.x86_64 : A program that speaks for you
```

**Au besoin**, exemples de mots clés pour la recherche: `speak`, `voice`, `text-to-speech`  

**Installation :**  
```bash
$ sudo dnf install -y kmouth
```

### Paquet 03 : Langage de programmation ***Go***
**Recherche du nom du paquet**  
```bash
$ dnf search go | grep -i lang
```
**Installation**  
```bash
$ sudo dnf install -y golang
```

### Paquet 04 : ***ag***, outil de recherche rapide dans les fichiers  
**Recherche du paquet**  
```bash
$ dnf provides ag
the_silver_searcher-2.2.0^2020704.5a1c8d8-3.el9.x86_64 : Super-fast text
                                                       : searching tool (ag)
Dépôt               : epel
Correspondances trouvées dans  :
Fournir : ag
```
**Installation**  
```bash
$ sudo dnf install -y the_silver_searcher
```

### Paquet 05 : Outil de visualisation de l’espace disque
**Recherche du paquet :**  
```bash
$ dnf search disk usage
=================== Nom & Résumé correspond à : disk, usage ====================
mate-disk-usage-analyzer.x86_64 : A disk usage analyzing tool for MATE Desktop
====================== Résumé correspond à : disk, usage =======================
dua-cli.x86_64 : Tool to conveniently learn about the disk usage of directories
duc.x86_64 : Disk usage tools
filelight.x86_64 : Graphical disk usage statistics
gdu.x86_64 : Fast disk usage analyzer with console interface written in Go
kdf.x86_64 : View disk usage
ncdu.x86_64 : Text-based disk usage viewer
quota.x86_64 : System administration tools for monitoring users' disk usage
```
**Installation (exemples possibles)**  
```bash
$ sudo dnf install -y ncdu   # Option 1
$ sudo dnf install -y quota  # Option 2 
```

### Paquet 06 : Lecteur de musique  
**Recherche du paquet**  
```bash
$ dnf search music player
================== Nom & Résumé correspond à : player, music ===================
game-music-emu-player.x86_64 : Demo player utilizing Game_Music_Emu
===================== Résumé correspond à : player, music ======================
juk.x86_64 : Music player
libmikmod.x86_64 : A MOD music file player library
openmpt123.x86_64 : Command-line tracker music player based on libopenmpt
sidplayfp.x86_64 : SID chip music module player
```
**Installation (exemples possibles)**  
```bash
$ sudo dnf install -y game-music-emu-player       
$ sudo dnf install -y juk 
```

### Paquet 07 : Jeu de mémoire 
**Recherche du paquet**  
```bash
$ dnf search memory game
====================== Résumé correspond à : memory, game ======================
blinken.x86_64 : Memory Enhancement Game
```
**Installation**  
```bash
$ sudo dnf install -y blinken   
```

### Paquet 08 : Suite bureautique  
**Recherche du paquet :**  
```bash
$ dnf search office suite
================== Nom & Résumé correspond à : suite, office ===================
libreoffice.x86_64 : Free Software Productivity Suite
```
**Installation**  
```bash
$ sudo dnf install -y libreoffice  # Suite bureautique complète
```

### Afficher l’historique des commandes ***dnf*** liées à l’installation  
Après avoir installé tous les paquets :  
```bash
history | grep "dnf install"
```
---

## Partie 2 : Expérimenter avec cron

Il y a **deux façons** d'aborder l'exercice:
1. (**Recommandée**) À l'aide d'un script qui contient la commande à exécuter (à chaque minute).
2. En écrivant la commande, directement dans la crontab.

### 2.1 À l'aide d'un script

1. **Création du script qui permet d'écrire la date et l'heure actuelles dans le fichier heures.txt**

   ```bash
   vim atelier8.sh
   ```
   **Dans le fichier atelier8.sh**
   ```bash
   #!/bin/bash

   date "+\%Y-\%m-\%d \%H:\%M:\%S" >> /home/ndesmangles/heures.txt
   ```

2. **Création de la tâche *cron* pour exécuter le script chaque minute**  

   **Ouvrir l'éditeur de tâches planifiées avec** :  
   ```bash
   crontab -e
   ```
   **Dans la crontab, indiquer le <b><span style="color:red;">chemin absolu<span></b> vers le script à exécuter chaque minute :**
   ```bash
   */1 * * * * bash  /home/ndesmangles/atelier08.sh
   ```

   **Explication** :  
   - `*/1 * * * *` → Exécute le script **chaque minute**.  
   - `date "+\%Y-\%m-\%d \%H:\%M:\%S"` → Capture la date et l'heure actuelles.  
   - bash `/home/ndesmangles/atelier08.sh` → exécution du script (**chemin absolu** vers le script)

3. **Vérifier que le fichier se met à jour**
  
   **Utilisez la commande suivante pour observer en temps réel l’évolution du fichier** :  
   ```bash
   tail -f /home/ndesmangles/heures.txt
   2025-03-23 16:26:01
   2025-03-23 16:27:02
   2025-03-23 16:28:01
   ...
   ```

---

### 2.2 Inscrire la commande directement dans la crontab

1. **Ouvrir l'éditeur de tâches avec** :  
   ```bash
   crontab -e
   ```

2. **Écrire la tâche cron**
   ```bash
   */1 * * * * date "+\%Y-\%m-\%d \%H:\%M:\%S" >> /home/ndesmangles/heures.txt
   ```

   **Explication** :  
   - `*/1 * * * *` → Exécute la commande **chaque minute**.  
   - `date "+\%Y-\%m-\%d \%H:\%M:\%S"` → Capture la date et l'heure actuelles.  
   - `>> /home/ndesmangles/heures.txt` → Ajoute le résultat au fichier sans l'écraser.  

3. **Vérifier que le fichier se met à jour**
  
   **Utilisez la commande suivante pour observer en temps réel l’évolution du fichier** :  
   ```bash
   tail -f /home/ndesmangles/heures.txt
   2025-03-23 16:26:01
   2025-03-23 16:27:02
   2025-03-23 16:28:01
   ...
   ```
---

### Désactiver la tâche après le test  

Une fois que vous avez vérifié que cela fonctionne, **commentez la ligne dans la crontab** en ajoutant `#` au début :  
```bash
# */1 * * * * bash  home/ndesmangles/atelier08.sh
```

ou 

```bash
# */1 * * * * date "+\%Y-\%m-\%d \%H:\%M:\%S" >> /home/ndesmangles/heures.txt
```

Puis enregistrez et quittez l'éditeur.

**Alternative pour désactiver la tâche complètement** :  
Vous pouvez aussi **supprimer définitivement la tâche** avec :  
```bash
crontab -e  # Puis supprimez la ligne

ou

crontab -r  # Supprime toutes les crontab existantes.
```
