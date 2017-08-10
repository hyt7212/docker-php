FROM php:7.0-fpm-alpine

RUN apk add --no-cache \
      bash ca-certificates tzdata \
      freetype \
      libmcrypt \
      libjpeg-turbo \
      libpng \
      openssl \
      hiredis \
      hiredis-dev \
      libmcrypt-dev \
      freetype-dev \
      openssl-dev \
      libjpeg-turbo-dev \
      libpng-dev \
      linux-headers \
      musl \
      gcc \
      libtool && \
    cp -r -f /usr/share/zoneinfo/Hongkong /etc/localtime && \
    apk add --update \
      tar \
      gzip \
      wget && \
    apk del \
      wget && \
    rm -rf /var/cache/apk/* && rm -rf /tmp/*

# 安装扩展
RUN  docker-php-ext-install  gd zip mcrypt mbstring pdo_mysql opcache pcntl

# redis
RUN  pecl install redis-3.1.2 
RUN  echo "extension=redis.so" > /usr/local/etc/php/conf.d/phpredis.ini