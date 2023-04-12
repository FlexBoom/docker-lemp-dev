# Docker LEMP development

[![build](https://github.com/FlexBoom/docker-lemp-dev/actions/workflows/build.yml/badge.svg)](https://github.com/FlexBoom/docker-lemp-dev/actions/workflows/build.yml)

Do not use in production.

## Containers

Name    | Version | Port
--------|---------|----------
nginx   | latest  | 8080
PHP     | 8.2     | 9000
MySQL   | latest  | 3306
Xdebug  | latest  | 9003
Redis   | latest  | 6379
MailDev | latest  | 1080,1025

## Extra PHP extensions

zip, OPcache, GD, imagick, gmp, pdo_mysql, memcached, BCMath, intl.

## Usage

- clone this repo into the desired folder and `cd` into it.
- Run `docker compose build`.
- Run `docker compose up -d`.
- Tips:
  - If the folder you cloned to was named `test` then you can run this command to get into e.g. the PHP container: `docker exec -it test-php-1 /bin/sh`.
  - By default the user in the docker containers are `UID=1000` and `GID=1000` because that was Linux uses for the default user your a logged in with.
  - You can rename `.env.example` to `.env` and change the values for `UID` and `GID`.
  - On MAC it usually is `UID=501` and `GID=501`. You can find it by running `id` in the terminal.
