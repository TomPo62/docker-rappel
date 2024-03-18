# Dockerfile : Construire des Images Personnalisées

Un **Dockerfile** est un fichier texte (qu'on nomme `Dockerfile`) qui contient une série de commandes que l'outil de ligne de commande **Docker** (`docker`) peut utiliser pour assembler une image automatiquement. Ces commandes permettent de définir et de configurer votre image, y compris l'installation de logiciels, la configuration des environnements, l'exposition des ports, etc. L'image construite peut alors être utilisée pour démarrer de nouveaux conteneurs.

## Structure de Base d'un Dockerfile

Un **Dockerfile** typique commence par une instruction `FROM`, qui définit l'image de base. Ensuite, il contient une série d'instructions qui appliquent des modifications à cette image, créant ainsi une nouvelle image qui est une version modifiée de l'image de base.

Voici les instructions **Dockerfile** les plus couramment utilisées :

  - **`FROM` :** Définit l'image de base.
  - **`RUN `:** Exécute des commandes dans le conteneur.
  - **`CMD `:** Fournit des commandes par défaut pour l'exécution du conteneur.
  - **`LABEL` :** Ajoute des métadonnées à l'image comme le mainteneur.
  - **`EXPOSE` :** Indique les ports sur lesquels un conteneur va écouter.
  - **`ENV` :** Définit des variables d'environnement.
  - **`ADD` et `COPY` :** Copient des fichiers et des répertoires dans l'image.
  - **`ENTRYPOINT` :** Configure un conteneur qui va s'exécuter comme un exécutable.
  - **`VOLUME` :** Crée un point de montage pour accéder et stocker les données.
  - **`WORKDIR` :** Définit le répertoire de travail pour les instructions `RUN`, `CMD`, `ENTRYPOINT`, `COPY` et `ADD`.

## Exemple Pratique : Créer un Dockerfile Simple

Supposons que vous souhaitiez créer une image personnalisée basée sur **Ubuntu**, avec le serveur web **Nginx** installé.

### Dockerfile :
```
# Définit l'image de base
FROM ubuntu:latest

# Met à jour les paquets et installe Nginx
RUN apt-get update && apt-get install -y nginx

# Définit le répertoire de travail
WORKDIR /usr/share/nginx/html

# Copie le contenu du site web dans le conteneur
COPY . .
```
### Explications :

  - **`FROM ubuntu:latest`** utilise l'image Ubuntu comme base.
  - **`RUN apt-get update && apt-get install -y nginx`** installe **Nginx** sur l'image.
  - **`WORKDIR /usr/share/nginx/html`** définit le répertoire de travail où les commandes suivantes seront exécutées.
  - **`COPY . .`** copie les fichiers locaux (dans le même répertoire que votre Dockerfile) dans le répertoire de travail du conteneur (ici, `/usr/share/nginx/html`).

Pour construire l'image à partir de ce **Dockerfile**, exécutez la commande suivante dans le même répertoire que votre **Dockerfile** (idéalement ayez un `index.html` de test dans ce même répertoire) :
  ```
  docker build -t mon-image-nginx .
  ```

Et pour démarrer un conteneur basé sur votre image :
  ```
  docker run -d -p 8080:80 --name monexemple mon-image-nginx
  ```

Cette commande démarre un conteneur qui aura le nom `monexemple` en arrière-plan, mappant le port 80 du conteneur sur le port 8080 de l'hôte.

## Bonnes Pratiques

  - **Minimiser le nombre de couches :** Combine les commandes `RUN` autant que possible (&&) pour réduire le nombre de couches dans l'image, ce qui optimise la taille et la construction de l'image.
  - **Commandes en cache :** Organisez votre **Dockerfile** de manière à exploiter le cache **Docker**. Dans l'exemple si dessus, nous isntallons d'abord **Ubuntu**, il sera donc stocké dans le cache et recupéré depuis le cache pour tous nouveaux `build`.

En maîtrisant la création de Dockerfiles, vous pouvez automatiser la construction d'images **Docker** personnalisées, facilitant le déploiement et la distribution de vos applications.
