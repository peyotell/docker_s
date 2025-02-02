FROM php:8.4-fpm

WORKDIR "/application"

# Updating and installing required packages
RUN apt-get update && apt-get install -y \
    nano \
    libzip-dev zip libicu-dev \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    libpq-dev 
    # default-mysql-client # mysql 

# Installing Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Installing PHP extensions
RUN docker-php-ext-install zip intl pdo_pgsql pgsql gd
# RUN docker-php-ext-install zip intl pdo_mysql mysqli gd

# Setting up GD
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/

# Create user with UID and GID
ARG UID
ARG GID

RUN groupadd -g ${GID} appuser && \
    useradd -m -u ${UID} -g appuser appuser && \
    usermod -aG www-data appuser

# Specify user to run processes
USER appuser
