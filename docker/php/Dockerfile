FROM php:8-apache

RUN set -eux && apt-get update -y && apt-get -y upgrade

RUN apt-get autoremove && apt-get clean && rm -r /var/lib/apt/lists/*

COPY php.ini-development /usr/local/etc/php/php.ini
COPY conf.d/ /usr/local/etc/php/conf.d/

RUN sed -i s%/var/www/html%/var/www/html/\${PUBLIC_ROOT}%g  /etc/apache2/sites-enabled/000-default.conf

# resolve o problema que impedia o usuário www-data de gravar no diretório /var/www/html
RUN usermod --non-unique --uid 1000 www-data \
  && groupmod --non-unique --gid 1000 www-data \
  && chown -R www-data:www-data /var/www
