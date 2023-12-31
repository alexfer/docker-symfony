FROM php:fpm-alpine

RUN set -ex \
  && apk --no-cache add \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libxpm-dev \
    postgresql-dev \
    libzip-dev \
    graphicsmagick \
    imagemagick \
    libtool \
    curl \
    wget \
    bash

RUN docker-php-ext-install pdo intl opcache zip pdo_mysql

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pgsql pdo_pgsql

RUN docker-php-ext-configure gd --enable-gd --with-webp --with-freetype --with-jpeg --with-xpm \
    && docker-php-ext-install gd

RUN apk add --update --no-cache --virtual .build-dependencies $PHPIZE_DEPS \
        && pecl install apcu \
        && docker-php-ext-enable apcu \
        && pecl install redis \
        && docker-php-ext-enable redis \
#        && pecl install gmagick-2.0.6RC1 \
#        && docker-php-ext-enable gmagick \
        && pecl clear-cache \
        && apk del .build-dependencies

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

WORKDIR /var/www/project

CMD ["php-fpm"]
