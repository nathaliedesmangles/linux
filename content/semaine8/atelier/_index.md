+++
title = "ATELIER #8: Dnf et Cron"
weight = 82
+++

## Objectifs de l'atelier

 - Installer des utilitaires et des applications avec ***dnf***.
 - Se familiariser avec ***cron***.

---

## Instructions de remise
  
Les éléments à remettre incluent :  
- **Captures d’écran annotées :**  
  - Montrez les étapes suivies pour déterminer le nom du paquet et l'installer.  
  - Votre nom d’utilisateur Linux doit être visible sur chaque capture. 
- **Nom des captures d'écran :** Suivez le format proposé (ex. `01_ifconfig.png`).  
- **Fichiers :**  
  - Une copie de votre *crontab*.  
  - Le fichier `heures.txt` (après validation).  
  - Le contenu de votre script (lignes utilisées dans *cron*).  

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
     $ dnf provides */fichier
     ```  

La commande `dnf provides` (ou `dnf whatprovides`) permet de rechercher quel paquet contient un fichier spécifique.

### Exemple

Si vous essayez d'exécuter `ifconfig` mais que la commande n'est pas trouvée, vous pouvez chercher le paquet qui l'inclut avec la commande :
```bash
dnf provides */ifconfig
```

**Résultat possible** :
```yaml
net-tools-2.0-0.52.20160912git.el8.x86_64 : Basic networking tools
```
Cela indique que la commande `ifconfig` est fournie par le paquet `net-tools`.

**Pour l'installer** :
```bash
sudo dnf install net-tools
```

---

### Paquets à installer

1. **Paquet 01 : (voir l'exemple plus haut)**  
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

## Partie 2 : Expérimenter avec *cron*

Dans cet exercice, vous allez configurer une tâche planifiée qui exécutera une commande périodiquement afin d’accumuler des Relevés d’heure dans un fichier.

L’objectif est d’observer comment un fichier peut croître automatiquement au fil du temps et d’apprendre à gérer une tâche récurrente. Vous pourrez ensuite suivre l’évolution du fichier en temps réel et désactiver la tâche une fois satisfait du résultat.

1. Installer une commande *cron* qui va :
	- exécuter une commande enregistrant l’heure actuelle chaque minute
	- accumuler ce contenu dans le fichier **heures.txt**.
		<br><b><span style="color:red;">ATTENTION</span></b>: utiliser un <b><u>chemin absolu</u></b>
2. Vous pouvez vérifier que le fichier **heures.txt** grossit à chaque minute à l'aide de la commande suivante:

	```bash
	$ tail -f heures.txt
	```

3. <b><span style="color:red;">IMPORTANT</span></b> : une fois satisfait que votre commande fonctionne, désactiver votre ligne *cron*.
	- (p.ex. en la mettant en commentaire à l'aide du symbole `#`)
	- on ne veut pas continuer à accumuler du contenu dans **heures.txt** à chaque minute pour toujours.


### Remise 

- **Capture d’écran `09_crontab.png`**, on doit voir :  
  - le contenu de votre *crontab*.  
  - la date de validation.  

