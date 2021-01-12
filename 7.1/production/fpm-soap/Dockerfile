FROM ikerlin/php:7.1-fpm-supervisor

RUN apt-get update && \
    apt-get install -y libxml2-dev && \
    docker-php-ext-install soap && \
    pecl install swoole-4.2.12 && docker-php-ext-enable swoole

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*