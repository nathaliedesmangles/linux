+++
title = "Commandes Entrées/Sorties, redirection, filtres, pipeline des commandes et while"
weight = 41
+++

Les concepts d'entrées/sorties, de redirection, de filtres, de pipelines et l'utilisation des boucles pour automatiser des tâches sont des bases essentielles pour manipuler efficacement des données.

## Les entrées et sorties des commandes

### Qu'est-ce que l'entrée (input) ?

L'entrée (standard input ou `stdin`) est une source d'information qu'une commande peut utiliser. Par défaut, l'entrée provient du **clavier**.

### Qu'est-ce que la sortie (output) ?

La sortie (standard output ou `stdout`) est l'endroit où une commande affiche ses résultats. Par défaut, cette sortie s'affiche dans le **terminal**.

### Qu'est-ce que la sortie d'erreur (stderr) ?

La sortie d'erreur (standard error ou `stderr`) est où les messages d'erreur sont affichés. Par défaut, elle s'affiche également dans le **terminal**.

---

## La redirection

La redirection permet de changer la source d'entrée ou la destination des sorties pour enregistrer ou réutiliser des données facilement.

{{% notice style="info" title="Information" %}}
Nous ne verrons pas la redirection à l’aide de `<`.
Cependant, vous pouvez rediriger `stdin` pour lire des données à partir d'un fichier ou d'une autre commande, en récupérant la sortie standard d’une autre commande grâce au pipeline (vu plus loin).
{{% /notice %}}

### Rediriger la sortie standard (***stdout***)

Pour envoyer le résultat d'une commande dans un fichier :
```bash
commande > fichier.txt
```
Exemple :
```bash
$ echo "Bonjour !" > bonjour.txt
```

### Ajouter à un fichier existant

Pour ajouter une sortie à la fin d'un fichier existant **sans écraser** son contenu :
```bash
commande >> fichier.txt
```
Exemple :
```bash
$ echo "Encore une ligne." >> bonjour.txt
```

### Rediriger la sortie standard avec ***1>***

La redirection explicite de `stdout` s'écrit :
```bash
commande 1> fichier.txt
```
Ceci a le même effet que `>`.

### Rediriger la sortie d'erreur (***stderr***)

Pour enregistrer les erreurs dans un fichier :
```bash
commande 2> erreurs.txt
```

### Combiner ***stdout*** et ***stderr***

Pour rediriger les deux vers un même fichier :
```bash
commande > fichier.txt 2>&1
```
Pour rediriger la sortie d’erreur standard vers la sortie standard et envoyer le tout dans un fichier 
```bash
$ find / -name services >resultats.txt 2>&1
```
### Redirection vers ***/dev/null***

Pour ignorer la sortie d'une commande, vous pouvez la rediriger vers `/dev/null` :
```bash
commande > /dev/null
```

Exemple :
```bash
$ ls dossier_inexistant > /dev/null 2>&1
```

Ici, la commande `ls` tente d'afficher le contenu d'un dossier inexistant, et ses messages (sortie standard et erreurs) sont redirigés vers `/dev/null` pour être ignorés.

### Utiliser un fichier comme entrée

Pour utiliser un fichier comme source d'entrée :
```bash
commande < fichier.txt
```
Exemple :
```bash
$ sort < liste.txt
```

Exercices 1 : Entrées/Sorties

1. Sans être root et sans utiliser `sudo`, rechercher le fichier services sur tout le disque dur.
- Est-ce facile de le trouver dans la sortie de la commande ?
2. Faites la même recherche mais en redirigeant les lignes “Accès refusé” vers le fichier `/dev/null`.
- Est-ce plus facile de trouver le résultat de la commande ?
- Sauvegardez le résultat dans le fichier `~/services.txt` à l’aide d’une redirection.

---

## Les filtres

Un filtre est une commande qui traite une entrée pour produire une sortie modifiée. Voici les filtres les plus courants :

