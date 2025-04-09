FROM php:8.4-fpm

# Instala dependências
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
    && pecl install -f xdebug \
    && docker-php-ext-enable xdebug \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Composer (direto da imagem oficial)
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Define diretório de trabalho
WORKDIR /var/www/html

# Copia o código-fonte do host (redundante por volume, mas útil no build inicial)
COPY ./ /var/www/html
