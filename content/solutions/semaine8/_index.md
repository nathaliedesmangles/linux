+++
title = "Atelier 8"
weight = 178
draft = true
+++

# Solution des exercices

## Partie 1 : Utilisation de dnf

Voici comment identifier et installer les paquets demandés à l’aide de `dnf` :  


### Paquet 01 : Utilitaire ***ifconfig***  
**Recherche du paquet :**  
```bash
dnf provides */ifconfig
```
**Installation :**  
```bash
sudo dnf install -y net-tools
```

### Paquet 02 : ***Kmouth***  
**Recherche du paquet :**  
```bash
dnf search kmouth
```
**Installation :**  
```bash
sudo dnf install -y kmouth
```

### Paquet 03 : Langage de programmation ***Go***
**Recherche du paquet :**  
```bash
dnf search golang
```
**Installation :**  
```bash
sudo dnf install -y golang
```

### Paquet 04 : ***ag***, outil de recherche rapide dans les fichiers  
**Recherche du paquet :**  
```bash
dnf search silversearcher
```
**Installation :**  
```bash
sudo dnf install -y the_silver_searcher
```

### Paquet 05 : Outil de visualisation de l’espace disque
**Recherche du paquet :**  
```bash
dnf search disk usage
```
**Installation (exemples possibles) :**  
```bash
sudo dnf install -y ncdu  # Option 1
sudo dnf install -y baobab  # Option 2 (GNOME Disk Usage Analyzer)
```

### Paquet 06 : Lecteur de musique  
**Recherche du paquet :**  
```bash
dnf search music player
```
**Installation (exemples possibles) :**  
```bash
sudo dnf install -y vlc   # Lecteur multimédia puissant
sudo dnf install -y rhythmbox  # Lecteur de musique GNOME
```

### Paquet 07 : Jeu de mémoire 
**Recherche du paquet :**  
```bash
dnf search memory game
```
**Installation (exemples possibles) :**  
```bash
sudo dnf install -y gnome-sudoku   # Jeu de logique avec mémoire
sudo dnf install -y kbraintrainer  # Jeu d'entraînement de la mémoire
```

### Paquet 08 : Suite bureautique  
**Recherche du paquet :**  
```bash
dnf search office suite
```
**Installation (exemples possibles) :**  
```bash
sudo dnf install -y libreoffice  # Suite bureautique complète
```

### Afficher l’historique des commandes ***dnf*** liées à l’installation  
Après avoir installé tous les paquets :  
```bash
history | grep "dnf install"
```

<!--
===================

### Paquet 01

```bash
$ dnf provides ifconfig
$ sudo dnf install -y net-tools
```

### Paquet 02

```bash
$ dnf search speak
$ sudo dnf install -y kmouth
</pre>

### Paquet 03

```bash
$ dnf search go | grep -i lang
$ sudo dnf install -y golang


### Paquet 04

```bash
$ dnf provides ag
$ dnf install -y the_silver_searcher


### Paquet 05

```bash
$ dnf search disk usage
$ sudo dnf install -y filelight


### Paquet 06

```bash
$ dnf search music
$ sudo dnf install -y juk


### Paquet 07

```bash
$ dnf search game | grep -i memory
$ sudo dnf install -y blinken


### Paquet 08

```bash
$ dnf search office
$ sudo dnf install -y libreoffice-writer libreoffice-math libreoffice-calc libreoffice-impress ...


## Cron

Créez un script <code class="gr">/home/&lt;user&gt;/script.sh</code>

Dans le script :

{{< highlight bash "linenos=true,linenumbersintable=false"  >}}
wget --no-check-certificate https://gyoukou.ca/heure.brut
cat /home/axel/heure.brut >> /home/axel/heures.txt
rm /home/axel/heure.brut
{{< / highlight >}}

Ensuite, éditez la crontab :

<pre>
$ crontab -e
</pre>

Dans la crontab :

{{< highlight bash "linenos=true,linenumbersintable=false"  >}}
* * * * * bash /home/axel/script.sh
{{< / highlight >}}
-->

## Partie 2 : Expérimenter avec cron

### Configuration d'une tâche cron pour enregistrer l'heure chaque minute 

#### Éditer la crontab 

Ouvrez l'éditeur de tâches planifiées avec :  
```bash
crontab -e
```

#### Ajouter la tâche cron
  
```bash
* * * * * date "+\%Y-\%m-\%d \%H:\%M:\%S" >> /home/ndesmangles/heures.txt
```

**Explication** :  
- `* * * * *` → Exécute la commande **chaque minute**.  
- `date "+\%Y-\%m-\%d \%H:\%M:\%S"` → Capture l'heure et la date actuelles.  
- `>> /home/ndesmangles/heures.txt` → Ajoute le résultat au fichier sans l'écraser.  

#### Vérifier que le fichier se met à jour
  
Utilisez la commande suivante pour observer en temps réel l’évolution du fichier :  
```bash
tail -f /home/ndesmangles/heures.txt
```

#### Désactiver la tâche après test  

Une fois que vous avez vérifié que cela fonctionne, **commentez la ligne dans la crontab** en ajoutant `#` au début :  
```bash
# * * * * * date "+\%Y-\%m-\%d \%H:\%M:\%S" >> /home/ndesmangles/heures.txt
```
Puis enregistrez et quittez l'éditeur.

**Alternative pour désactiver la tâche complètement** :  
Vous pouvez aussi **supprimer la tâche** avec :  
```bash
crontab -e  # Puis supprimez la ligne
```
