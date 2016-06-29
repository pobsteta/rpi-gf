# Docker Setup for SIME GF (Gestion Forestière)

Ce dépôt Docker est un moyen rapide et efficace d'installer
un serveur de démonstration de [SIME GF] (http://www.bioecoforests.com/index.html)
(Système Intégré de Management Environnemental Bio Eco Forests).

Ce build est basé sur les images officielles :

* [Docker base image](https://hub.docker.com/r/pobsteta/docker-base/)
* [Docker gf-db](https://hub.docker.com/r/pobsteta/gf-db/)
* [Docker gf-sime](https://hub.docker.com/r/pobsteta/gf-sime/)

et utilise

* [docker-compose](https://docs.docker.com/compose/)

pour la définition du lancement des application et mise en place de
l'environnement de production.

L'image est automatiquement construite depuis [GitHub](https://github.com/pobsteta/bef.git).

## Installation

### Prérequis

Vous devez avoir installé un serveur docker et curl pour télécharger
certains fichiers nécessaires.

Sur un système ubuntu, lancer la commande :

    sudo apt-get install docker.io curl

Ajouter l'utilisateur docker (i.e. vous-mêmes) au groupe docker :

    sudo useradd myuser docker

Note: vous devez vous reconnecter à votre système pour prise en compte des changements.

Ajouter pip sur un système ubuntu avec la commande

    sudo apt-get install python-pip
    
Puis installer docker-compose avec la commande

    sudo pip install docker-compose

## Usage

Créer un répertoire de travail

    mkdir ~/gf
    cd gf

Télécharger le ficher docker-compose.yml

    curl -o ./docker-compose.yml https://raw.githubusercontent.com/pobsteta/gf/master/docker-compose.yml

Exécuter

    docker-compose up

et allez prendre une tasse de café pour patienter...

La première instanciation prend quelques temps pour

* charger les images
* importer la base de données de GF (Gestion Forestière)

Les instanciations suivantes par la commande `docker-compose up` iront beaucoup plus vite.
Arrêter le serveur avec la commande Ctrl+C.


Lister les conteneurs :

  docker ps
  
Se connecter sur le conteneur sime :

  docker exec -ti <id_conteneur_sime> bash
  
Ou directement avec le nom du conteneur conteu dans docker-compose.yml :

  docker exec -ti sime bash
  
Se rendre dans le répertoire /opt/tryton/bin et lancer le serveur par la commande :

  ./trytond -d tryton
  
Lancer un client tryton avec les attributs :

  host: localhost:8000
  base de données: tryton
  identifiant: admin
  mot de passe: admin
  
Voilà vous pouvez utiliser SIME GF !