| Commande | Description | Options et descriptions |
|----------|-------------|--------------------------|
| `grep` | Recherche des lignes contenant un mot ou une expression. | `-i` : Ignore la casse \\n  `-r` : Recherche récursive\\n  `-v` : Inverse la recherche\\n  `-n` : Affiche les numéros de ligne |
| `sort` | Trie les lignes d'un fichier. | `-r` : Ordre inverse\\n  `-n` : Tri numérique\\n  `-k` : Tri par clé spécifique |
| `uniq` | Supprime les doublons dans une liste triée. | `-c` : Compte les occurrences\\n  `-d` : Affiche les doublons uniquement |
| `wc` | Compte le nombre de lignes, mots ou caractères. | `-l` : Compte les lignes\\n  `-w` : Compte les mots\\n  `-c` : Compte les caractères |
| `sed` | Modifie le contenu des lignes selon des motifs. | `-e` : Applique plusieurs commandes\\n  `-i` : Modifie en place |
| `find` | Recherche des fichiers ou dossiers selon des critères. | `-name` : Recherche par nom\\n  `-type` : Recherche par type (dossier ou fichier) |
| `cut` | Extrait des sections de chaque ligne d'un fichier. | `-d` : Spécifie le délimiteur\\n  `-f` : Spécifie les champs à extraire |
| `tr` | Traduit ou supprime des caractères. | `-d` : Supprime des caractères\\n  `-s` : Remplace des séquences répétées |

### Exemples

- **`grep`** : Recherche des lignes contenant un mot ou une expression.
  ```bash
  $ grep "mot" fichier.txt
  ```
- **`sort`** : Trie les lignes d'un fichier.
  ```bash
  $ sort fichier.txt
  ```
- **`uniq`** : Supprime les doublons dans une liste triée.
  ```bash
  $ sort fichier.txt | uniq
  ```
- **`wc`** : Compte le nombre de lignes, mots ou caractères.
  ```bash
  $ wc fichier.txt
  ```
- **`sed`** : Modifie le contenu des lignes selon des motifs.
  ```bash
  $ sed 's/ancien/nouveau/g' fichier.txt
  ```
  Exemple : Remplacer "erreur" par "avertissement" dans un fichier :
  ```bash
  $ sed 's/erreur/avertissement/g' journal.txt
  ```
- **`find`** : Recherche des fichiers ou dossiers selon des critères.
  ```bash
  $ find . -name "*.txt"
  ```
- **`cut`** : Extrait des sections de chaque ligne d'un fichier.
  ```bash
  $ cut -d':' -f1 fichier.txt
  ```
  Exemple : Extraire le premier champ d'un fichier où les champs sont séparés par des deux-points (:).
  ```bash
  $ cut -d':' -f1 liste.txt
  ```
- **`tr`** : Traduit ou supprime des caractères.
  ```bash
  $ tr 'a-z' 'A-Z' < fichier.txt
  ```
  Exemple : Convertir tout le texte en majuscules.
---

## Les pipelines

Les pipelines (ou "pipes") permettent de connecter plusieurs commandes ensemble. Le symbole `|` transmet la sortie d'une commande comme entrée à une autre.

### Exemples

1. 
```bash
$ cat fichier.txt | grep "mot" | sort
```
1. **`cat fichier.txt`** : Lit le fichier.
2. **`grep "mot"`** : Filtre les lignes contenant "mot".
3. **`sort`** : Trie les lignes filtrées.


2. Pour afficher les 5 mots les plus fréquents dans un texte :
```bash
cat texte.txt | tr -s ' ' '\n' | sort | uniq -c | sort -nr | head -5
```
1. **`tr -s ' '`** : Transforme les espaces multiples en simples et ajoute des sauts de ligne.
2. **`uniq -c`** : Compte les occurrences de chaque mot.
3. **`sort -nr`** : Trie par ordre décroissant des fréquences.
4. **`head -5`** : Affiche les 5 premiers.

3. Redirection de l'entrée standard (***<***)

Vous pouvez utiliser un fichier en entrée dans un pipeline. Par exemple, pour afficher les lignes contenant "erreur" dans un fichier trié :
```bash
$ grep "erreur" < journal.txt | sort
```


