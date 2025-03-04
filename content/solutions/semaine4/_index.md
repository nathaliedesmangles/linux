+++
title = "Atelier 4"
weight = 164
+++

# Solution des exercices

## Exercice 1

1. Ouvrir une session avec l’utilisateur standard et reproduire, dans le répertoire courant, l'arborescence suivante et ce en utilisant un **maximum de trois commandes** : 
 
```
├── H2025
│   ├── Linux
│   │   ├── Cours
│   │   └── Ateliers
│   └── Virtualisation
│       └── machines
└── Icones 
``` 

### Solution 1 : Une seule commande ***mkdir -p***

```bash
$ mkdir -p H2025/{Linux/{Cours,Ateliers},Virtualisation/machines} Icones
```
**Avantages** : Très concise, une seule commande.  
**Inconvénients** : Moins lisible si l'arborescence est complexe.  

---

### Solution 2 : Trois commandes ***mkdir*** séparées
```bash
$ mkdir -p H2025/Linux H2025/Virtualisation Icones
$ mkdir -p H2025/Linux/Cours H2025/Linux/Ateliers
$ mkdir -p H2025/Virtualisation/machines
```
**Avantages** : Plus lisible, chaque commande crée une partie logique de l'arborescence.  
**Inconvénients** : Utilise trois commandes, soit le maximum autorisé.   

---


2. Changer de répertoire en allant dans le dossier **Cours**. 
```bash
$ cd H2025/Linux/Cours
```

