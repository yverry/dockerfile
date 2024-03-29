#
# Dockerfile
#

FROM php:8-fpm-alpine AS builder
MAINTAINER Yann Verry <docker@verry.org>


# build FROM
RUN apk update && apk add --no-cache postgresql-dev \
	    git \
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
	    imagemagick \
	    freetype-dev \
	    libjpeg-turbo-dev \
	    icu-dev \
	    gettext-dev \
	    re2c \
	    zlib-dev \
	    gmp-dev && \
    pecl install apcu redis && \
    docker-php-ext-configure gd --with-webp --with-jpeg --with-freetype && \
    docker-php-ext-install pdo_pgsql pdo_mysql mysqli zip gd intl exif gettext gmp bcmath && \
    docker-php-ext-enable opcache redis && \
	docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini

# build php-imagick from github source (php8 compat)
RUN cd /usr/src && \
	git clone https://github.com/Imagick/imagick.git && \
	cd imagick && \
	phpize && \
	./configure && \
	make && \
	make install && \
	rm -rf /usr/src/* && \
	docker-php-ext-enable imagick

# run FROM
FROM php:8-fpm-alpine

RUN apk update && apk add --no-cache imagemagick \
	postgresql-libs \
	libzip \
	libpng \
	libwebp \
	libjpeg-turbo \
	icu-libs

# copy so
COPY --from=builder /usr/local/lib/php/extensions/no-debug-non-zts-20200930/*.so /usr/local/lib/php/extensions/no-debug-non-zts-20200930/
COPY --from=builder /usr/local/etc/php/conf.d/* /usr/local/etc/php/conf.d/

COPY config/ini/*.ini $PHP_INI_DIR/conf.d/
COPY config/php-fpm/*.conf /usr/local/etc/php-fpm.d/