Exercices 2 : Filtres et pipe

- En utilisant le `|` et les filtres, trouvez le numéro de port de zephyr-srv dans le fichier `/etc/services`.
- Dans le fichier /etc/services, combien y a-t-il de lignes qui ne contiennent pas de e?
- Et combien de lignes ne contiennent ni e ni a ?
---

## Automatiser avec la boucle while

Les boucles permettent de répéter des commandes sur un ensemble d'éléments.

### Syntaxe de la boucle while

Voici la forme générale d'une boucle `while` en ligne de commande :

```bash
while [ condition ]; do
    # Actions à répéter
    commande1
    commande2
    ...
done
```

- **condition** : C'est ce que le programme vérifie à chaque fois.
- **do...done** : Tout le code entre `do` et `done` sera répété tant que la condition est vraie.

### Exemples

1. Compter de 1 à 5
```bash
compteur=1; while [ $compteur -le 5 ]; do echo "Compteur : $compteur"; compteur=$((compteur + 1)); done
```

- **`compteur=1`** : On commence avec le chiffre 1.
- **`[ $compteur -le 5 ]`** : La condition signifie "tant que le compteur est inférieur ou égal à 5".
- **`echo`** : Affiche le compteur.
- **`compteur=$((compteur + 1))`** : On ajoute 1 au compteur à chaque tour.

Affichera :
```
Compteur : 1
Compteur : 2
Compteur : 3
Compteur : 4
Compteur : 5
```

2. Lire un fichier ligne par ligne et afficher chaque ligne :
```bash
while read ligne; do
  echo "Ligne : $ligne"
done < fichier.txt
```
- **`read ligne`** : Lit chaque ligne du fichier.
- **`echo`** : Affiche le contenu de la ligne.

3. Renommer tous les fichiers `.txt` d'un répertoire pour ajouter le suffixe `_backup` :
```bash
find . -name "*.txt" | while read fichier; do
  mv "$fichier" "${fichier%.txt}_backup.txt"
done
```
- **`find`** : Trouve tous les fichiers `.txt`.
- **`mv`** : Renomme chaque fichier en ajoutant "_backup".

4. Demander un mot de passe à l'utilisateur
```bash
mot_de_passe="secret"; reponse=""; while [ "$reponse" != "$mot_de_passe" ]; do echo "Entrez le mot de passe :"; read reponse; done; echo "Mot de passe correct !"
```

- **`mot_de_passe="secret"`** : Le mot de passe attendu est "secret".
- **`read reponse`** : Demande à l'utilisateur de taper une réponse.
- **`[ "$reponse" != "$mot_de_passe" ]`** : Tant que la réponse n'est pas égale au mot de passe, la boucle continue.

Cette commande, demandera le mot de passe jusqu'à ce que l'utilisateur tapes "secret".

## Boucles infinie

{{% notice style="warning" title="Attention aux boucles infinies" %}}
- Si la condition ne devient jamais fausse, la boucle ne s'arrêtera pas. 
{{% /notice %}}

Par exemple :
```bash
$ while true; do echo "Ceci ne s'arrête jamais !"; sleep 1; done
```

{{% notice style="info" title="Information" %}}
- Utilise `Ctrl + C` pour arrêter une boucle infinie. 
{{% /notice %}}


Exercices 3 : While et autres commandes

- Recherchez tous les fichiers de configuration du système (on considère qu’ils se terminent par `.conf`) puis n’affichez que le nom du fichier sans le chemin.
- La commande `basename /rep1/rep2/…/fichier.txt` affiche seulement `fichier.txt`.
- Une fois l’exercice terminé, classez les résultats par ordre alphabétique.
- Avec une boucle `while`, parcourez le fichier `/etc/services` et pour chaque ligne, ne garder que le 1er champs en utilisant comme délimiteur `‘ ’` (espace).
- Une fois terminé, éliminez les doublons et comptez le nombre de lignes.

