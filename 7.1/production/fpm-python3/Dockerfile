FROM hyt7212/php:7.1-fpm-supervisor

RUN apt-get update && apt-get install -y \
        python3 \
        python3-pip \
    && pip3 install xlrd

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*