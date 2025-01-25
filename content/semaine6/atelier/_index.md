+++
title = "ATELIER #6: Les expressions régulières"
weight = 62
+++

## Objectif de l'atelier

- Maîtriser les bases des expressions régulières.
- Renforcer la capacité à manipuler des fichiers texte.
- Renforcer la précision dans la recherche et le filtrage de données.
---

# Atelier

{{% notice style="important" title="Important" %}}
- Utiliser le fichier `expr.txt` se trouvant sur Moodle.
- Utiliser seulement la matière vue dans le cours (semaines 1 à 6).
- Utiliser des expressions régulières courtes et simples au lieu d'expressions complexes et longues.
{{% /notice %}}


**Dans le fichier fourni**:

1. Trouvez les codes postaux canadiens :
   - Format attendu : Lettre-Chiffre-Lettre Chiffre-Lettre-Chiffre.

2. Identifiez les codes d’employés composés de :
   - Deux lettres majuscules suivies de quatre chiffres.

3. Comptez les lignes ne se terminant pas par une lettre :

4. Identifier les numéros de téléphone aux formats : `(xxx)xxx-xxxx` ou `+1(xxx)xxx-xxxx`.

5. Trouver les URLs comme :

- `http://www.domaine.tld` ou `http://www.domaine.tld/`
- `https://www.domaine.tld` ou `https://www.domaine.tld/`

6. Rechercher des adresses e-mail valides. Elles contiennent :
 - des lettres majuscules ou minuscules, 
 - des chiffres et 
 - possiblement un ou plusieurs '_' (tiret bas) et 
 - un ou plusieurs '.' . 
 - Ensuite il y a forcément un '@' puis 
 - d’autres caractères (lettres majuscules ou minuscules, chiffres, '.', tiret bas '_') 
 - Ensuite il y a obligatoirement un '.' puis pour finir, 
 - Entre 2 et 6 lettres minuscules (.qc.ca) et 
 - Possiblement un '.' à la fin 

---

**Dans le fichier `/etc/services`**: 

7. Trouver les lignes contenant "ssh" sans espace après.

8. Compter les lignes totales et celles non vides.

9. Trouver les lignes contenant soit `udp` soit `tcp` avec un numéro à trois chiffres.

10. Rechercher les mots de quatre lettres entourés d'espaces.

11. Identifier les mots avec exactement deux "a".

---

**Dans le fichier `/etc/passwd`**: 

12. Assurez-vous que toutes les lignes contiennent deux nombres entre ":".

13. Compter les utilisateurs sans bash comme shell.


