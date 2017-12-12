FROM php:7.0-fpm

RUN apt-get update && apt-get install -y \
        libicu-dev \
        libpq-dev \
        libbz2-dev \
        php-pear \
        mc \
        vim \
        wget \
        libevent-dev \
        librabbitmq-dev \
    && docker-php-ext-install iconv \
    && docker-php-ext-install zip \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install opcache \
    && docker-php-ext-enable opcache

# Change TimeZone
RUN echo "Set default timezone - Asia/Shanghai"
RUN echo "Asia/Shanghai" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Install mcrypt
RUN apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mcrypt

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
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com

# Install redis
RUN pecl install redis && docker-php-ext-enable redis

# Install Xdebug
RUN curl -fsSL 'https://xdebug.org/files/xdebug-2.5.3.tgz' -o xdebug.tar.gz \
    && mkdir -p xdebug \
    && tar -xf xdebug.tar.gz -C xdebug --strip-components=1 \
    && rm xdebug.tar.gz \
    && ( \
        cd xdebug \
        && phpize \
        && ./configure --enable-xdebug \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r xdebug \
    && docker-php-ext-enable xdebug

# Install phpunit
RUN wget https://phar.phpunit.de/phpunit-6.2.phar \
    && chmod +x phpunit-6.2.phar \
    && mv phpunit-6.2.phar /usr/local/bin/phpunit

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*