3. En saisissant une seule commande, créer, à l’intérieur du répertoire courant, les dossiers semaine1, semaine2, …, semaine15. Vous **ne devez pas** entrer tous les noms de semaines dans la commande (**hint**: expansion d'accolades). 
```bash
$ mkdir semaine{1..15}
```

4. À l'aide d'une **boucle for**, à l'intérieur de chaque dossier **semaine**, créer un fichier .txt qui contient la phrase suivante :
<mark>Ce cours concerne la semaineN</mark>

Où `N` correspond au numéro de la semaine. 
```bash
$ for i in {1..15}; do echo "Ce cours concerne la semaine$i" > semaine$i/semaine$i.txt; done
```
**Explication** :
- ***for i in {1..15}*** : Crée une boucle qui itère de 1 à 15.
- ***echo "Ce cours concerne la semaine$i"*** : Génère la phrase avec le numéro de la semaine.
- ***> semaine$i/semaine$i.txt*** : Crée un fichier semaine$i.txt dans le dossier semaine$i et y écrit la phrase.

```
└── Cours
    ├── semaine1
    │   └── semaine1.txt
    ├── semaine10
    │   └── semaine10.txt
    ├── semaine11
    │   └── semaine11.txt
```


5. Toujours à partir du répertoire courant, utiliser un **chemin relatif** pour copier dans le dossier **Ateliers** le fichier **`passwd`** qui est dans **`/etc`**. 
```bash
$ cp ../../../../../etc/passwd ../Ateliers/
```
```
├── Ateliers
│   └── passwd
└── Cours
    ├── semaine1
    │   └── semaine1.txt
    ├── semaine10
    │   └── semaine10.txt
```

6. Toujours à partir du répertoire courant et en utilisant un **chemin relatif**, renommer le fichier copié en ajoutant "Copie" à son nom (`passwdCopie`).
```bash
$ mv ../Ateliers/passwd ../Ateliers/passwdCopie
```
```
├── Ateliers
│   └── passwdCopie
└── Cours
    ├── semaine1
    │   └── semaine1.txt
    ├── semaine10
    │   └── semaine10.txt
```

7. Changer toutes les occurrences du caractère délimiteur `:` (deux points) du fichier `passwdCopie` par `;` (point-virgule).
```bash
$ sed -i 's/:/;/g' ../Ateliers/passwdCopie
```

**Explication :**
- `sed` : Outil pour modifier un fichier en ligne.
- `-i` : Modifie le fichier en place (sans créer de fichier temporaire).
- `s/:/;/g` : Remplace tous les `:` par des `;` (g pour global, c'est-à-dire dans tout le fichier).
- `../Ateliers/passwdCopie` : Le fichier à modifier, situé dans le dossier **`Ateliers`**.

8. Trier le contenu du fichier `passwdCopie` en ordre croissant du numéro de groupe, soit le quatrième champ. On veut que le fichier soit trié et non uniquement le résultat retourné par la commande. 
```bash
$ sort -t ';' -k4n ../Ateliers/passwdCopie -o ../Ateliers/passwdCopie
```

**Explication :**
- `sort` : Outil pour trier le contenu d'un fichier.
- `-t ';'` : Définit le délimiteur comme étant le point-virgule (`;`).
- `-k4n` : Trie les lignes en fonction du quatrième champ qui est numérique.
- `-o ../Ateliers/passwdCopie` : Sauvegarde directement le résultat trié dans le même fichier **`passwdCopie`**.

---

## Exercice 2

Revenir dans votre dossier personnel.
```bash
$ cd ~
```

1. Écrire la commande qui permet de compter le nombre d'utilisateurs qui ont pour shell le `/bin/bash`. Vous trouverez cette information dans le fichier `/etc/passwd`. 
```bash
$ echo "$(grep -c '/bin/bash' /etc/passwd) utilisateurs ont pour shell /bin/bash"
```

**Explication :**
- `grep -c '/bin/bash' /etc/passwd` : Cherche toutes les lignes contenant **`/bin/bash`** dans le fichier **`/etc/passwd`** et renvoie le nombre de correspondances (l'option `-c` compte les lignes).
- `echo "$( ... )"` : Affiche le résultat avec le texte personnalisé. Le nombre d'utilisateurs est inséré dans le message.


2. Maintenant on veut écrire la ligne de commande qui permet d’afficher le nombre d’utilisateurs qui ont pour shell par défaut un des shells disponibles sur votre machine. Pour cela, il faut parcourir le fichier `/etc/shells` **ligne par ligne** (**hint**: boucle). Vous y trouverez les shells disponibles. 
```bash
while read shell; do
    cpt=$(grep -c "^.*:$shell" /etc/passwd)
    echo "$cpt utilisateurs ont pour shell $shell"
done < /etc/shells

```

**Explication :**
- `while read shell; do` : Lit chaque ligne du fichier `/etc/shells` et stocke la valeur dans shell.
- `grep -c "^.*:$shell" /etc/passwd` : Compte le nombre de lignes dans `/etc/passwd` où le champ shell correspond.
- `done < /etc/shells` : Indique que la boucle doit lire les entrées de `/etc/shells`.

**Autre solution** :
```bash
cat /etc/shells | while read i; do echo "$(cat /etc/passwd | grep $i | wc -l) utilisateurs ont pour shell $i"; done
```

1. **`cat /etc/shells`**  
   → Affiche le contenu du fichier `/etc/shells` (liste des shells disponibles sur le système).  
2. **`| while read i; do ... done`**  
   → Lit chaque ligne du fichier `/etc/shells` et stocke la valeur dans la variable `i`.  
3. **`cat /etc/passwd | grep $i | wc -l`**  
   - `cat /etc/passwd` : Affiche le contenu du fichier `/etc/passwd` (liste des utilisateurs avec leur shell).  
   - `grep $i` : Filtre les lignes contenant le shell `i`.  
   - `wc -l` : Compte le nombre de lignes correspondantes (donc le nombre d’utilisateurs utilisant ce shell).  
4. **`echo "$( ... ) utilisateurs ont pour shell $i"`**  

    
L’utilisation de `cat` avant `grep` est inutile et moins efficace que la solution précédente.  


--- 

## Exercice 3

1. En une seule ligne de commande, on veut savoir combien de **fichiers et dossiers** contient le répertoire courant.
```bash
$ echo "Le répertoire `basename $PWD` contient $(find . ! -path . | wc -l) fichiers et dossiers"
```

**Explication** :
- **`find . ! -path .`** → Recherche **tout** dans le répertoire courant, sauf `.` (le dossier courant lui-même).
- **`wc -l`** → Compte le nombre d'éléments trouvés.
- **`basename $PWD`** → Affiche uniquement le **nom** du répertoire courant.
- **`echo`** → Formate le message de sortie.


2. En une seule ligne de commande, on veut savoir combien de **fichiers standards** contient le répertoire courant. Le résultat doit être affiché comme suit :
```bash
$ echo "Le répertoire $(pwd) contient $(ls -l | grep ^- | wc -l) fichiers standard";
```

3. En une seule ligne de commande, on veut savoir combien d’éléments ne sont **ni des dossiers ni des fichiers standards** dans le répertoire courant.
```bash
$ echo "Le répertoire $(pwd) contient $(ls -l | grep -v ^d | grep -v ^- | wc -l) fichiers qui ne sont ni des fichiers standards ni des répertoires"
```

4. Écrire une commande qui récupère le nom du **dernier utilisateur** qui a été créé sur votre machine (c'est celui qu'on retrouve à la **dernière ligne** du fichier `/etc/passwd`). Le résultat doit être stocké dans une variable nommée `nomUtilisateur`.
```bash
$ nomUtilisateur=$(tail -n 1 /etc/passwd | cut -d: -f1)
```

**Explication** :
-  `tail -n 1 /etc/passwd` → Récupère la dernière ligne du fichier `/etc/passwd`, qui contient les informations du dernier utilisateur créé.
- `cut -d: -f1` → Coupe la ligne en utilisant `:` comme délimiteur et extrait le premier champ, qui correspond au nom de l’utilisateur.


5. En utilisant la variable `nomdurépertoire` qui contient le nom du dernier utilisateur défini dans `/etc/passwd`, écrivez une commande permettant de :
    - Rechercher tous les fichiers à partir de `/home` (*find*)
    - Lister leurs détails avec `ls -l`
    - Filtrer uniquement les fichiers appartenant à cet utilisateur.
    - Filtrer uniquement les fichiers standards. 
    - La commande doit être une seule ligne en utilisant un pipe (`|`) et une boucle `while read`.
```bash
$ find /home -type f -user "$nomUtilisateur" 2>/dev/null | while read fichier; do ls -ld "$fichier"; done
```

**Explication** :
- `find / -type f -user "$nomUtilisateur" 2>/dev/null`  
   - `find /home` → Recherche dans tout le répertoire `/home` et ses sous dossiers.  
   - `-type f` → Filtre pour ne garder que les fichiers standards (exclut les dossiers et autres types de fichiers).  
   - `-user "$nomUtilisateur"` → Sélectionne uniquement les fichiers appartenant à l’utilisateur défini dans la variable `nomUtilisateur`.  
   - `2>/dev/null` → Supprime les messages d'erreur liés aux permissions pour éviter qu'elles s'affichent.  

- `| while read fichier; do ls -ld "$fichier"; done`  
   - Lit chaque fichier trouvé, stockant chaque chemin de fichier dans la variable `fichier`.  
   - Utilise `ls -ld` pour afficher les détails du fichier (-l pour le format détaillé, -d pour éviter de suivre les liens symboliques).

**Autre solution non optimale**
```bash
find /home -name "$user" 2>/dev/null |while read i; do ls -ld $i ; done |grep ^-  
```
---

## Exercice 4

1. En tant qu’utilisateur standard, on veut trouver tous les fichiers `.txt` sur votre disque dur (**ne pas utiliser `sudo`**). Écrire la commande qui permet de retrouver cette information **sans afficher les erreurs**.
```bash
$ find / -type f -name "*.txt" 2>/dev/null
```

**Explication** :
- `find /` → Recherche à partir de la racine du système.  
- `-type f` → Filtre pour ne garder que les fichiers standards.  
- `-name "*.txt"` → Cherche uniquement les fichiers avec l'extension `.txt`.
- `2>/dev/null` → Redirige les erreurs (par exemple, permissions refusées) vers `/dev/null`, les rendant invisibles.  


2. Récupérer la sortie standard de la commande précédente et à partir de son résultat, **lire chaque ligne** et à l'aide de la commande `ls`, afficher la taille de ces fichiers suivi du chemin vers les fichiers.(**en une seule commande sans utiliser de variable**).
```bash
$ find / -type f -name "*.txt" 2>/dev/null | while read fichier; do ls -l "$fichier" | tr -s ' ' | cut -d' ' -f5,9-; done
```

**Explication** :
- `find / -type f -name "*.txt" 2>/dev/null`  
   - Recherche tous les fichiers `.txt` accessibles.  
   - Ignore les erreurs de permission.  

- `| while read fichier; do ls -l "$fichier" | tr -s ' ' | cut -d' ' -f5,9-; done`  
   - Lit chaque fichier trouvé.  
   - `ls -l "$fichier"` affiche les détails du fichier.  
   - `tr -s ' '` compresse les espaces multiples en un seul espace pour éviter les décalages dans `cut`.  
   - `cut -d' ' -f5,9-` extrait :
     - `-f5` → La taille du fichier (5ᵉ champ).  
     - `-f9-` → Extrait le chemin du fichier (le nom commence au 9ᵉ champ).  


3. Récupérer la sortie standard de la commande précédente et **trier** le résultat par **ordre croissant de taille**. (**en une seule commande sans utiliser de variable**).
```bash
$ find / -type f -name "*.txt" 2>/dev/null | while read fichier; do ls -l "$fichier" | tr -s ' ' | cut -d' ' -f5,9-; done | sort -n
```

**Explication** :  
- `| sort -n`  
   - Trie les résultats par ordre croissant de taille (`sort -n` pour tri numérique).  

**Autres solutions**
```bash
$ find / -name "*.txt" 2>/dev/null| while read i; do du -sh $i; done | sort -h
```

**Explication**
- `while read i` → Lit chaque ligne de la sortie de find, stockant chaque chemin de fichier dans i.
- `du -sh $i` →
   - `du` (Disk Usage) mesure la taille du fichier.
   - `s` → Affiche uniquement la taille totale du fichier, sans détails supplémentaires.
   - `h` → Formate la taille en unités lisibles (K, M, G).
- `sort -h` → Trie les fichiers par taille, en interprétant correctement les suffixes (K, M, G).
- Sans `-h`, le tri serait incorrect pour des valeurs comme 512K et 1.2M (car sort classerait alphabétiquement).


```bash
$ find / -name "*.txt" 2>/dev/null | while read fichier; do ls -lh $fichier; done |sort -t' ' -k5h
```

**Explication**
- `ls -lh $fichier` → Affiche les détails du fichier (ls -l), mais avec -h pour afficher la taille dans un format lisible (Ko, Mo, Go).