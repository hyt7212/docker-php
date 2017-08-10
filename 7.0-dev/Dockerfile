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

# 安装debug扩展
RUN  pecl install xdebug-2.5.0 
RUN  echo "zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

# 安装 composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update \
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com