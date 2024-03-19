FROM php:8.2-fpm

# install dependencies for necessary modules activation
RUN apt update \
    && apt install -y zip libzip-dev libpng-dev libicu-dev libxml2-dev

# install modules
RUN docker-php-ext-install mysqli pdo pdo_mysql gd zip intl xml

# clean cache
RUN apt clean
