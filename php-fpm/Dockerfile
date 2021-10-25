FROM php:7.4-fpm as php-base

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmcrypt-dev \
        libxml++2.6-dev \
        libcurl3-dev \
        libxpm-dev \         
        python git \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd 
    
RUN docker-php-ext-install \
    curl \
    xml\
    sockets \
    intl \
    bcmath \
    pdo \
    mysqli \
    pdo_mysql

EXPOSE 9000

WORKDIR /var/www

FROM php-base

RUN apt-get update -y && \
    apt-get install -y openssh-client && \
    mkdir -p /home/www-data/.ssh && \
    chmod 777 /home/www-data/.ssh 

RUN curl -LO https://deployer.org/deployer.phar && \
    mv deployer.phar /usr/local/bin/dep && \
    chmod +x /usr/local/bin/dep

COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

USER www-data

WORKDIR /var/www
