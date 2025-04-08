FROM php:8.4-fpm

# Instala dependências do sistema
RUN apt-get update && apt-get install -y \
    git \
    curl \
    unzip \
    zip \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    libicu-dev \
    autoconf \
    gcc \
    make \
    && docker-php-ext-install \
    pdo \
    pdo_mysql \
    mbstring \
    zip \
    xml \
    intl \
    && echo '' | pecl install -f xdebug \
    && docker-php-ext-enable xdebug \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Copia o Composer diretamente da imagem oficial
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Define diretório de trabalho
WORKDIR /var/www/html

# Copia o código-fonte do host para o container
COPY ./ /var/www/html

# Copia as configurações do PHP (php.ini, xdebug.ini)
COPY .docker/php/conf.d/php.ini /usr/local/etc/php/conf.d/php.ini
COPY .docker/php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
