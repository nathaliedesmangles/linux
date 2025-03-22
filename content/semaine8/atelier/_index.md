+++
title = "ATELIER #8: Dnf et Cron (À MODIFIER POUR CRON)"
weight = 82
draft = true
+++

## Objectif de l'atelier

 - Installer des utilitaires et des applications avec dnf.
 - Se familiariser avec cron.

---

## Instructions de remise

Vous devez soumettre votre travail sur Moodle **d'ici les deux prochaines séances.**  
Les éléments à remettre incluent :  
- **Captures d’écran annotées :**  
  - Montrez les étapes suivies pour déterminer et installer les paquets.  
  - Ajoutez votre nom d’utilisateur Linux sur chaque capture.  
- **Fichiers :**  
  - Une copie de votre crontab.  
  - Le fichier `heures.txt` (après validation).  
  - Le contenu de votre script (lignes utilisées dans cron).  

**Nom des captures d'écran :**  
Suivez le format proposé (ex. `01_ifconfig.png`). Chaque capture doit inclure :  
- Les étapes pour déterminer le nom du paquet.  
- Votre nom d'utilisateur Linux.  

---

# Atelier

## Partie 1 : Utilisation de dnf

1. **Pour chaque description ci-dessous :**  
   - Utilisez `dnf` pour identifier le nom du paquet correspondant (sans utiliser le Web).  
   - Installez le paquet.  
   - Immédiatement après l'installation, exécutez la commande :  
     ```bash
     $ history
     ```  
     - Prenez une capture d’écran montrant uniquement les commandes liées à l’installation.  
     - Rognez et annotez au besoin (ex. nom d'utilisateur).  
2. **Astuces :**  
   - Les descriptions des paquets sont en anglais.  
   - La commande suivante est utile pour rechercher un fichier spécifique dans un paquet :  
     ```bash
     $ dnf provides */FICHIER
     ```  

### Exemple

- **Installer un jeu de ninja.**  
  - Capture nommée : `exemple_ninja.png`  
  - Contenu : étapes pour identifier le paquet + votre nom d'utilisateur.

---

#### Paquets à installer

1. **Paquet 01 :**  
   - Description : l'utilitaire `ifconfig` (ancêtre de `ip addr`).  
   - Capture : `01_ifconfig.png`.  

2. **Paquet 02 :**  
   - Description : `Kmouth` (permet à l'ordinateur de parler pour des personnes muettes).  
   - Capture : `02_kmouth.png`.  

3. **Paquet 03 :**  
   - Description : le langage de programmation `go`.  
   - Capture : `03_go.png`.  

4. **Paquet 04 :**  
   - Description : `ag`, un utilitaire rapide pour chercher dans des fichiers textes.  
   - Capture : `04_ag.png`.  

5. **Paquet 05 :**  
   - Description : un outil pour visualiser l’espace disque utilisé.  
   - Capture : `05_espace.png`.  

6. **Paquet 06 :**  
   - Description : un lecteur de musique.  
   - Capture : `06_musique.png`.  

7. **Paquet 07 :**  
   - Description : un jeu de mémoire où il faut se souvenir de séquences de plus en plus longues.  
   - Capture : `07_jeu.png`.  

8. **Paquet 08 :**  
   - Description : une suite bureautique.  
   - Capture : `08_bureautique.png`.  

---

## Partie 2 : Introduction à cron

Configurer une tâche cron pour automatiser le téléchargement d’un fichier.
 
1. **Configurer une commande cron** pour :  
   - Télécharger le contenu de `http://gyoukou.ca/heure.brut` toutes les minutes :  
     ```bash
     $ wget http://gyoukou.ca/heure.brut
     ```  
   - Ajouter ce contenu dans un fichier nommé `heures.txt`. **Utilisez un chemin absolu pour ce fichier.**  
2. **Vérifiez que la commande fonctionne** :  
   - Utilisez la commande suivante pour observer l’évolution de `heures.txt` :  
     ```bash
     $ tail -f heures.txt
     ```  
3. **Désactivez la tâche cron une fois qu’elle est validée** :  
   - Commentez la ligne dans votre crontab pour éviter que le fichier continue à se remplir à l'infini.

---

### Éléments de validation 

- **Capture d’écran `09_crontab.png`** :  
  - Montrez le contenu de votre crontab.  
  - Indiquez la date de validation.  

