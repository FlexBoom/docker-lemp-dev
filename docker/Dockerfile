FROM php:fpm

# PHP
RUN apt-get update -y && apt-get install -y --no-install-recommends libpng16-16 libzip4 libfreetype6-dev libpng-dev libjpeg62-turbo libjpeg62-turbo-dev libicu-dev libgmp-dev libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd intl bcmath gmp zip pdo_mysql pcntl \
    && docker-php-ext-enable gd intl bcmath gmp zip pdo_mysql pcntl \
    && docker-php-source delete \
    && apt-get purge -y libpng-dev libfreetype6-dev libjpeg62-turbo-dev libicu-dev libonig-dev libgmp-dev libzip-dev

# PECL
RUN apt-get update -y && apt-get install -y --no-install-recommends libmagickwand-6.q16-6 libmagickwand-dev libmcrypt4 libmcrypt-dev libmemcached11 libmemcached-dev \
    && pecl install imagick redis mcrypt memcached \
    && docker-php-ext-enable imagick redis mcrypt memcached \
    && apt-get purge -y libmagickwand-dev libmcrypt-dev libmemcached-dev

# Xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
COPY ./xdebug/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN apt-get clean -y && apt-get autoremove --purge -y && rm -rf /var/lib/apt/lists/*

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN useradd -ms /bin/bash docker
