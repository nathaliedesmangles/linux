+++
title = "Les processus de Linux"
weight = 51
+++


## Les processus

Chaque application, chaque commande est un processus.

Certains processus vont s'exécuter jusqu'à ce que vous les arrêtiez, d'autres vont réaliser une tâche et s'arrêter tout seul.

> **Exemple:**

| Commande | Comportement |
|----------|-------------|
| `ls` | S'exécute et se termine immédiatement. |
| `firefox` | Ouvre Firefox et reste en exécution empêchant l'utilisation du terminal, jusqu'à la fermeture de Firefox. |

Quand une commande empêche l'utilisation du terminal pendant son exécution, elle s'exécute au **premier plan**.

Pour permettre l'utilisation du terminal, il faut lancer l'application bloquante en **arrière-plan**.

### Exécution en arrière-plan

Deux possibilités :

1. **Au lancement** : Ajouter `&` à la fin de la commande :
   ```bash
   $ firefox &
   ```
2. **Après lancement** :
   - Suspendre avec `Ctrl-z`
   - Reprendre en arrière-plan avec `bg`
   - Repasser au premier plan avec `fg`


### Exercice 1

Lancez Firefox, passez-le en arrière-plan et ramenez-le au premier plan.

{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
```bash
$ firefox &  # Lancement en arrière-plan
$ fg         # Ramène au premier plan
```

Pour arrêter une commande au premier plan : `Ctrl-c`
{{% /notice %}}


## Affichage et gestion des processus

Chaque processus est identifié par :

| Identifiant | Description |
|-------------|------------|
| `pid` | Identifiant unique du processus. |
| `ppid` | Identifiant du processus parent. |

> **Exemple:**
>
> Si vous lancez une commande à partir du terminal, celui-ci est le parent du processus créé.


| Commande | Description |
|----------|------------|
| `ps -f` | Affiche les processus en cours d'exécution depuis le terminal. |
| `ps -ef` | Affiche les détails de tous les processus du système. |
| `pstree` | Affiche l’arborescence des processus. |
| `top` | Affiche les processus en temps réel. |
| `kill pid` | Termine un processus avec son `pid`. |
| `kill -9 pid` | Termine immédiatement un processus. |
| `killall nom_processus` | Termine tous les processus portant un certain nom. |


### Exercice 2

Utilisez `ps` pour :
- Noter le `pid` de votre shell.
- Lancer Firefox an **arrière-plan** et observer son `pid` ainsi que son `ppid`.

{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
```bash
$ ps -ef | grep bash
$ firefox &
$ ps -ef | grep firefox  # Trouver le PID et PPID
```
Le `pid` du parent de Firefox doit être le `pid` de votre SHELL.
{{% /notice %}}


## États des processus

![États des processus](etats.png?width=50vw)

| État | Description |
|------|------------|
| **Élu** | En cours d'exécution sur le processeur. |
| **Prêt** | En attente d'exécution, sans attente de ressource. |
| **Bloqué** | En attente d'une ressource autre que le processeur. |
| **Zombie** | Terminé mais non encore récupéré par son processus parent. |

Ces états sont gérés par l’**ordonnanceur**.

{{% notice style="primary" title="L'ordonnanceur" %}}
C'est la partie du noyau du système d'exploitation **responsable du choix du processus élu qui va pouvoir bénéficier du service du processeur** (et globalement toutes les tâches annexes qui en découlent). Cette tâche se nomme **l'ordonnancement**.
{{% /notice %}}

### Exercice 3

- Lancez Firefox en arrière-plan et notez son `pid` et `ppid`.
- Tuez son parent.
- Quel est le `ppid` de Firefox maintenant ?

{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
```bash
$ firefox &
$ ps -ef | grep firefox  # Noter PID et PPID
$ kill -9 <PPID>  # Tuer le parent
$ ps -ef | grep firefox  # Observer le nouveau PPID (probablement systemd, ou une  instance)
```
Le `ppid` de firefox est le `pid` de votre terminal.
{{% /notice %}}

{{% notice style="green" title="Comment se nomme le processus 1?" groupid="notice-toggle" expanded="false" %}}
***init***
{{% /notice %}}


## Exécution persistante des processus

Si un terminal est fermé, ses processus sont arrêtés. Pour éviter cela :

| Commande | Effet |
|----------|-------|
| `disown <pid>` | Si le processus est en cours, il se détachera de son terminal. |
| `nohup <commande>` | Lance une commande en ignorant les signaux de fermeture du terminal. |

### Exercice 4

1. Exécuter `grep <fichier>`, puis: 
   - Noter que cette commande ne se termine pas.
   - Ouvrir un autre terminal.
   - Trouver le `pid` de la commande `grep`.
   - Tuer la commande.


2. Ouvrir un nouveau terminal, 
   - a) Lancer Firefox en arrière-plan, fermer le terminal. Que se passe-t-il ?
   - b) Exécuter `disown <pid firefox>`, puis lancer Firefox en arrière-plan, fermer le terminal. Que se passe-t-il ?
   - c) Exécuter `nohup firefox`, puis lancer Firefox en arrière-plan, fermer le terminal. Que se passe-t-il ?


