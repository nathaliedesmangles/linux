+++
title = "Commandes utiles, redirection, chainage, filtres et boucle While"
weight = 41
+++

## Commandes diverses

{{% notice style="secondary" title="Information" %}}
Les guillemets simples (') ou doubles (") peuvent tous les deux être utilisés, lorsque des guillemets sont nécessaires.
{{% /notice %}}

### ***tree***: Afficher l'arborescence des dossiers

La commande `tree` affiche les fichiers et dossiers sous forme d'arborescence.

- L'option `-d` permet d'afficher uniquement les répertoires (et pas les fichiers).
- L'option `-L` permet de limiter l'affichage à N niveaux de profondeur.

   **Afficher uniquement les dossiers** :
   ```bash
   $ tree -d	# `d` pour directory
   ```

   **Afficher les dossiers d'un endroit précis** :
   ```bash
   $ tree /etc
   ```

   **Limiter l'affichage aux 2 premiers niveaux** :
   ```bash
   $ tree -L 2
   ```

---

### ***grep*** : Rechercher du texte dans un fichier

- L'option `-r` permet de rechercher de manière récursive dans un répertoire et tous ses sous-dossiers.
- Le caractère `^` est utilisé pour faire correspondre le début d'une ligne dans un fichier lorsqu'il est placé **au début** d'une chaine.

   **Trouver "ssh" dans `/etc/services`** :
   ```bash
   $ grep ssh /etc/services
   ```

   **Chercher dans tous les fichiers d'un dossier** :
   ```bash
   $ grep -r "ssh" /etc/
   ```

   **Chercher uniquement au début des lignes** :
   ```bash
   $ grep "^root" /etc/passwd
   ```

---

### ***sed***: Remplacer du texte dans un fichier

- Le préfixe `s` dans `sed` signifie substitution. Il est utilisé pour rechercher et remplacer une chaîne de caractères dans un fichier ou un flux de texte.
- L'option `-i` permet de modifier un fichier **sans créer de fichier temporaire**.
- Par défaut, `sed` ne remplace que la première occurrence d'un motif sur une ligne. En ajoutant `g`, il remplace toutes les occurrences.

```
`s/ancien/nouveau/`	# Remplace 'ancien' par 'nouveau' (`s` pour "substitute").
`s/ancien/nouveau/g`	# Remplace toutes les occurrences 'd'ancien' par 'nouveau' (`g` pour "global").
```    

 
   **Changer « root » en « admin » (affichage uniquement)** :
   ```bash
   $ sed 's/root/admin/' /etc/passwd
   ```

   **Changer toutes les occurrences** :
   ```bash
   $ sed 's/root/admin/g' /etc/passwd
   ```

   **Changer et enregistrer directement dans le fichier** :
   ```bash
   $ sed -i 's/ancienne_chaine/nouvelle_chaine/g' fichier_non_temporaire.txt
   ```

---

### ***cut***: Extraire des colonnes d'un fichier

- L'option `-d` permet de définir le **délimiteur** utilisé pour diviser les champs d'une ligne.
- L'option `-f` est utilisée pour sélectionner un ou plusieurs champs **après avoir défini un délimiteur** avec `-d`.

   {{% notice style="blue" title="Délimiteur par défaut" %}}
   Par défaut, `cut` utilise la **tabulation** comme délimiteur.
   {{% /notice %}}

   **Extraire le 6e champ d’un fichier où les champs sont séparés par `:`** :
   ```bash
   $ cut -d':' -f6 /etc/passwd
   ```

   **Extraire plusieurs colonnes (1re ET 3e)** :
   ```bash
   $ cut -d':' -f1,3 /etc/passwd
   ```

---

### ***more***: Lire un fichier page par page (ou ***less***)

- `more` affiche le fichier page par page, mais on ne peut pas remonter.
- `less` permet d’aller en avant et en arrière.

```bash
$ less /etc/passwd
```

**Commandes utiles dans `less`** :
- Aller en bas : `↓` ou `Entrée`
- Aller en haut : `↑`
- Aller au début du fichier : `g`
- Aller à la fin du fichier : `G`
- Descendre d'une page : `Espace`
- Monter d'une page : `b`
- Rechercher un mot : `/mot` puis `Entrée`
- Rechercher en arrière: `?mot` puis `Entrée`
- Aller à la prochaine occurrence : `n`
- Revenir à l’occurrence précédente : `N`
- Quitter : `q`

---

### ***sort***: Trier des lignes

- L'option `-k` permet de spécifier la colonne (ou champ) à utiliser pour le tri.
- L'option `-n` permet de trier des nombres correctement (plutôt qu’en mode texte).

   **Trier un fichier alphabétiquement** :
   ```bash
   $ sort fruits.txt
   ```

   **Trier par colonne (exemple : fichier avec noms et numéros)** :
   ```bash
   $ sort -k2 profs.txt
   ```

   **Trier numériquement (sinon, 10 est avant 2)** :
   ```bash
   $ sort -k2 -n data.csv
   ```

---

## Rediriger la sortie d’une commande

**Enregistrer la sortie dans un fichier avec `1>` ou `>`**:
```bash
$ find / -name services 1> resultats.txt
```

{{% notice style="info" title="Information" %}}
Ici, le chiffre `1` n'est pas obligatoire. Si on ne le met pas, la sortie standard est utilisée par défaut.
{{% /notice %}}

La commande précédente peut s'écrire aussi comme cela:
```bash
$ find / -name services 1> resultats.txt
```

**Ignorer les erreurs à l'aide de `2>`**:
```bash
$ find / -name services 2>/dev/null
```

**Envoyer sortie + erreurs dans un fichier en combinant `2>` et `1>`**:
```bash
$ find / -name services 1> resultats.txt 2>&1
```

**Ajouter du texte à un fichier sans l’écraser à l'aide de `>>`**:
```bash
$ echo "Bonjour" >> fichier.txt
```

---

## Enchaîner des commandes avec **|** (pipe)

Le `|` envoie le résultat d’une commande à une autre commande. La 2ème commande récupère le résultat de la 1ère commande pour travailler dessus.

Le nombre de commandes que l’on peut ainsi enchainer n’a pas de limite.

**Afficher le fichier avec `less`** :
```bash
$ cat /etc/services | less
```

**Chercher « ssh » dans un fichier et afficher** :
```bash
$ cat /etc/services | grep ssh
```

**Compter le nombre de lignes d’un fichier** :
```bash
$ cat fichier.txt | wc -l
```

### Exercice 1

1. Sans être `root` et sans utiliser `sudo`, rechercher le fichier `services` sur tout le disque dur.
 - Est-ce facile de le trouver dans la sortie de la commande ?

2. Faites la même recherche mais en redirigeant les lignes "Accès refusé" vers le fichier `/dev/null`.
 - Est-ce plus facile de trouver le résultat de la commande ?
 - Sauvegardez le résultat dans le fichier <code class="gr">~/services.txt</code> à l'aide d'une redirection.

{{% notice style="green" title="Solution" groupid="notice-toggle" expanded="false" %}}
```bash
$ find / -name services
```

C'est difficile de lire la sortie car les résultats sont noyés au milieu de nombreux messages d'erreurs.
![Find](find.png?height=200)

Pour rediriger les messages d'erreur:
```bash
$ find / -name services 2>/dev/null
```
Maintenant la lecture est beaucoup plus facile:
![Find2](find2.png?height=70)

Pour sauvegarder le résultat dans un fichier:
```bash
$ find / -name services 2>/dev/null >~/services.txt
```
{{% /notice %}}

---

## Les filtres

Enchainer des commandes permet d’appliquer de nombreux filtres sur le résultat d’une commande:

|Commande|Résutats|
|---|---|
|<code class="gr">cat fichier.txt \| wc -l</code>|Compte le nombre de lignes du fichier (<code class="gr">wc</code> : word count, <code class="gr">-l</code> pour les lignes)|
|<code class="gr">cat fichier \| grep [-iv] recherche</code>|Permet de garder (ou éliminer <code class="gr">-v</code>) les lignes contenant la recherche, sans tenir compte des majuscules <code class="gr">-i</code>.|
|<code class="gr">find / -name "*.conf" \| sort</code>|classe le résultat de la commande find par ordre alphabétique.|
|<code class="gr">cat /etc/passwd \| sed 's/root/admin/'</code>|Remplace la 1ère occurrence de root par admin dans l'affichage (pas dans le fichier)|
|<code class="gr">cat /etc/passwd \| cut -d':' -f1 \| sort</code>|Affiche uniquement le 1er champs de chaque ligne du fichier /etc/passwd en utilisant : comme séparateur de champs et les classe par ordre alphabétique.|

## D'autres commandes utiles

**Remplacer des lettres avec la commande `tr`**
```bash
$ echo sAlut | tr 'A' 'a'
salut
```

**Supprimer les doublons (nécessite `sort`) avec la commande `uniq`**
```bash
$ cat fichier | sort | uniq
```

**Transformer `$PATH` en liste triée**
```bash
$ echo $PATH | tr ':' '\n' | sort
```
Cela affiche chaque dossier du `PATH` sur une ligne et le trie.

### Exercice 2

1. Trouver le  **numéro de port** de `zephyr-srv` dans `/etc/services`.
2. Combien de lignes dans `/etc/services` **n'ont pas de `e`**?
3. Combien de lignes **n'ont ni `e` ni `a` ?

{{% notice style="green" title="Solution" groupid="notice-toggle" expanded="false" %}}
Pour trouver le numéro de port:
```bash
cat /etc/services | grep "zephyr-srv"
```

Le numéro du port est 2102.
Pour trouver le nombre de lignes ne contenant pas 'e':
```bash
cat /etc/services | grep -v e | wc -l
```

Pour les lignes ne contenant ni 'e' ni 'a':
```bash
cat /etc/services | grep -v e | grep -v a | wc -l
```
{{% /notice %}}

---

## La boucle ***while***

La boucle `while` permet de **traiter chaque ligne** d’une commande **une par une**.

La syntaxe de base d’une boucle while en Bash est la suivante :

```bash
while condition; do Commandes à exécuter tant que la condition est vraie; done
```
ou sur plusieurs lignes
```bash
while condition
do
    Commandes à exécuter tant que la condition est vraie
done
```

Exemple : connaître la taille de chaque dossier dans la variable d'environnement `$PATH`.
```bash
$ echo $PATH | tr ':' '\n' | while read i; do du -sh $i; done
```
 - `tr ':' '\n'` ➡ Remplace `:` par un saut de ligne.
 - `while read i; do ... done` ➡ Lit chaque ligne et exécute `du -sh` dessus.

**Résultat** : La taille de chaque dossier dans `$PATH`.

### Exercices 3

1. Recherchez tous les fichiers de configuration du système (on considère qu'ils se terminent par `.conf`) puis n'affichez que le nom du fichier sans le chemin.
 - La commande `basename /rep1/rep2/…/fichier.txt` affiche seulement `fichier.txt`.
 - Une fois l'exercice terminé, classez les résultats par ordre alphabétique.
2. Avec une boucle **while**, parcourez le fichier `/etc/services` et pour chaque ligne, ne garder que le 1er champs en utilisant comme délimiteur ` ` (espace).
 - Une fois terminé, éliminez les doublons et comptez le nombre de lignes.


{{% notice style="green" title="Solution" groupid="notice-toggle" expanded="false" %}}
**Première partie**:
Pour trouver les fichiers de configuration:
```bash
find / -name "*.conf" 2>/dev/null
```

Pour afficher seulement le nom sans le chemin:
```bash
find / -name "*.conf" 2>/dev/null | while read i; do basename "$i"; done
```

Pour classer par ordre alphabétique:
```bash
find / -name "*.conf" 2>/dev/null | while read i; do basename "$i"; done | sort
```

**Deuxième partie**:
```bash
cat /etc/services | while read i; do echo "$i" | cut -d' ' -f1 ; done
```

Pour enlever les doublons et compter le nombre de ligne:
```bash
cat /etc/services | while read i; do echo "$i" | cut -d' ' -f1 ; done | sort | uniq | wc -l
```
{{% /notice %}}
