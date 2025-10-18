# Temel imaj: PHP 7.2 + Apache (EOL ama Docker Hub'da mevcut)
FROM php:7.2-apache

# Sistem kütüphaneleri ve PHP eklentileri
RUN apt-get update && apt-get install -y \
    git unzip \
    libzip-dev \
    libpng-dev libjpeg-dev libfreetype6-dev \
    libicu-dev \
    libxml2-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) \
       mysqli pdo pdo_mysql mbstring xml intl zip gd \
    && a2enmod rewrite

# Composer yükle (projende gerekirse)
RUN curl -fsSL https://getcomposer.org/installer -o /tmp/composer-setup.php \
 && php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer \
 && rm /tmp/composer-setup.php

# Apache, Codespaces içinde foreground çalışır (php:7.2-apache default CMD)
EXPOSE 80