{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
**1**
```bash
$ grep fichier
$ ps -ef | grep egrep  # Trouver le PID de egrep
$ kill -9 <PID de egrep>  # Terminer depuis un autre terminal
```
**2 a)**
```bash
$ firefox &
```
Après avoir fermé le terminal, Firefox se ferme aussi.

**2 b)**
```bash
$ disown <PID>
$ firefox &
```
**2 c)**
```bash
$ nohup 
$ firefox &
```
Avec l'utilisation de `disown` et `nohup`, le terminal peut être fermé mais Firefox reste ouvert.
{{% /notice %}}


## Codes de retour et variables système

| Variable | Description |
|----------|------------|
| `$?` | Code de retour de la dernière commande (0 = succès, autre = erreur). |
| `$!` | `PID` de la dernière commande exécutée en arrière-plan. |

> **Exemple:**
>
> ```bash
> $ test -e fichier   
> $ echo $?  # Affiche 0 si le fichier existe, un autre chiffre sinon
> ```

### Exercice 5

1. Lancez `ls`. Quel est son code de retour ? Est-ce un succès ou un échec ?
2. Lancez `find / -name "*.conf"` sans être root. Quel est le code de retour ? Pourquoi ?

{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
**1.**
```bash
$ ls
$ echo $?
```
Le code de retour est 0, car `ls` se termine avec succès.

**2.**
```bash
$ find / -name "*.conf"
$ echo $?  # Probablement 1 à cause des permissions
```
Le code de retour est différent de 0 (probablement 1), car il y a eu  une erreur (permission: accès refusé)
{{% /notice %}}


## Opérateurs de comparaison en Bash

Les opérateurs de comparaison permettent de tester des valeurs numériques dans des conditions.

| Opérateur | Signification | Exemple |
|-----------|--------------|---------|
| `-eq` | Égalité (`equal`) | `test $var -eq 0` |
| `-ne` | Différence (`not equal`) | `test $var -ne 0` |
| `-lt` | Strictement inférieur (`less than`) | `test $var -lt 0` |
| `-gt` | Strictement supérieur (`greater than`) | `test $var -gt 0` |
| `-le` | Inférieur ou égal (`less or equal`) | `test $var -le 0` |
| `-ge` | Supérieur ou égal (`greater or equal`) | `test $var -ge 0` |

## Attente de la fin d'exécution d'une commande

Il est possible d'attendre qu'une commande en arrière-plan se termine avant de poursuivre l'exécution d'autres commandes.

> **Exemple :**

```bash
$ cp dossierVolumineux/* destination &
$ wait $!
```

`wait`  attend que la copie en arrière-plan soit terminée avant de poursuivre.

Dans un script, on peut attendre plusieurs commandes exécutées en arrière-plan :

```bash
#!/bin/bash
cp dossier1/* destination1 &
cp dossier2/* destination2 &
wait 
echo "Toutes les copies sont terminées."
```

## Combinaison et synchronisation des commandes

### Opérateurs logiques

| Opérateur | Exemple | Fonctionnement |
|-----------|---------------|-----------------|
| `;` | `$ commande1 ; commande2` | `commande2` s’exécute une fois que `commande1` se termine, indépendamment du succès ou de l'échec. |
| `&` | `$ commande1 & commande2 &` | Les commandes s'exécutent en parallèle, simultanément. |
| `&&` | `$ commande1 && commande2` |`commande2` s’exécute si `commande1` réussit. |
| `\|\|` | `$ commande1 \|\| commande2` | `commande2` s’exécute si `commande1` échoue. |

> **Exemples :**

Tester l'existence d'un fichier avant d'exécuter une commande :
```bash
$ test -e fichier && commande
```

Afficher "OK" si la commande réussit :
```bash
$ commande && echo "OK"
```

Afficher "ERREUR" si la commande échoue :
```bash
$ commande || echo "ERREUR"
```

Afficher "OK" si la commande réussit, sinon "ERREUR" :
```bash
$ test $var -eq 0 && echo "OK" || echo "ERREUR"
```

C'est l'équivalent d'un SI var = 0 ALORS affiche "OK", SINON affiche "ERREUR". 

### Exercice 6 : Expérimentation des opérateurs logiques

1. Exécutez :
   ```bash
   $ find / -name "*.conf" && ls
   ```
   - Les deux commandes s'exécutent elles ? Inversez-les et observez le résultat.

2. Exécutez :
   ```bash
   $ find / -name "*.conf" || ls
   ```
   - Les deux commandes s'exécutent elles ? Inversez-les et observez le résultat.

3. Exécutez :
   ```bash
   $ find / -name "*.conf" & ls &
   ```
   - Les deux commandes s'exécutent elles en parallèle ?


{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
```bash
$ find / -name "*.conf" && ls 
```
`ls` s'exécute si `find` réussit.

```bash
$ find / -name "*.conf" || ls
```
`ls` s'exécute si `find` échoue

```bash
$ find / -name "*.conf" & ls &
```
Les deux commendes s'exécutent simultanément.
{{% /notice %}}


## Priorité des opérateurs

On peut utiliser des parenthèses pour organiser l'ordre d'exécution des opérateurs :

> **Exemple :**

```bash
$ (find / -name "*.conf" 2>/dev/null || ls) | grep a
```

Dans cet exemple :
- `find` est exécuté en premier. Si une erreur survient, `ls` prend le relais.
- Ensuite, `grep` filtre les résultats.

Si on écrit :

```bash
$ find / -name "*.conf" 2>/dev/null || (ls | grep a)
```

Seul le résultat de `ls` sera filtré par `grep` en cas d'échec de `find`.

## Création et exécution d'un script Bash

Un script Bash est un fichier `.sh` contenant une série de commandes.

### Création d'un script

1. Ouvrir un fichier avec Vim :
   ```bash
   $ vim monscript.sh
   ```
2. Ajouter l'en-tête (1re ligne) du script :
   ```bash
   #!/bin/bash
   ```
   Elle n'est pas obligatoire, mais **pour ce cours**, cette ligne DOIT TOUJOURS être présente. Il faut aussi comprendre son utilité.
3. Écrire les commandes et ajouter des commentaires (précédés de `#`).

> **Exemple : fichier monscript.sh**

```bash
#!/bin/bash
echo "Bonjour tout le monde"
pwd
touch fiche{1..5}.txt
```

### Exécution d'un script

```bash
$ bash chemin_vers_monscript.sh
```

## Scripts concurrents

Un script concurrent contient des commandes exécutées **en arrière-plan**.

> **Exemple :**

```bash
#!/bin/bash
(echo "Début copie dossier 1"; cp dossier1/* destination1; echo "Fin copie") &
(echo "Début copie dossier 2"; cp dossier2/* destination2; echo "Fin copie") &
wait
echo "Toutes les copies sont terminées."
```

Dans cet exemple :
- Chaque copie est lancée en arrière-plan avec `&`.
- `wait` garantit que le script affiche "Toutes les copies sont terminées" uniquement après la fin des copies.

Un autre exemple avec `sleep` :

```bash
#!/bin/bash
(sleep 15; echo "Pause de 15 secondes terminée") &
(sleep 20; echo "Pause de 20 secondes terminée") &
(sleep 3; echo "Pause de 3 secondes terminée") &
wait
echo "Réveillez-vous, toutes les pauses sont terminées !"
```
Ce script Bash lance trois commandes `sleep` en parallèle, chacune suivie d'un message indiquant la fin de la pause.  

**Explication** :
1. **Lancement en arrière-plan (`&`)** :  
   - `sleep 15` attend 15 secondes avant d'afficher "Pause de 15 secondes terminée".  
   - `sleep 20` attend 20 secondes avant d'afficher "Pause de 20 secondes terminée".  
   - `sleep 3` attend 3 secondes avant d'afficher "Pause de 3 secondes terminée".  

   Chaque commande est exécutée en arrière-plan grâce au `&`, ce qui signifie qu'elles démarrent immédiatement et ne bloquent pas l'exécution du script.

2. **`wait`** :  
   - Cette commande attend que **toutes** les tâches en arrière-plan soient terminées avant de poursuivre.

3. **Affichage final** :  
   - Une fois toutes les pauses terminées, appuyer sur `Entrée`, le script affiche `"Réveillez-vous, toutes les pauses sont terminées !"`.


### Exercice 7

1. Exécutez un script avec `sleep 15`, `sleep 20`, et `sleep 3` en parallèle.
2. Dans quel ordre s'afficheront les messages ?
3. Que se passe-t-il si vous retirez `wait` ?

{{% notice style="green" title="Solution..." groupid="notice-toggle" expanded="false" %}}
2. L'ordre d'affichage:
- Après **3 secondes** → `"Pause de 3 secondes terminée"`
- Après **15 secondes** → `"Pause de 15 secondes terminée"`
- Après **20 secondes** → `"Pause de 20 secondes terminée"`
- Enfin, lorsque toutes les commandes sont terminées → `"Réveillez-vous, toutes les pauses sont terminées !"
3. Si on enlève `wait`, le script pourrait afficher immédiatement le dernier message avant la fin des `sleep`.
{{% /notice  %}}

`





