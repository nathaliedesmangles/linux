+++
title = "Test 2"
weight = 182
+++

{{% notice style=info title=Information %}}
L'ordre des questions et des choix de réponses peut varier selon votre groupe.
{{% /notice %}}  


#### **Question 1.** Quelle option de la commande *tree* permet d'afficher uniquement les répertoires ?
- [x] `-d` ✅ Bonne réponse
- [ ] `-L`
- [ ] `-r`
- [ ] `-f`


#### **Question 2.** Que signifie l'option *-i* avec la commande *sed* ?
- [x] Modifier un fichier sans créer de fichier temporaire ✅ Bonne réponse
- [ ] Afficher le contenu du fichier
- [ ] Rechercher du texte
- [ ] Extraire des colonnes


#### **Question 3**. Quelle commande permet de forcer l'arrêt d'un processus en utilisant son PID ?
- [ ] `kill <pid>`
- [ ] `killall -9`
- [ ] `kill bill`
- [x] `kill -9 <pid>` ✅ Bonne réponse


#### **Question 4.** Quelle commande permet d'afficher le PID du dernier processus lancé en arrière-plan ?
- [x] `$!` ✅ Bonne réponse
- [ ] `$$`
- [ ] `$?`


#### **Question 5.** Quelle commande permet d'afficher tous les processus en cours d'exécution sur le système ?
- [x] `ps -ef` ✅ Bonne réponse
- [ ] `ps -f`
- [ ] `pid`
- [ ] `ppid`


#### **Question 6.** Quelle commande permet d'extraire la 3ᵉ colonne d'un fichier en utilisant la virgule comme séparateur ?  
**Réponse** :  
```bash
cut -d, -f3
```


#### **Question 7.** Quelle commande permet de rechercher toutes les lignes contenant le mot 'erreur' dans le fichier 'log.txt' ?  
**Réponse** :  
```bash
grep 'erreur' log.txt
```


#### **Question 8.** Quelle commande permet d'extraire la 2ᵉ colonne d'un fichier 'data.txt' (séparé par des espaces) et de rechercher les lignes contenant 'valeur' ? 
**Réponse** :  
```bash
cut -d' ' -f2 data.txt | grep 'valeur'
```


### **Question 9.** Quelle option doit-on ajouter à la commande *sort* pour trier des nombres correctement ?
**Réponse** :  
```bash
-n
```


#### **Question 10.** Quel sera le résultat du code suivant (ne tenez pas compte de l'absence du # sur la première ligne) ?
![code boucle](./while.png)
- [ ] Une erreur 
- [ ] rien
- [ ] Les chiffres de 0 à 5 sur une ligne (horizontal)
- [x] Les chiffres de 0 à 5 sur une colonne (vertical) ✅ Bonne réponse


#### **Question 11.** Vous devez effectuer une recherche de tous les fichiers ".log" dans `/etc/`. Vous voulez aussi  enregistrer tous les résultats de la recherche, y compris les éventuelles erreurs de permission, dans un fichier nommé **"fichiers_log.txt"**. Quelle commande utilisez vous pour effectuer cette recherche et rediriger à la fois la sortie standard et les erreurs vers le fichier "fichiers_log.txt" ?<br>
**Réponse** :  
```bash
find /etc/ -name "*.log"> fichiers_log.txt 2>&1
```


#### **Question 12.** Dans le répertoire `/etc`, vous devez compter le nombre de fichiers dont le nom contient le mot "test", en redirigeant les erreurs de la commande vers "/dev/null" . Quelle commande utiliserez vous ?
Réponse :
```bash
find /etc/ -name " test " 2>/dev/null | wc -l
```


#### **Question 13.** 
- Écrivez un script **bash** qui crée trois fichiers nommés `file1.txt`, `file2.txt` et `file3.txt`.
- Après la création de chaque fichier, le script vérifie son existence avec la commande *test* et affiche un message confirmant la création.
- Utilisez une boucle `while` pour gérer la création des fichiers 
**Réponse** :  
```bash
#!/bin/bash

i=1

while test $i -le 3

do

   touch "file$i.txt"

   test -f "file$i.txt" && echo "file$i.txt créé avec succès."

   i=$((i + 1))

done
```


#### **Question 14.** En glissant les choix aux bons endroits, complétez le script Bash ci-dessous qui parcourt 3 fichiers simultanément et compte le nombre de mots.

{{% notice style=warning title=ATTENTION %}}
Les crochets dans la solution, représentent les cases que vous deviez remplir. Il ne s'agit pas des crochets commande test, ni des crochets dans les expressions régulières.
{{% /notice %}} 
**Réponse** :  
```bash
[#!/bin/bash]

fichiers="fichier1.txt  fichier2.txt  fichier3.txt"

[for] f in $fichiers

do

    (

        [test] -e "$f" [&&] nb=$([wc ‑w] < "$f") [&&] 

        echo "Le fichier [$f] contient [$nb] mots." [|| ]

        echo "Le fichier [$f] n'existe pas."

    ) [&]

done

[wait]


echo "Tous les fichiers ont été traités."
```

##### Choix à caser :
- `#!/bin/bash`
- `for`
- `test`
- `&&`
- `wc -w`
- `$f`
- `$nb`
- `||`
- `&`
- `wait`


