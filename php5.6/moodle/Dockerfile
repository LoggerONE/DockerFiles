# docker build -t snowsprout/php5.6-fpm:moodle .

FROM php:5.6-fpm

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN apt-get update && apt-get install -y libmemcached-dev zlib1g-dev libicu-dev g++ \
    && pecl install memcached-2.2.0 \
    && docker-php-ext-enable memcached

RUN apt-get update && apt-get install -y \
			libmcrypt-dev \
			libxml2-dev \
			libssl-dev \
			libpng-dev

RUN apt-get update \
    && apt-get install libpng12-dev libfreetype6-dev libjpeg62-turbo-dev -qy \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd			

# Install Exts
RUN docker-php-ext-install dom
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install xmlrpc
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip
RUN docker-php-ext-install iconv
RUN docker-php-ext-install opcache
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install bcmath
