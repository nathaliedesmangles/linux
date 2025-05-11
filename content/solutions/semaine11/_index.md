+++
title = "Atelier #10b"
weight = 181
+++

# Solution de l'exercice

---

## 1. Connexion avec l’utilisateur `didi`

💡 *Pourquoi ?*  
On veut que toutes les actions suivantes soient faites par l’utilisateur `didi`.

```bash
su - didi
```

> *`su` signifie “switch user” – on change d’utilisateur pour didi.*


## 2. Gestion des permissions de fichier

### a. Création du fichier `fichierCommun.txt`

```bash
touch fichierCommun.txt
```

> *On crée un fichier vide nommé fichierCommun.txt.*

### b. Ajouter `fifi` au **groupe propriétaire du fichier**

1. Vérifier le groupe actuel du fichier :

```bash
ls -l fichierCommun.txt
```

Sortie exemple :

```bash
-rw-r--r-- 1 didi didi 0 avril 12 10:00 fichierCommun.txt
```

> Ici, le groupe du fichier est aussi `didi`.

2. Ajouter `fifi` au groupe `didi` (à faire comme **root**) :

```bash
usermod -aG didi fifi
```

💡 *Explication :*  
- `usermod` : commande pour modifier un utilisateur  
- `-aG` : ajoute (`a`) au groupe secondaire (`G`)  
- `didi` : le nom du groupe  
- `fifi` : le nom de l’utilisateur à ajouter

> ⚠️ Nécessite les droits administrateur.

### c. Donner les **droits de lecture et écriture** au **groupe propriétaire** (méthode symbolique)

```bash
chmod g+rw fichierCommun.txt
```

💡 *Explication :*  
- `g` = group  
- `+rw` = ajouter lecture (`r`) et écriture (`w`)


## 3. Vérification des droits

```bash
ls -l fichierCommun.txt
```

Exemple de résultat :

```bash
-rw-rw---- 1 didi didi 0 avril 12 10:00 fichierCommun.txt
```

💡 *Interprétation des droits :*

- `rw-` pour le propriétaire → lecture et écriture
- `rw-` pour le groupe → lecture et écriture
- `---` pour les autres → aucun droit


## 4. Modification des droits (2 méthodes)

### Objectif :

| Type d’utilisateur | Droits voulus    |
|--------------------|------------------|
| Propriétaire       | lecture, écriture, exécution |
| Groupe             | lecture seulement |
| Autres             | aucun             |

### a. Méthode **symbolique**

```bash
chmod u=rwx,g=r,o= fichierCommun.txt
```

💡 *Décomposition :*

- `u=rwx` → user = lecture, écriture, exécution  
- `g=r` → group = lecture seulement  
- `o=` → other = aucun droit

### b. Méthode **octale**

```bash
chmod 740 fichierCommun.txt
```

💡 *Correspondance :*

- `7` (user) = 4 (lecture) + 2 (écriture) + 1 (exécution)  
- `4` (group) = lecture  
- `0` (other) = aucun droit


## 5. Vérification finale

```bash
ls -l fichierCommun.txt
```

Sortie attendue :

```bash
-rwxr----- 1 didi didi 0 avril 12 10:05 fichierCommun.txt
```


## 6. Retour à votre session habituelle

```bash
su - votreLogin
```

> *On revient à l’utilisateur initial pour terminer le travail.*