FROM php:8.4-fpm

WORKDIR "/application"

# Обновление и установка необходимых пакетов
RUN apt-get update && apt-get install -y \
    nano \
    libzip-dev zip libicu-dev libpq-dev \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev

# Установка Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Установка расширений PHP
RUN docker-php-ext-install zip intl pdo_pgsql pgsql gd

# Настройка GD
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/

ARG UID
ARG GID
RUN groupadd -g $GID appuser && \
    useradd -m -u $UID -g appuser appuser
USER appuser
