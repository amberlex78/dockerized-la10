FROM php:8.2-fpm

# First
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && apt-get install -y dialog apt-utils libpq-dev zip unzip curl wget git && \
    echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# PHP Extensions
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && \
    docker-php-ext-install pdo_mysql

# Composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer -q

# Config PHP
RUN cp $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini
COPY ./conf.d $PHP_INI_DIR/conf.d

WORKDIR /app
