FROM php:7.4-fpm as php-base

# PHP EXTENSIONS
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/
RUN chmod uga+x /usr/local/bin/install-php-extensions \
    && sync \
    && install-php-extensions --cleanup gd intl pdo_pgsql soap zip bcmath xmlrpc mbstring pcntl pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

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
