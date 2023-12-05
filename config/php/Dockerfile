FROM php:fpm-alpine

RUN set -ex \
  && apk --no-cache add \
    postgresql-dev \
    libpng-dev \ 
    libzip-dev \
    curl

RUN docker-php-ext-install pdo pdo_pgsql intl

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pgsql pdo_pgsql

RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
#RUN docker-php-ext-install curl
RUN docker-php-ext-install pdo_mysql
   
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/project

CMD ["php-fpm"]
