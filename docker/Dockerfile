FROM php:8.2-fpm-alpine

ARG UID
ARG GID

RUN pear config-set php_ini "$PHP_INI_DIR"

RUN apk update && apk upgrade && apk add --no-cache $PHPIZE_DEPS libzip-dev zlib-dev \
    gmp-dev libmemcached-dev linux-headers imagemagick-dev libpng-dev libwebp-dev \
    libjpeg-turbo-dev freetype-dev icu-dev \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-configure intl \
    && docker-php-ext-install gd gmp pdo_mysql opcache zip bcmath intl

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN pecl install imagick redis memcached xdebug \
    && docker-php-ext-enable imagick redis memcached xdebug

COPY ./xdebug/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN addgroup -g $GID docker && adduser -D -u $UID -G docker -s /bin/sh docker

USER docker
