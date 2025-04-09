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

# Instalação do SonarScanner
RUN apt-get update && \
    apt-get install -y curl unzip openjdk-17-jre && \
    curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip && \
    unzip sonar-scanner.zip -d /opt && \
    ln -s /opt/sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner && \
    rm sonar-scanner.zip


# Composer (direto da imagem oficial)
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Define diretório de trabalho
WORKDIR /var/www/html

# Copia o código-fonte do host (redundante por volume, mas útil no build inicial)
COPY ./ /var/www/html
