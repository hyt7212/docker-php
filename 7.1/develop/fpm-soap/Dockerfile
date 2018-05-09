FROM ikerlin/php:7.1-fpm-soap

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