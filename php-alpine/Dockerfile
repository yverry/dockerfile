#
# Dockerfile
#

FROM php:fpm-alpine
MAINTAINER Yann Verry <docker@verry.org>


RUN apk update && apk add --no-cache postgresql-dev \
	    autoconf \
	    dpkg-dev dpkg \
	    file \
	    g++ \
	    gcc \
	    libc-dev \
	    make \
	    pkgconf \
	    libzip-dev \
	    libpng-dev \
	    libwebp-dev \
	    imagemagick-dev \
	    freetype-dev \
	    libjpeg-turbo-dev \
	    icu-dev \
	    gettext-dev \
	    re2c && \
    pecl install apcu imagick && \
    docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-webp-dir=/usr/include/ && \
    docker-php-ext-install pdo_pgsql pdo_mysql mysqli zip gd intl exif gettext && \
    docker-php-ext-enable imagick opcache

COPY config/opcache.ini $PHP_INI_DIR/conf.d/
