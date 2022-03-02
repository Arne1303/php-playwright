FROM mcr.microsoft.com/playwright:v1.19.0-focal
RUN apt update

# Adding php repository
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:ondrej/php

# Installing php
RUN apt install -y \
    libzip-dev \
    mysql-client \
	php8.1 \
	php8.1-mysql \
	php8.1-gd \
	php8.1-fileinfo \
	php8.1-simplexml \
	php8.1-mbstring \
	php8.1-dom \
	php8.1-zip \
	php8.1-curl

# Clearing cache
RUN rm -rf /var/lib/apt/lists/*

# Installing composer, just in case someone needs it
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
