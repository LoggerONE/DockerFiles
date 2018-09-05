# docker build -t snowsprout/php7.2-fpm:moodle .

FROM php:7.2-fpm

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN apt-get update && apt-get install -y libmemcached-dev zlib1g-dev libicu-dev g++ \
    && pecl install memcached \
    && docker-php-ext-enable memcached

RUN apt-get update && apt-get install -y \
			libmcrypt-dev \
			libxml2-dev \
			libssl-dev \
			libjpeg-dev \
			libpng-dev \
			libfreetype6-dev \
		&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
		&& docker-php-ext-install -j$(nproc) gd
				

# Install Exts
RUN docker-php-ext-install dom
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install xmlrpc
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip
RUN docker-php-ext-install iconv
RUN docker-php-ext-install opcache
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
