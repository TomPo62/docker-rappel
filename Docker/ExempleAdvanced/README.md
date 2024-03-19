# Projet LAMP avec Docker Compose

Ce projet utilise **Docker** et **Docker Compose** pour créer un environnement de développement LAMP (Linux, Apache, MySQL (ici MariaDB), PHP), comprenant également **PHPMyAdmin** pour la gestion de la base de données. Il est conçu pour fournir un moyen rapide et facile de déployer un environnement de développement LAMP sans nécessiter d'installation manuelle de chaque composant.

## Structure du Projet

Le projet est organisé comme suit :

  - **`docker-compose.yml` :** Définit les services **Docker** nécessaires pour le projet.
  - **`.gitignore` :** Fichier pour exclure des fichiers spécifiques du versionnage avec Git.
  - **`.env` :** Fichier de variables d'environnement pour les services Docker.
  - **`apache_docker` :** Dossier contenant la configuration Apache et le **Dockerfile** personnalisé.
      - **`apache-vhost.conf` :** Configuration du Virtual Host pour Apache.
      - **`Dockerfile` :** **Dockerfile** pour construire l'image Apache avec la configuration personnalisée.
  - **`php_docker` :** Dossier contenant le **Dockerfile** pour l'image PHP.
      - **`Dockerfile` :** **Dockerfile** pour construire l'image PHP avec les extensions nécessaires.
  - **`app` :** Dossier contenant le code source de votre application.
      - **`index.php` :** Fichier PHP de test.

  > ⚠️ Dans le `.gitignore`, le `/.env` a été commenté volotairement pour publier le `.env`. Assurez vous de decommenter cette ligne.

  > ⚠️ Aussi des choix peuvent être fait selon vos configurations voulue ou preferences en decommentant certaines lignes et en commentant ou supprimant d'autres. Bien lire les fichiers est crucial.

## Pré-requis

  - **Docker**
  - **Docker Compose**
  - **Git** (optionnel mais recommandé pour le contrôle de version)

## Mise en Place

  1. Cloner le dépôt (si versionné avec Git) :
  ```
  git clone [URL_DU_DEPOT]
  cd lamp-test
  ```

  2. Initialiser le dépôt Git (si vous partez de zéro) :
  Cette étape est cruciale pour s'assurer que le fichier `.env` soit pris en compte correctement.
  ```
  git init
  ```

3. Configurer le fichier `.env` :

Le fichier `.env` est déjà **configuré avec des valeurs par défaut**. Assurez-vous de les modifier selon vos besoins.
> ⚠️ Ne les utilisez pas comme ca ! Entrez vos propres valeurs.

4. Lancer l'environnement avec **Docker Compose** :
  ```
  docker-compose up -d
  ```
  OU
  ```
  docker compose up -d --build
  ```

Cette commande va télécharger les images nécessaires, construire les images personnalisées et démarrer les conteneurs.

## Accéder aux Services

  - **Application Web :** Ouvrez votre navigateur et allez sur `http://localhost:8085` pour voir l'application PHP.
  - **PHPMyAdmin :** Accédez à PHPMyAdmin à l'adresse `http://localhost:8084` pour gérer votre base de données MySQL.

## Commandes Utiles

  - **Arrêter les conteneurs :**
    ```
    docker compose down
    ```

  - **Nettoyer le cache de Docker :**
    ```
    docker buildx prune -f
    ```

## Bonnes Pratiques

  - **Gestion des données :** Utilisez des volumes Docker pour persister les données MySQL au-delà de la durée de vie des conteneurs.
  - **Sécurité :** Ne jamais utiliser les configurations par défaut en production. Assurez-vous de changer les mots de passe et de configurer correctement les réseaux **Docker**.

