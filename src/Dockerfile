FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive
ARG TZ=Europe/Belfast

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
	npm \
    ttf-mscorefonts-installer

RUN apt install -y --no-install-recommends git openssh-client
RUN npm install -g yarn

RUN rm -rf /var/lib/apt/lists/*
RUN adduser pwuser

ENV PLAYWRIGHT_BROWSERS_PATH=/playwright-browsers

RUN mkdir /playwright-browsers && \
    mkdir /playwright-browser-downloader && \
    cd /playwright-browser-downloader && \
    npm init -y && npm i @playwright/test && \
    npx playwright install --with-deps && \
    rm -rf playwright-browser-downloader && \
    chmod -R 777 /playwright-browsers

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
