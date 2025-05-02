+++
title = "ATELIER: WSL, Ubuntu et système de fichiers"
weight = 142
+++


## Exercice 0 - Installation de WSL

{{% notice style="warning" title="Attention" %}}
Votre Windows doit être à jour
{{% /notice %}}

- Dans Windows, démarrer paramètres windows update. et cliquer sur ***Vérifier les mises à jour***.
- Au besoin, mettre à jour votre windows.

### Étape 1 : Installer WSL et Ubuntu pour Windows

1. Chercher les fonctionnalités Windows

![HTTP](./recherche-fonctionnalites.png?width=30vw)

2. Ouvrir **Activer ou désactiver des fonctionnalités Windows**
	- Dans la liste, cocher **Sous-Système Windows pour Linux**

![HTTP](activer-fonctionnalite.png?width=35vw)

3. Redémarrer
4. Ouvrir le <a href="https://apps.microsoft.com">Microsoft Store</a>
	- Chercher la dernière version de Ubuntu 24.04.1
	- Cliquer sur **Obtenir** pour Télécharger et Installer
	- Cliquer sur **Ouvrir**

![HTTP](./microsoft_store_ubuntu.png?width=35vw)

5. Dans la fenêtre Ubuntu: patienter durant l'installation

![HTTP](./wsl_patienter.png?height=160)

6. Dans fenêtre Ubuntu: créer votre usager
	- Entrer le nom d'usager de votre choix
	- Entrer le mot de passe de votre choix
	- Confirmer votre mot de passe

![HTTP](./wsl_usager.png?width=65vw)

7. Votre Ubuntu sous WSL est installé!

![HTTP](./wsl.png?width=45vw)

### Étape 2 : Mettre Ubuntu à jour

Avant de commencer, s'assurer qu'Ubuntu est à jour:

```bash
$ sudo apt update
$ sudo apt upgrade
```

<mark>
Prendre une copie d'écran ici
</mark>

---

## Exercice 1 – Démarrer WSL en ligne de commande

**Objectif :** Apprendre à lancer WSL depuis l'invite de commande Windows.

### Étapes :
1. Ouvrir l'invite de commande (cmd) ou PowerShell.
2. Taper la commande suivante :
```bash
$ wsl
```

3. Vous devriez maintenant être dans un shell Ubuntu. Vérifiez avec quelques commande linux :
```bash
$ ls
$ whoami
$ pwd
```

---

## Exercice 2 – Explorer votre disque Windows depuis WSL

**Objectif :** Utiliser le terminal Ubuntu (WSL) pour accéder au système de fichiers Windows.

### Étapes :
1. Ouvrir votre terminal Ubuntu (WSL)
2. Tapez la commande suivante pour accéder à votre disque Windows :
   ```bash
   $ ls /mnt/c
   ```
3. Accédez à votre dossier Documents :
   ```bash
   $ cd /mnt/c/Users/VOTRE_NOM/Documents
   ```
   *(Remplacez `VOTRE_NOM` par votre nom d’utilisateur Windows)*
4. Créez un fichier texte :
   ```bash
   $ echo "Ceci est un test depuis WSL" > test_wsl.txt
   ```
5. Ouvrez l’Explorateur de fichiers Windows et vérifiez que le fichier `test_wsl.txt` existe dans vos Documents.

---

## Exercice 3 – Modifier le fichier avec Visual Studio Code

**Objectif :** Utiliser VS Code pour éditer un fichier se trouvant dans le système de fichiers Windows depuis WSL.

### Étapes :
1. Depuis le terminal Ubuntu, restez dans le dossier :
   ```bash
   $ cd /mnt/c/Users/VOTRE_NOM/Documents
   ```
2. Lancez Visual Studio Code :
   ```bash
   $ code .
   ```
3. Dans VS Code, ouvrez le fichier `test_wsl.txt`.
4. Modifiez son contenu (par exemple : ajoutez une nouvelle ligne), puis **enregistrez**.
5. Revenez au terminal et tapez :
   ```bash
   $ cat test_wsl.txt
   ```
   pour vérifier que les changements sont bien enregistrés.


---
**References**:  
1. [Site Ubuntu WSL](https://documentation.ubuntu.com/wsl/en/latest/guides/install-ubuntu-wsl2/)
2. [Vidéo YouTube](https://youtu.be/HrAsmXy1-78?si=VyvuNbkGmthsnLAI)
---
