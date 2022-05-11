FROM php:8.1.5-fpm

RUN apt-get update && apt-get full-upgrade -y && apt-get install -y \
    apt-utils \
    libpq-dev \
    libpng-dev \
    libjpeg-dev \
    libzip-dev \
    git \
    libmagickwand-dev \
    unzip && \
    pecl install -o -f redis && \
    pecl install -o -f xdebug && \
    pecl install -o -f imagick && \
    rm -rf /tmp/pear && \
    docker-php-ext-enable imagick && \
    docker-php-ext-enable redis && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gd && \
    docker-php-ext-install zip && \
    docker-php-ext-enable xdebug && \
    apt-get autoremove --purge && \
    apt-get autoclean && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rm /usr/local/etc/php-fpm.d/zz-docker.conf

COPY ./services/php/conf/zz-docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf

RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

WORKDIR /var/www

