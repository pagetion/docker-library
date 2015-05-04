FROM ubuntu:14.04

MAINTAINER Seva Dolgopolov

ENV PHP_VERSION 7.0
ENV PHP_INI_DIR /etc/php

RUN apt-get update && apt-get install -yq build-essential curl libicu-dev libxml2-dev autoconf libcurl4-openssl-dev pkg-config bison git libbz2-dev libjpeg-dev libpng-dev libXpm-dev libfreetype6-dev libt1-dev libgmp-dev libmcrypt-dev libmysqlclient-dev libpspell-dev librecode-dev

RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h
ADD src /tmp/php

WORKDIR /tmp/php

ENV LAST_UPDATE 2015-04-26

RUN ./buildconf && ./configure \ 
    --with-config-file-path=$PHP_INI_DIR \
    --enable-mbstring \
    --enable-zip \
    --enable-bcmath \
    --enable-pcntl \
    --enable-ftp \
    --enable-exif \
    --enable-calendar \
    --enable-sysvmsg \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-wddx \
    --enable-fpm \
    --with-curl \
    --with-mcrypt \
    --with-iconv \
    --with-gmp \
    --with-pspell \
    --with-gd \
    --with-jpeg-dir=/usr \
    --with-png-dir=/usr \
    --with-zlib-dir=/usr \
    --with-xpm-dir=/usr \
    --with-freetype-dir=/usr \
    --with-t1lib=/usr \
    --enable-gd-native-ttf \
    --enable-gd-jis-conv \
    --with-openssl \
    --with-pdo-mysql=/usr \
    --with-gettext=/usr \
    --with-zlib=/usr \
    --with-bz2=/usr \
    --with-recode=/usr \
    --with-mysqli=/usr/bin/mysql_config
RUN make && make install

#fpm
RUN sed 's_NONE_/usr/local_' < /usr/local/etc/php-fpm.conf.default > /usr/local/etc/php-fpm.conf && \
 sed 's_nobody_www-data_' < /usr/local/etc/php-fpm.d/www.conf.default > /usr/local/etc/php-fpm.d/www.conf 
