# Version: 1.0
FROM php:7.1-apache

# ADD 000-default.conf /etc/apache2/sites-enabled/

# Instalar dependencias.
RUN apt update && \
    apt install -y curl git wget nano
RUN apt-get update && \
    apt-get install -y libmagickwand-dev --no-install-recommends && \
    pecl install imagick && \
    docker-php-ext-enable imagick
RUN apt-get update && \
    apt-get install -y zlib1g-dev libmcrypt-dev

# Instalar  dependencias de PHP.
RUN docker-php-ext-install mysqli 
RUN docker-php-ext-install bcmath 
RUN docker-php-ext-install pdo_mysql 
RUN docker-php-ext-install mcrypt 
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install zip
RUN docker-php-ext-install soap
RUN apt-get update && apt-get install -y libwebp-dev libxpm-dev && \
    docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir \
    --with-png-dir --with-zlib-dir --with-xpm-dir --with-freetype-dir \
    --enable-gd-native-ttf
RUN docker-php-ext-install gd
RUN apt-get update && \
    apt-get install -y libxslt-dev && \
    docker-php-ext-install xsl
RUN docker-php-ext-install intl

# Instalar composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"

# Composer de forma global
RUN mv composer.phar /usr/local/bin/composer

RUN a2enmod rewrite
