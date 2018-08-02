FROM php:7.2.8-fpm

MAINTAINER LNMP Docker Maintainers 'lance.zyb@gmail.com'

ENV PHP_VERSION 7.2.8

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
	&& docker-php-ext-install -j$(nproc) iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd
