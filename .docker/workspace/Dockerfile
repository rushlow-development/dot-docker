ARG PHP_VERSION

FROM php:${PHP_VERSION}-cli-bullseye

# Install dependencies
RUN apt-get update && apt-get install -yqq \
    libzip-dev \
    zip \
    unzip \
    wget \
    gnupg \
    git \
    libsodium-dev \
    libsodium23 \
    libcurl4-openssl-dev \
    libxslt1-dev \
    libxslt1.1 \
    libicu67 \
    libicu-dev \
    libpq-dev \
    chromium \
    chromium-driver \
    firefox-esr

RUN apt-get install -yqq \
    postgresql-client \
    mariadb-client


RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install sodium
RUN docker-php-ext-install xsl
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install exif
RUN docker-php-ext-install soap
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install curl

# Install node and yarn
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get install -yqq \
    nodejs \
    yarn

# Create a regular user account to work from
RUN set -xe; \
    groupadd -g 1000 developer && \
    useradd -u 1000 -g developer -m developer && \
    usermod -p "*" developer -s /bin/bash

# Install composer & make composer global
RUN curl -s https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Add cache location for composer
RUN mkdir /.composer && chown developer:developer /.composer

# Cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Symfony Installer
RUN wget https://get.symfony.com/cli/installer -O - | bash

# Make Symfony Global
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

COPY php.ini /usr/local/etc/php/php.ini

# Set which account to use
USER developer

# Set working dir for container
WORKDIR /var/htdocs
