FROM php:8.0-fpm

# Debian Buster configuration
RUN apt update -y --fix-missing
RUN apt upgrade -y
RUN apt install -y apt-utils nano wget dialog software-properties-common build-essential git curl openssl

# PHP Module: mysql
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo

# PHP Module: json
RUN docker-php-ext-install tokenizer

# PHP Module: zip
RUN apt install -y libzip-dev unzip
RUN docker-php-ext-install zip

# PHP Module: intl
RUN apt install -y libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

# PHP Module: gd
RUN apt install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-install -j$(nproc) gd

# PHP Module: bcmath
RUN docker-php-ext-install bcmath

# PHP Module: imap
RUN apt install -y libc-client-dev libkrb5-dev
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap

# PHP Module: opcache
RUN docker-php-ext-enable opcache

# PHP Module: soap
#RUN apt install libxml2-dev -y
#RUN docker-php-ext-install soap

# Install xdebug
#RUN pecl install xdebug-2.9.2
#RUN docker-php-ext-enable xdebug

#Github Configs
## Github user var to be set in .env
RUN git config --global user.email GITHUB_USER_EMAIL \
    && git config --global user.name GITHUB_USER_NAME

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

#Symfony Cli
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN cp /root/.symfony/bin/symfony /usr/local/bin/symfony

#RUN composer install --no-interaction
## Install node
#RUN curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh
#RUN bash nodesource_setup.sh
#RUN apt-get install nodejs -y
#RUN command -v node

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

EXPOSE 9000

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]




