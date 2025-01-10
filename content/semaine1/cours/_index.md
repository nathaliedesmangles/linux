+++
title = "Qu'est-ce que Linux ?"
weight = 11
+++

## Qu'est-ce qu'un système d'exploitation?

Un système d'exploitation (SE) est un logiciel essentiel qui agit comme un intermédiaire entre l'utilisateur et le matériel de l'ordinateur. Il gère les ressources matérielles et logicielles de l'ordinateur et fournit des services communs pour les programmes informatiques. Voici quelques-unes de ses principales fonctions:

1. **Gestion des ressources matérielles**: Le système d'exploitation contrôle et coordonne l'utilisation du processeur, de la mémoire, des périphériques de stockage, et des périphériques d'entrée/sortie comme le clavier, la souris et l'écran.

2. **Gestion des fichiers**: Il organise les données en fichiers et dossiers, permettant aux utilisateurs de stocker, récupérer et manipuler des informations de manière efficace.

3. **Gestion des processus**: Le système d'exploitation gère l'exécution des programmes, en allouant du temps processeur et en assurant que les tâches s'exécutent sans conflit.

4. **Interface utilisateur**: Il fournit une interface utilisateur, qui peut être en ligne de commande (CLI) ou graphique (GUI), permettant aux utilisateurs d'interagir facilement avec l'ordinateur.

5. **Sécurité et gestion des utilisateurs**: Le système d'exploitation protège les données et les ressources de l'ordinateur contre les accès non autorisés et permet la gestion des comptes utilisateurs.

## Exemples de systèmes d'exploitation

- **Windows**: Développé par Microsoft, c'est l'un des systèmes d'exploitation les plus utilisés dans le monde.
- **macOS**: Développé par Apple, il est utilisé sur les ordinateurs Mac.
- **Linux**: Un système d'exploitation open-source utilisé principalement par les développeurs et les serveurs.
- **Android**: Utilisé principalement sur les smartphones et les tablettes.
- **iOS**: Le système d'exploitation d'Apple pour ses appareils mobiles comme l'iPhone et l'iPad.

## Pourquoi est-ce important?

Le système d'exploitation est crucial car il permet à l'utilisateur d'exploiter pleinement les capacités de l'ordinateur sans avoir à gérer directement les complexités matérielles. Il offre une plateforme stable et sécurisée pour exécuter des applications et effectuer des tâches quotidiennes.


## Qu’est-ce que Linux ?
{{% notice style=info title=Définition %}}
Linux est un **système d'exploitation** puissant et flexible qui offre de nombreux avantages, notamment en termes de sécurité, de stabilité, et de personnalisation. 
{{% /notice %}}

Que ce soit pour un usage personnel, professionnel, ou pour des serveurs, Linux est une option solide et fiable.


### Un peu d'histoire
- **1991** : Créé par ***Linus Torvalds*** et est basé sur le système ***Unix***. 
- **1992** : Le noyau Linux a été re-licencié sous la licence publique générale GNU GPL (*GNU’s Not Unix General Public Licence*), ce qui a renforcé son statut de logiciel libre.
- **1994** : La version 1.0 du noyau Linux a été publiée, marquant une étape importante dans son développement.

Depuis sa création, Linux est devenu l'un des systèmes d'exploitation les plus populaires, notamment pour les serveurs, les superordinateurs, et les appareils embarqués.


### Caractéristiques principales
1. **Open Source** : Le code source de Linux est disponible gratuitement, permettant aux utilisateurs de le modifier et de le distribuer.
2. **Sécurité** : Linux est réputé pour sa robustesse et sa sécurité. Les mises à jour régulières et la communauté active contribuent à maintenir un haut niveau de sécurité.
3. **Stabilité** : Linux est connu pour sa stabilité et sa capacité à fonctionner pendant de longues périodes sans nécessiter de redémarrage.
4. **Personnalisation** : Les utilisateurs peuvent personnaliser leur environnement Linux selon leurs besoins, grâce à une multitude de distributions et d'outils disponibles.

### Distributions Linux
{{% notice style=info title=Définition %}}
Une **distribution Linux** est une version de Linux qui inclut le noyau Linux ainsi que divers logiciels et outils.
{{% /notice %}}

 Voici quelques-unes des distributions les plus populaires :
- **Ubuntu** : Connue pour sa convivialité et son support communautaire.  
[Site d'Ubuntu](https://ubuntu.com/)
- **Fedora** : Souvent utilisée par les développeurs et les administrateurs système.  
[Site de Fedora](https://fedoraproject.org/)
- **Red Hat** : L'une des premières distributions commerciales de Linux. Elle est particulièrement populaire dans les environnements d'entreprise.  
[Site de Red Hat](https://www.redhat.com/fr)
- **Debian** : Réputée pour sa stabilité et sa large collection de logiciels.  
[site de Debian](https://www.debian.org/index.fr.html)
- **Arch Linux** : Appréciée par les utilisateurs avancés pour sa flexibilité et sa simplicité.  
[Site d'Arch Linux](https://archlinux.org/)


### Utilisations de Linux
- **Serveurs** : Linux est largement utilisé pour les serveurs web, les serveurs de bases de données, et les serveurs de fichiers en raison de sa fiabilité et de sa sécurité.
- **Superordinateurs** : La majorité des superordinateurs dans le monde fonctionnent sous Linux.
- **Appareils embarqués** : De nombreux appareils, tels que les routeurs, les téléviseurs intelligents, et les smartphones (via Android), utilisent Linux.
- **Postes de travail** : Bien que moins courant que Windows ou macOS, Linux est utilisé par de nombreux développeurs et professionnels de l'informatique pour ses capacités de personnalisation et ses outils puissants.


### Répartition des SE chez les développeurs

![Répartition SE 2018-2023](repartition2018_2023.png)

[Répartition des systèmes d'exploitation pour le développement de logiciels dans le monde de 2018 à 2023](https://www.statista.com/statistics/869211/worldwide-software-development-operating-system/)

| Avantages | Inconvénients |
|-----------|----------------|
| Très souvent le même environnement que la machine de production (surtout pour la portion serveur d’une application) | Accès très limité aux outils Microsoft : pas de Visual Studio, seulement VS Code et un support minimal pour C# |
| Très facile d’installer des nouveaux outils de développement :<br> `$ dnf install nodejs`<br> `$ dnf install nodejs` | |
| Une bonne console (ligne de commande) est souvent un bon dépanneur pour un développeur (p.ex. les messages d’erreur sont souvent plus explicites à la ligne de commande que dans l’IDE) | |
| Plus facile d’automatiser des tâches de compilation et de tests | |
| Systèmes plus légers qui laissent la place aux outils de développement (p.ex. mon Linux prend moins de 1Go de mémoire, alors le reste est pour les outils, VM, etc.). Dans le cours Android p.ex., l’environnement de développement prend 15Go de mémoire (pour l’IDE + deux émulateurs de téléphone). | |

### Part de marché des SE pour les serveurs 

![Part de marché SE 2023](repartition_serveurs.png)

[Part de marché des systèmes d'exploitation pour les serveurs](https://www.fortunebusinessinsights.com/server-operating-system-market-106601)