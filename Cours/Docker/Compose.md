Structure du dossier:

```
mon-wordpress/
├── Dockerfile
├── docker-compose.yml

```

## Dockerfile
```Dockerfile
# Utiliser l'image officielle PHP avec Apache
FROM php:8.2-apache

# Installer les extensions PHP nécessaires pour WordPress
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    unzip \
    wget \
    libzip-dev \
    && docker-php-ext-install mysqli pdo pdo_mysql zip gd

# Activer .htaccess
RUN a2enmod rewrite

# Télécharger WordPress
WORKDIR /var/www/html
RUN rm -rf * && \
    wget https://wordpress.org/latest.tar.gz && \
    tar -xzf latest.tar.gz --strip-components=1 && \
    rm latest.tar.gz

# Changer les permissions
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Exposer le port 80
EXPOSE 80

# Lancer Apache en avant-plan
CMD ["apache2-foreground"]

```

## docker-compose.yml

```Dockerfile
version: '3.8'

services:
  wordpress:
    build: .
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: wp_pass
    depends_on:
      - db

  db:
    image: mariadb:10.5
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: wp_pass
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:

```


## Construire l'image

```
docker compose build
```

## Lancer les conteneurs
```
docker compose up -d
```

## Tout fermer proprement

```
docker-compose down

```

## Tout fermer proprement puis tout supprimer

```
docker-compose down -v

```