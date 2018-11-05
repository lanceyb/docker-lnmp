FROM php:7.1-fpm

MAINTAINER LNMP Docker Maintainers 'lance.zyb@gmail.com'

ENV PHP_VERSION 7.1.20
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --disable-cgi

RUN apt-get update

RUN usermod -u 1000 www-data

RUN apt-get install -y --no-install-recommends git zip unzip

RUN apt-get install -y --no-install-recommends apt-utils

RUN apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
	&& docker-php-ext-install -j$(nproc) iconv \
  && docker-php-ext-install pdo pdo_mysql \
  && docker-php-ext-install zip \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --filename=composer --install-dir=/usr/local/bin
RUN php -r "unlink('composer-setup.php');"

RUN mkdir /usr/local/php/composer

RUN composer global require 'laravel/installer:2.0'
