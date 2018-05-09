FROM ikerlin/php:7.1-fpm-supervisor-dev

RUN apt-get update && \
    apt-get install -y libxml2-dev && \
    docker-php-ext-install soap

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*