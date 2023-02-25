FROM php:8.1-fpm

ARG UID

# Create user and some useful stuff
RUN adduser -u ${UID} --disabled-password --gecos "" appuser
RUN mkdir /home/appuser/.ssh
RUN chown -R appuser:appuser /home/appuser/
RUN echo "StrictHostKeyChecking no" >> /home/appuser/.ssh/config
RUN echo "export COLUMNS=300" >> /home/appuser/.bashrc
RUN echo "alias sf=/usr/bin/console" >> /home/appuser/.bashrc

RUN apt update && \
    apt-install -y curl wget zip unzip

# Install PHP extensions
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions opcache \
                           intl \
                           pdo_mysql \
                           pdo_sqlsrv \
                           xdebug

RUN echo 'memory_limit = 512M' >> /usr/local/etc/php/conf.d/docker-php-ram-limit.ini

RUN rm -rf /var/lib/apt/lists/*

COPY ./xdebug.ini "${PHP_INI_DIR}/conf.d"

# Install and update composer
RUN curl https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer
RUN composer self-update

# Install lastest version of Symfony CLI
RUN curl -sS https://get.symfony.com/cli/installer | bash


# Install fnm (Fast Node Manager)
RUN curl -fsSL https://fnm.vercel.app/install | bash
# Install lastest version of Node.js
RUN fmn install
# Enable corepack for yarn
RUN corepack enable

RUN mkdir /app
WORKDIR /app
