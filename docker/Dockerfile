FROM php:7.4-fpm

ARG USER
ARG UID

RUN apt-get update && \
    apt-get install -y wget libcurl4-openssl-dev libicu-dev libonig-dev git && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    docker-php-ext-install json curl intl mbstring mysqli pdo_mysql

RUN useradd -U $USER -u $UID
RUN mkdir -m777 -p /home/$USER
RUN chown $USER /home/$USER
RUN echo "$USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

COPY ./php.ini /usr/local/etc/php/php.ini
RUN wget https://getcomposer.org/download/latest-2.x/composer.phar 
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN mkdir -p /var/www/project
WORKDIR /var/www/project

EXPOSE 8000 9003