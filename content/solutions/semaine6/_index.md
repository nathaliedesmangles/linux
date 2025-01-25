+++
title = "Atelier 6"
weight = 166
draft = true
+++

# Solutions des exercices

**Dans le fichier fourni: **

1. Trouver les codes postaux canadiens:
   - Format attendu : Lettre-Chiffre-Lettre Chiffre-Lettre-Chiffre.
     ```bash
     $ grep -E '\b[A-Z][0-9][A-Z] ?[0-9][A-Z][0-9]\b' expr.txt
     ```

2. Identifier les codes d’employés composés de :
   - Deux lettres majuscules suivies de quatre chiffres.
     ```bash
     $ grep -E '\b[A-Z]{2}[0-9]{4}\b' expr.txt
     ```

3. Compter les lignes **ne se terminant pas** par une lettre :
   ```bash
   $ egrep '[^a-zA-Z]$' expr.txt
   ```

4. **Identifier les numéros de téléphone :**
    - Format : `(xxx)xxx-xxxx` ou `+1(xxx)xxx-xxxx`.
   ```bash
   $ grep -E '\+1\([0-9]{3}\)[0-9]{3}-[0-9]{4}|\([0-9]{3}\)[0-9]{3}-[0-9]{4}' expr.txt
   ```

5. Trouver les URLs comme :
   - `http://www.domaine.tld` ou `http://www.domaine.tld/`
   - `https://www.domaine.tld` ou `https://www.domaine.tld/`

    ```bash
    $ egrep 'https?://[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}/?' fichier
    ```

6. Rechercher des adresses e-mail :
   ```bash
   $ egrep '\b[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}\b' fichier
   ```
---

**Dans le fichier `/etc/sercices`**

7. Trouver les lignes contenant "ssh" sans espace après.
   ```bash
   $ egrep 'ssh(?! )' /etc/services
   ```

8. Compter les lignes totales et celles non vides.
   - Total : 
   ```bash
   $ wc -l /etc/services
   ```
   - Non vides : 
   ```bash
   $ egrep -v '^$' /etc/services | wc -l
   ```

9. Trouver les lignes contenant soit `udp` soit `tcp` avec un numéro à trois chiffres.
   ```bash
   $ egrep '(udp|tcp).*\b[0-9]{3}\b' /etc/services
   ```

10. Rechercher les mots de quatre lettres entourés d'espaces.
   ```bash
   $ egrep '\b[a-zA-Z]{4}\b' /etc/services
   ```

11. Identifier les mots avec exactement deux "a".
   ```bash
   $ egrep '\b[^ ]*a[^ ]*a[^ ]*\b' /etc/services
   ```
---

**Dans le fichier /etc/passwd**

12. **Assurez-vous que toutes les lignes dans `/etc/passwd` contiennent deux nombres entre ":" :**
   ```bash
   $ egrep ':[0-9]+:[0-9]+:' /etc/passwd
   ```

13. Compter les utilisateurs sans bash comme shell.
    ```bash
    $ egrep -v '/bash$' /etc/passwd | wc -l
    ```