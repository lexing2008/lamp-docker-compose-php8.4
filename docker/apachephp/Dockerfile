FROM php:8.4-apache

RUN apt-get update \
    && apt-get install -y libpng-dev libjpeg-dev \
    libwebp-dev \
    libmemcached-dev zlib1g-dev vim

# копирование virtual hosts apache
COPY apache/hosts/* /etc/apache2/sites-available

RUN a2enmod rewrite # включаем в апаче модуль rewrite
RUN a2enmod proxy_http # включаем в апаче модуль proxy_http
RUN service apache2 restart


# install php zip
RUN apt-get install -y  \
        libzip-dev \
        zip \
        libxml2-dev \
  && docker-php-ext-install zip

# установка mysql клиента
RUN apt-get install -y default-mysql-client

# установка расширения DB
RUN docker-php-ext-install pdo pdo_mysql mysqli xml
RUN docker-php-ext-install dom xmlwriter

# install php GD
RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-webp && docker-php-ext-install gd \
    && apt-get install -y libmagickwand-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# установка композера
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# установка расширения
#RUN pecl install xdebug \
#    && docker-php-ext-enable xdebug

# копирование конфигов php
COPY php/conf.d/* $PHP_INI_DIR/conf.d/
