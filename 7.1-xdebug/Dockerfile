FROM php:7.1-apache

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions mysqli soap pdo_mysql intl sqlsrv pdo_sqlsrv xdebug

RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

