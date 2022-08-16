FROM php:8-apache

RUN set -eux && apt-get update -y && apt-get -y upgrade

#RUN docker-php-ext-install -j$(nproc) iconv

#RUN apt-get install -y libc-client-dev libkrb5-dev \
#    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
#    && docker-php-ext-install -j$(nproc) imap

#RUN apt-get install -y libicu-dev \
#&& docker-php-ext-configure intl \
#&& docker-php-ext-install -j$(nproc) intl

#RUN apt-get install -y libldap2-dev \
#    && docker-php-ext-install -j$(nproc) ldap \

#RUN docker-php-ext-install -j$(nproc) mysqli

#RUN apt install -y wget unzip libaio1 libaio-dev \
#    && mkdir /opt/oracle \
#    && cd /opt/oracle \
#    && wget https://download.oracle.com/otn_software/linux/instantclient/217000/instantclient-basic-linux.x64-21.7.0.0.0dbru.zip \
#    && wget https://download.oracle.com/otn_software/linux/instantclient/217000/instantclient-sdk-linux.x64-21.7.0.0.0dbru.zip \
#    && unzip /opt/oracle/instantclient-basic-linux.x64-21.7.0.0.0dbru.zip -d /opt/oracle \
#    &&  unzip /opt/oracle/instantclient-sdk-linux.x64-21.7.0.0.0dbru.zip -d /opt/oracle \
#    && rm -rf /opt/oracle/*.zip \
#    && [ -f /opt/oracle/instantclient_21_7/libclntsh.so ] || ln -s /opt/oracle/instantclient_21_7/libclntsh.so.21.7 /opt/oracle/instantclient_21_7/libclntsh.so \
#    && [ -f /opt/oracle/instantclient_21_7/libclntshcore.so ] || ln -s /opt/oracle/instantclient_21_7/libclntshcore.so.21.7 /opt/oracle/instantclient_21_7/libclntshcore.so \
#    && [ -f /opt/oracle/instantclient_21_7/libocci.so ] || ln -s /opt/oracle/instantclient_21_7/libocci.so.21.7 /opt/oracle/instantclient_21_7/libocci.so \
#    && [ -f /lib/x86_64-linux-gnu/libnnz21.so ] || ln -s /opt/oracle/instantclient_21_7/libnnz21.so /lib/x86_64-linux-gnu/libnnz21.so \
#    && [ -f /lib/x86_64-linux-gnu/libclntshcore.so.21.1 ] || ln -s /opt/oracle/instantclient_21_7/libclntshcore.so.21.1 /lib/x86_64-linux-gnu/libclntshcore.so.21.1 \
#    && docker-php-ext-configure oci8 --with-oci8=shared,instantclient,/opt/oracle/instantclient_21_7,21.7 \
#    && docker-php-ext-install -j$(nproc) oci8 \
#    && docker-php-ext-configure pdo_oci --with-pdo-oci=shared,instantclient,/opt/oracle/instantclient_21_7,21.7 \
#    && docker-php-ext-install -j$(nproc) pdo_oci

#RUN docker-php-ext-install -j$(nproc) opcache

#RUN docker-php-ext-install -j$(nproc) pcntl

#RUN apt-get install -y freetds-bin freetds-dev freetds-common \
#    && docker-php-ext-install -j$(nproc) pdo_dblib

#RUN apt-get install -y libfbclient2 firebird-dev \
#    && docker-php-ext-install -j$(nproc) pdo_firebird

#RUN docker-php-ext-install -j$(nproc) pdo_mysql

#RUN apt-get install -y libpq-dev \
#    && docker-php-ext-install -j$(nproc) pdo_pgsql

#RUN apt-get install -y libpq-dev \
#    && docker-php-ext-install -j$(nproc) pgsql

#RUN apt-get install -y libpspell-dev \
#    && docker-php-ext-install -j$(nproc) pspell

#RUN docker-php-ext-install -j$(nproc) shmop

#RUN apt-get install -y libxml2 libxml2-dev \
#    && docker-php-ext-install -j$(nproc) simplexml

#RUN apt-get install -y libsnmp-dev \
#       && docker-php-ext-install -j$(nproc) snmp

#RUN apt-get install -y libxml2 libxml2-dev \
#    && docker-php-ext-install -j$(nproc) soap

#RUN docker-php-ext-install -j$(nproc) sockets

#RUN docker-php-ext-install -j$(nproc) sysvmsg

#RUN docker-php-ext-install -j$(nproc) sysvshm

#RUN apt-get install -y libargon2-dev \
RUN docker-php-ext-install -j$(nproc) tidy
RUN docker-php-ext-install -j$(nproc) tokenizer
#RUN docker-php-ext-install -j$(nproc) xml
#RUN docker-php-ext-install -j$(nproc) xmlreader
#RUN docker-php-ext-install -j$(nproc) xmlwriter
#RUN docker-php-ext-install -j$(nproc) xsl
#RUN docker-php-ext-install -j$(nproc) zend_test
#RUN docker-php-ext-install -j$(nproc) zip

#RUN docker-php-ext-install -j$(nproc) amqp
#RUN pecl install redis-4.1.1 && docker-php-ext-enable redis
#RUN pecl install xdebug && docker-php-ext-enable xdebug
#imagemagick \
 #        libgraphicsmagick1-dev \
 #        libmagickwand-dev \
#RUN pecl install imagick-3.4.3 && docker-php-ext-enable imagick

RUN apt-get autoremove && apt-get clean && rm -r /var/lib/apt/lists/*

COPY php.ini-development /usr/local/etc/php/php.ini
COPY conf.d/ /usr/local/etc/php/conf.d/

RUN sed -i s%/var/www/html%/var/www/html/\${PUBLIC_ROOT}%g  /etc/apache2/sites-enabled/000-default.conf

# resolve o problema que impedia o usuário www-data de gravar no diretório /var/www/html
RUN usermod --non-unique --uid 1000 www-data \
  && groupmod --non-unique --gid 1000 www-data \
  && chown -R www-data:www-data /var/www
