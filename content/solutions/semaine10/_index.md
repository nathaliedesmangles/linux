+++
title = "Atelier #10a"
weight = 180
+++

# Solution de l'exercice

---

### **1. Informations sur les utilisateurs**
Les deux fichiers contenant les informations sur les utilisateurs sont :
- `/etc/passwd` : contient les informations générales sur les utilisateurs (login, UID, GID, répertoire personnel, shell, etc.).
- `/etc/shadow` : contient les mots de passe cryptés des utilisateurs (accessible uniquement par root).


### **2. Création de groupes**
```bash
sudo groupadd dev
sudo groupadd finance
```

### **3. Création de comptes utilisateurs**
```bash
sudo useradd -c "Financier" -g finance fifi
sudo useradd -c "Développeur" -g dev didi
```
Explication :
- `-c` permet d’ajouter un commentaire.
- `-g` spécifie le groupe principal.


### **4. Changement de mot de passe**
```bash
echo "fifi:psswdfifi" | sudo chpasswd
echo "didi:psswddidi" | sudo chpasswd
```
> ⚠️ Astuce : ces mots de passe doivent être **robustes**, donc dans la vraie vie, évitez les mots de passe simples ou contenant le nom d’utilisateur.


### **5. Modification du shell**

**Liste des shells disponibles :**
```bash
cat /etc/shells
```

**Changer le shell de `didi` (ex: `/bin/bash` vers `/bin/sh`)** :
```bash
sudo usermod -s /bin/sh didi
```


### **6. Affichage des informations utilisateurs**

**À partir du fichier `/etc/passwd` :**
```bash
grep fifi /etc/passwd
grep didi /etc/passwd
```

**Avec la commande `id` :**
```bash
id fifi
id didi
```

### **7. Groupes primaires et secondaires**

Après avoir utilisé la commande `id` pour chaque utilisateur, vous verrez une sortie comme :

```bash
id fifi
# uid=1001(fifi) gid=1002(finance) groups=1002(finance)

id didi
# uid=1002(didi) gid=1003(dev) groups=1003(dev)
```

> Le **groupe principal** est celui associé à `gid=...`, les **groupes secondaires** sont listés après groups= (dans cet exemple, ils n’en ont pas, car c'est le même **id** que le groupe principal).
