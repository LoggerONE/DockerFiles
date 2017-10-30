# docker build -t snowsprout/php7.1-fpm:laravel .

FROM php:7.1-fpm

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN apt-get update && apt-get install -y \
			libmcrypt-dev \
			libxml2-dev \
			libssl-dev

# Install Exts
RUN docker-php-ext-install zip
RUN docker-php-ext-install dom
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install pdo_mysql

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

RUN cd /tmp
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer