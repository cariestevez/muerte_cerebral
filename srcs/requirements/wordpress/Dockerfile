FROM debian:bullseye

RUN apt-get update && apt-get install -y \
    php php-fpm php-mysql \
    curl tar git \
    && curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp \
    && apt-get clean \
    && mkdir -p /var/www/wordpress \
    && chown -R www-data:www-data /var/www/wordpress \
    && chmod -R 755 /var/www/wordpress \
    && mkdir -p var/run/php/ && cd var/run/php/ && touch php7.4-fpm.pid

COPY ../conf/www.conf /etc/php/7.4/fpm/pool.d/
COPY ../tools/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]