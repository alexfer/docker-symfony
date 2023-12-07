FROM php:fpm-alpine

RUN set -ex \
  && apk --no-cache add \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    postgresql-dev \     
    libzip-dev \
    imagemagick-dev \ 
    libtool \
    curl \
    wget \
    bash   

RUN docker-php-ext-install pdo pdo_pgsql intl opcache gd zip pdo_mysql
#RUN pecl install gmagick-2.0.6RC1

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pgsql pdo_pgsql

RUN docker-php-ext-configure gd \
#    --with-png=/usr/include/ \
    --with-jpeg=/usr/include/ \
    --with-freetype=/usr/include/

#RUN docker-php-ext-install gd
#RUN docker-php-ext-install zip
#RUN docker-php-ext-install pdo_mysql
   
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

WORKDIR /var/www/project

CMD ["php-fpm"]
