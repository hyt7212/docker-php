FROM hyt7212/php:7.0-fpm

RUN apt-get update && apt-get install -y \
        supervisor

COPY supervisor.conf /etc/supervisor/conf.d/supervisor.conf

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh

CMD ["/entrypoint.sh"]