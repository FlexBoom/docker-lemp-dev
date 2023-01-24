FROM php:8.2-fpm-alpine

RUN apk update && apk upgrade && apk add --no-cache $PHPIZE_DEPS gmp-dev libzip-dev zlib-dev libpng-dev libwebp-dev libjpeg-turbo-dev freetype-dev icu-dev imagemagick-dev libmemcached-dev linux-headers \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install gd gmp zip pdo pdo_mysql opcache \
    && docker-php-ext-enable gd gmp zip pdo pdo_mysql opcache \
    && pecl install imagick redis memcached xdebug \
    && docker-php-ext-enable imagick redis memcached xdebug

COPY ./xdebug/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN adduser -D -s /bin/sh docker

# TODO
# - Check if extensions like gmp already is bundled with PHP
# - Test with a Laravel installation
# - Test xdebug
