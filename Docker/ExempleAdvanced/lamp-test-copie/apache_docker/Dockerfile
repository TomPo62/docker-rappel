# D'abord definir de ou provient l'image, le Dockerfile contient toujours en premier, un FROM
FROM httpd:2.4-alpine

# Installation et mise a jour
RUN apk update; apk upgrade;

# Recuperer et copier le fichier apache-vhost.conf dans la destination, ici /usr/local/apache2/conf/apache-vhost.conf
COPY apache-vhost.conf /usr/local/apache2/conf/apache-vhost.conf

# Executer et inclure notre destination
RUN echo "Include /usr/local/apache2/conf/apache-vhost.conf" \
    >> /usr/local/apache2/conf/httpd.conf
