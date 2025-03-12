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
- Utiliser **uniquement** les commandes, les symboles et la matière vue dans le cours (semaines 1 à 6)
	- [RegExp: Tableaux récapitulatifs](https://linuxh25.netlify.app/semaine6/cours/recapitulatif)
{{% /notice %}}

---

**Dans le fichier `expr.txt` fourni, à l'aide d'expressions régulières**:

1. Trouvez les codes postaux canadiens :
	- Format attendu : `Lettre-Chiffre-Lettre Chiffre-Lettre-Chiffre`.

2. Identifiez les codes d’employés composés de :
	- Deux lettres majuscules suivies de quatre chiffres.

3. Comptez les lignes **ne se terminant pas** par une lettre :

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

**Dans le fichier `/etc/services`, à l'aide d'expressions régulières**: 

7. Trouver les lignes contenant "ssh" sans espace après.

8. Compter les lignes totales et celles non vides.

9. Trouver les lignes contenant `udp` ou `tcp` avec un numéro à trois chiffres.

10. Rechercher les mots de quatre lettres entourés d'espaces.

11. Identifier les mots avec exactement deux "a" (**consécutifs ou non**).

---

**Dans le fichier `/etc/passwd`, à l'aide d'expressions régulières**: 

12. 
	a) Avec une première commande, comptez le nombre de lignes du fichier `/etc/passwd`. <br>
	b) Avec une deuxième commande, assurez-vous ensuite que toutes les lignes contiennent deux nombres successifs, chacun valant de 0 à n (nombre entier de plusieurs chiffres) et entouré de ":". <br>
	c) Comptez le nombre de lignes obtenues et assurez-vous qu’il est égal au nombre précédent.

13. Compter les nombre d'utilisateurs qui n'ont pas le shell bash. <br>
**Rappel**: Dans le fichier `/etc/passwd`, chaque ligne correspond à un utilisateur.


