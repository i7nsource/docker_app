# Используем образ PHP 8.0 FPM
FROM php:8.2-fpm

# Обновляем APT и устанавливаем необходимые зависимости
RUN apt-get update && apt-get install -y \
    apt-utils \
    libpq-dev \
    libpng-dev \
    libzip-dev \
    zip \
    unzip \
    git \
    freetds-dev \
    freetds-bin \
    libonig-dev \
    libcurl4-openssl-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Устанавливаем расширения PHP
RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install curl

# Копируем пользовательский php.ini
COPY ./_docker/app/php.ini /usr/local/etc/php/conf.d/php.ini

# Устанавливаем драйвер Sybase
RUN docker-php-ext-configure pdo_dblib --with-libdir=lib/x86_64-linux-gnu \
    && docker-php-ext-install pdo_dblib

# Устанавливаем Composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

# Устанавливаем рабочую директорию
WORKDIR /var/www
