FROM ubuntu:14.04

MAINTAINER Seva Dolgopolov

ENV PHP_VERSION {YOUR_VERSION}
ENV PHP_INI_DIR /etc/php

RUN apt-get update && apt-get install -yq build-essential curl libicu-dev libxml2-dev autoconf libcurl4-openssl-dev pkg-config

WORKDIR /tmp

ENV LAST_UPDATE 2015-04-13

RUN curl -SL "http://php.net/get/php-$PHP_VERSION.tar.bz2/from/this/mirror" -o php.tar.bz2
RUN curl -SL "http://php.net/get/php-$PHP_VERSION.tar.bz2.asc/from/this/mirror" -o php.tar.bz2.asc

# varificate download
RUN gpg --keyserver pgp.mit.edu --recv-key $(gpg php.tar.bz2.asc 2>&1  | awk '$2 == "Signature" {print $14}') && gpg --verify php.tar.bz2.asc php.tar.bz2

# extract archive
RUN tar xjvf php.tar.bz2
RUN mkdir -p $PHP_INI_DIR/conf.d 
RUN cd php-$PHP_VERSION && ./configure \ 
--with-config-file-path="$PHP_INI_DIR" \ 
--with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
--with-openssl \
--enable-sockets \
&& make \
&& make install \
&& cd .. \
&& rm -fr php* 
