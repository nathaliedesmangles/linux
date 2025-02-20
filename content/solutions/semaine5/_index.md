+++
title = "Atelier 5"
weight = 165
draft = true
+++

# Solution des exercices


## Exercice 1 : nombre_de_fichiers_seq.sh`

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
