+++
title = "Atelier 5"
weight = 175
draft = true
+++

# Solution des exercices


## Exercice 1 : nombre_de_fichiers_seq.sh`

### Solution 1

```bash
#!/bin/bash

# Définition des types de fichiers à analyser
types="java conf txt png tiff"

echo "Décompte des fichiers $types"
echo ""

# Boucle sur chaque type de fichier
for i in $types
do
	nb=$(find / -name "*.$i" 2>/dev/null | wc -l)
	test $nb -eq 0 && echo "Il n'y a aucun fichier .$i" || echo "Il y a $nb fichiers .$i"
done
```

### Solution 2

```bash
#!/bin/bash

# Définition des types de fichiers à analyser
types="java conf txt png tiff"

echo "Décompte des fichiers $types"
echo ""

# Boucle sur chaque type de fichier
for type in $types; do
    # Compter le nombre de fichiers avec l'extension donnée
    nombre=$(find . -type f -name "*.$type" | wc -l)

    # Affichage du résultat en utilisant des expressions arithmétiques
    echo "Il y a $nombre fichiers .$type" | sed 's/ 0 fichiers/ aucun fichier/'
done
```

---

## Exercice 2 : nombre_de_fichiers_conc.sh

### Solution 1

```bash
# Définition des types de fichiers à analyser
types="java conf txt png tiff"

echo "Décompte des fichiers $types"
echo ""

# Boucle sur chaque type de fichier (lancement en arrière-plan)
for i in $types
do
	(nb=$(find / -name "*.$i" 2>/dev/null | wc -l)
	test $nb -eq 0 && echo "Il n'y a aucun fichier .$i" || echo "Il y a $nb fichiers .$i")&
done

# Attendre la fin de tous les processus en arrière-plan
wait
```

### Solution 2

```bash
#!/bin/bash

# Définition des types de fichiers à analyser
types="java conf txt png tiff"

echo "Décompte des fichiers $types"
echo ""

# Boucle sur chaque type de fichier (lancement en arrière-plan)
for type in $types; do
    (
        nombre=$(find . -type f -name "*.$type" | wc -l)
        
        # Affichage avec substitution via `sed`
        echo "Il y a $nombre fichiers .$type" | sed 's/ 0 fichiers/ aucun fichier/'
    ) &
done

# Attendre la fin de tous les processus en arrière-plan
wait
```

{{% notice style=warning title=Attention %}}
Notez que lors des l’exécution des scripts en parallèle, l’ordre des résultats peut changer d’une exécution à l’autre, ceci montre que les différentes commandes sont bien exécutées de façon asynchrone, totalement indépendantes les unes des autres.
{{% /notice %}}


