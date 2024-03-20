# D'abord definir de ou provient l'image, le Dockerfile contient toujours en premier, un FROM
FROM php:8.2-fpm

# install dependencies for necessary modules activation
# Installer les dependances necessaires a PHP
RUN apt update \
    && apt install -y zip libzip-dev libpng-dev libicu-dev libxml2-dev

# install modules
# Installer les modules
RUN docker-php-ext-install mysqli pdo pdo_mysql gd zip intl xml

# clean cache
# Nettoyer la cache apres toutes les operations
RUN apt clean
