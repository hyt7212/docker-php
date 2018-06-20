FROM php:7.1-fpm

ENV REDIS_VERSION=3.1.6

RUN apt-get update \
    && apt-get install -y apt-utils libmcrypt-dev libicu-dev libpq-dev libbz2-dev libevent-dev librabbitmq-dev \
        vim wget \
    && docker-php-ext-install iconv zip bz2 mbstring intl pdo_mysql mysqli bcmath mcrypt opcache pcntl \
    && docker-php-ext-enable opcache

# Change TimeZone
RUN echo "Set default timezone - Asia/Shanghai"
RUN echo "Asia/Shanghai" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Install GD
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-configure gd \
          --enable-gd-native-ttf \
          --with-freetype-dir=/usr/include/freetype2 \
          --with-png-dir=/usr/include \
          --with-jpeg-dir=/usr/include \
    && docker-php-ext-install gd \
    && docker-php-ext-enable gd

# Install composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org

# Install redis
RUN pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /data/www