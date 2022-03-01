FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive

# Bash & apache setup
SHELL ["/bin/bash", "-c"]

RUN mkdir app-dir
RUN apt update
RUN apt install -y \
	php8.1 \
	git \
	yarn \
	libzip-dev \
	nodejs \
	mysql-client \
	php-mysql \
	php-gd \
	php-fileinfo \
	php-simplexml \
	php-mbstring \
	php-dom \
	php-zip \
	php-curl \
	npm

RUN npm i -g @playwright/test
RUN npx playwright install

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

WORKDIR /app-dir
