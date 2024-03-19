# Containers **Docker**

Les conteneurs **Docker** encapsulent les applications et leurs dépendances dans des environnements isolés, permettant une exécution uniforme sur tout système supportant **Docker**.
Cette section vous guide à travers la création, la gestion, et l'interaction avec vos conteneurs **Docker**.

## Créer un Conteneur

Pour créer un conteneur **Docker**, vous commencez généralement par définir une image qui servira de base. Une image **Docker** est un modèle immuable qui contient le code de l'application, ses bibliothèques, ses dépendances et d'autres fichiers nécessaires à l'exécution de l'application.

### Exemple :
**Créer et démarrer un conteneur à partir de l'image nginx:**
```
docker run --name mon-serveur-nginx -d -p 8080:80 nginx
```

Cette commande télécharge l'image nginx si elle n'est pas déjà présente sur votre machine (sinon elle est récuérée localement (CACHED)), crée un conteneur à partir de cette image, et démarre le conteneur. Le conteneur s'exécute en arrière-plan (`-d`), et le port 8080 de l'hôte est mappé sur le port 80 du conteneur.

## Gérer les Conteneurs

**Docker** fournit plusieurs commandes pour gérer les conteneurs:

  - **Lister les conteneurs actifs :**
    ```
    docker ps
    ```

  - **Lister tous les conteneurs (y compris les inactifs) :**
    ```
    docker ps -a
    ```

  - **Arrêter un conteneur :**
    ```
    docker stop mon-serveur-nginx
    ```

  - **Redémarrer un conteneur :**
    ```
    docker start mon-serveur-nginx
    ```

    OU

    ```
    docker restart mon-serveur-nginx
    ```

  - **Supprimer un conteneur :**
    Vous devez d'abord arrêter le conteneur, puis le supprimer avec :
    ```
    docker rm mon-serveur-nginx
    ```
  >Toutes interactions avec les conteneurs peuvent etre faites avec le nom ou l'id (les 3premiers caracteres)

## Interagir avec les Conteneurs

  - **Accéder à un conteneur en cours d'exécution :**
    ```
    docker exec -it mon-serveur-nginx /bin/bash
    ```

  Cette commande ouvre un shell bash dans le conteneur mon-serveur-nginx, vous permettant d'interagir directement avec le système de fichiers et les processus du conteneur.

  - **Afficher les logs d'un conteneur :**
    ```
    docker logs mon-serveur-nginx
    ```

  Cette commande vous permet de voir les logs générés par votre application dans le conteneur.

## Interagir avec les Conteneurs via le Terminal avec `-it`

Lorsque vous lancez un conteneur Docker, l'option `-it` joue un rôle crucial pour permettre une interaction interactive avec le conteneur. Cette option combine deux fonctionnalités distinctes : `-i` (`--interactive`) et `-t` (`--tty`).

  - **`-i` ou `--interactive`** maintient le STDIN (standard input) ouvert pour le conteneur, même si vous n'êtes pas attaché à celui-ci. Cela vous permet de fournir une entrée (input) au conteneur via votre terminal.
  - **`-t` ou `--tty`** alloue un pseudo-TTY (terminal), ce qui vous donne un terminal dans le conteneur similaire à ce que vous auriez sur une connexion SSH. Cela rend possible l'exécution de programmes en mode interactif à l'intérieur du conteneur.

### Exemple Pratique d'Utilisation de `-it` :

Supposons que vous souhaitiez explorer le contenu d'un conteneur Nginx ou apporter des modifications temporaires pour tester quelque chose. Vous pourriez vouloir démarrer un shell **Bash** à l'intérieur du conteneur pour interagir directement avec son système de fichiers et ses processus. Voici comment procéder :

  1. **Lancer un Conteneur Nginx :**
    ```
    docker run --name explore-nginx -d -p 8080:80 nginx
    ```

  2. **Exécuter un Shell Interactif dans le Conteneur :**
  Pour ouvrir un shell **Bash** à l'intérieur du conteneur, utilisez :
    ```
    docker exec -it explore-nginx /bin/bash
    ```

Dans cet exemple :

  - **`docker exec`** exécute une nouvelle commande dans un conteneur en cours d'exécution.
  - **`-it`** attache un terminal interactif à ce conteneur, vous permettant de taper des commandes à l'intérieur du conteneur.
  - **`explore-nginx`** est le nom du conteneur où vous voulez exécuter le shell **Bash**.
  - **`/bin/bash`** est la commande exécutée à l'intérieur du conteneur, lançant un shell **Bash**.

Une fois à l'intérieur du conteneur, vous pouvez naviguer dans le système de fichiers (`cd`, `ls`), modifier des configurations, installer des logiciels temporaires, etc. Pour quitter le shell **Bash**, tapez **`exit`**.

## Utilisation des Ports et Accès via Localhost

Quand vous mappez un port du conteneur sur un port de votre machine hôte (comme avec `-p 8080:80`), vous pouvez accéder à l'application en cours d'exécution dans le conteneur via `http://localhost:8080` ou `http://127.0.0.1:8080`. Cette fonctionnalité est cruciale pour le test et le développement d'applications web.

## Bonnes pratiques

  - **Nettoyage :** Pensez à nettoyer les conteneurs que vous n'utilisez plus pour libérer des ressources. **Docker** fournit des commandes pour supprimer des conteneurs, des images, des volumes, et des réseaux non utilisés.

  - **Gestion des données :** Utilisez des volumes pour persister les données générées par et pour vos applications hors des conteneurs.
