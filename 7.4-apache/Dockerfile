FROM php:7.4-apache

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions mysqli soap pdo_mysql intl sqlsrv pdo_sqlsrv xdebug

RUN echo 'memory_limit = 512M' >> /usr/local/etc/php/conf.d/docker-php-ram-limit.ini

RUN rm -rf /var/lib/apt/lists/*

COPY ./xdebug.ini "${PHP_INI_DIR}/conf.d"