FROM php:7.4.2-fpm

# COPY php.ini
COPY ./Docker/php/php.ini /usr/local/etc/php/php.ini

# Composer install
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin

# install Node.js
COPY --from=node:14.18.2 /usr/local/bin /usr/local/bin
COPY --from=node:14.18.2 /usr/local/lib /usr/local/lib

RUN apt-get update && \
    apt-get -y install \
    git \
    zip \
    unzip \
    vim \
    wget \
    gpg \
    # GD Libraryインストール1
    libonig-dev \
    libfreetype6-dev \ 
    libjpeg62-turbo-dev \
    libpng-dev \
    libjpeg-dev \
    # ここまで
    && docker-php-ext-install pdo_mysql bcmath \
    # GD Libraryインストール2(先に1を入れておかないといけない？)
    && docker-php-ext-install \ 
                pdo_mysql \ 
                bcmath \
                gd \
    && docker-php-ext-configure gd \
                --with-freetype=/usr/include/ \
                --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

WORKDIR /var/www/html

# RUN composer global require "laravel/installer"