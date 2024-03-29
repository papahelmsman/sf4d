FROM php:7.3-fpm

LABEL maintainer="Pavel A. Petrov <papahelmsman@gmail.com>"

ARG APCU_VERSION=5.1.11
ARG TIMEZONE
ARG WORKDIR
ARG APP_NAME

ENV TIMEZONE=$TIMEZONE

RUN apt-get update && apt-get install -y \
    git \
    zip \
    unzip \
    libzip-dev \
    zlib1g-dev \
    libpq-dev \
    git-core \
    libmcrypt-dev \
    libfcgi0ldbl \
    gnupg \
    libjpeg62-turbo-dev \
    libicu-dev \
    wget

# gd extension
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libfreetype6-dev \
    libjpeg-dev \
    libxpm-dev \
    libxml2-dev \
    libxslt-dev \
    librabbitmq-dev \
    libssh-dev \
    libwebp-dev
RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-xpm-dir=/usr/include/ \
    --with-webp-dir=/usr/include/
RUN docker-php-ext-install gd

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo_pgsql pgsql \
    && docker-php-ext-install opcache \
    && docker-php-ext-install intl \
    && docker-php-ext-install mbstring

RUN pecl install apcu-${APCU_VERSION} \
    && docker-php-ext-enable apcu

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

RUN pecl install xdebug-beta \
    && docker-php-ext-enable xdebug

COPY docker/dev/php/7.3/fpm/xdebug.ini /usr/local/etc/php/conf.d/
COPY docker/dev/php/7.3/fpm/symfony.ini /usr/local/etc/php/conf.d/

## Permission fix
#RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /$WORKDIR

WORKDIR /$WORKDIR/$APP_NAME

USER www-data
