FROM php:8.3-fpm

# Librerías del sistema que necesitan las extensiones + herramientas útiles
RUN apt-get update && apt-get install -y \
        git unzip libzip-dev libicu-dev \
    && docker-php-ext-install pdo_mysql zip intl bcmath \
    && rm -rf /var/lib/apt/lists/*

# Composer, copiado desde su imagen oficial
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Hacer que www-data tenga TU mismo UID/GID (evita archivos de root en tu carpeta)
ARG USER_ID=1000
ARG GROUP_ID=1000
RUN groupmod -o -g ${GROUP_ID} www-data \
    && usermod -o -u ${USER_ID} -g www-data www-data \
    && chown www-data:www-data /var/www

WORKDIR /var/www/html
USER www-data
