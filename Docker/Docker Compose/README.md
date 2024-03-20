# Docker Compose

**Docker Compose** est un outil qui permet de définir et de gérer des applications multi-conteneurs **Docker** avec simplicité et efficacité. Avec **Docker Compose**, vous pouvez créer un fichier YAML (`.yml`, `.yaml`) pour configurer vos services, réseaux et volumes, puis créer et démarrer tous les services à partir de votre configuration en utilisant une seule commande. Cela simplifie considérablement le processus de déploiement et de gestion des applications conteneurisées.

## Avantages de Docker Compose

  - **Simplicité**: Permet de configurer et de démarrer plusieurs conteneurs Docker simultanément avec un seul fichier de configuration.
  - **Reproductibilité:** Assure une création cohérente des environnements de développement, de test et de production, réduisant les "ça marche sur ma machine" syndromes.
  - **Isolation:** Chaque service s'exécute dans son propre conteneur, garantissant une isolation et une séparation claires.

## Utilisation Basique

### Installation

Pour installer **Docker Compose**, référez-vous à la documentation officielle: [Installation de Docker Compose](https://docs.docker.com/compose/install/).

### Création d'un fichier docker-compose.yml

Créez un fichier `docker-compose.yml` dans votre répertoire de projet (à la racine).Ce fichier peut aussi se nommer differement (`compose.yaml` par exemple). C'est ce fichier qui définit tous les services, réseaux et volumes nécessaires à votre application.
> ⚠️ Attention : l'indentation compte, si une erreur est retournée, verifiez l'indentation et/ou consultez la [documentation officelle de Docker](https://docs.docker.com/compose/compose-file/compose-file-v3/)

Exemple de `docker-compose.yml`
  ```
  version: '3.8'

services:
  a:
    container_name: tata
    build:
      context: ./front
      dockerfile: Dockerfile
    command: ["ping", "google.fr"]
  b:
    container_name: toto
    image: alpine
    command: ["ping", "google.fr"]

networks:
  default:
    name: mynetwork

  ```

Dans cet exemple, deux services sont configurés :

  - **`a`**: qui construit un conteneur nommé `tata` à partir d'un **Dockerfile** situé dans le répertoire `./front` et exécute la commande `ping google.fr`.
  - **`b`**, qui utilise l'image alpine pour créer un conteneur nommé `toto` et exécute également `ping google.fr`.

### Démarrage des services

Pour démarrer tous les services définis dans votre fichier `docker-compose.yml`, exécutez :
  ```
  docker-compose up
  ```

Pour démarrer les services en arrière-plan, ajoutez l'option `-d` (`--detach`) :
  ```
  docker compose up -d
  ```

### Arrêt des services

Pour arrêter tous les services démarrés par **Docker Compose**, utilisez :
```
docker compose down
```

## Autre exemple

Vous trouverez aussi dans cette repo, un [dossier](../Exemple%20Avancé/README.md) `lamp-test` qui simulera la construction d'une stack (pile) appelée **LAMP**.

## Bonnes Pratiques

  - **Organisation:** Gardez votre fichier `docker-compose.yml` aussi simple et clair que possible. Utilisez des fichiers séparés pour les environnements de développement, de test et de production si nécessaire.
  - **Sécurité:** Ne stockez pas de données sensibles (comme les mots de passe) directement dans le fichier `docker-compose.yml`. Utilisez plutôt des variables d'environnement ou des fichiers `.env`.
  - **Nettoyage:** Après avoir testé ou déployé votre application, assurez-vous d'exécuter `docker-compose down` pour nettoyer et arrêter tous les services, évitant ainsi l'utilisation inutile de ressources. Vous pouvez aussi si demandé ou `WARN` dans le terminal executer cette commande `docker compose down --remove-orphans`. Aussi parfois, bien nettoyer et utiliser `docker compose up -d --build` a la creation peut resoudre des problemes.

**Docker Compose** transforme la complexité des applications multi-conteneurs en un processus de développement et de déploiement simple et accessible, rendant la gestion de votre infrastructure Docker plus efficace et plus agréable.
