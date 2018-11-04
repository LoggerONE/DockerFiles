# docker build -t snowsprout/php7.0-fpm .

FROM php:7.0-fpm

MAINTAINER "SnowSprout" <me@snowsprout.net>

RUN apt-get update && apt-get install -y \
			libmcrypt-dev \
			libxml2-dev \
			libssl-dev \
			zlib1g-dev

# Install Exts
RUN docker-php-ext-install dom
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install pdo_mysql

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

RUN cd /tmp
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"