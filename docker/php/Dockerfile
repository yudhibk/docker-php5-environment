FROM php:5.6-fpm-stretch

# Fix apt sources for Debian Stretch (archived)
RUN echo "deb http://archive.debian.org/debian stretch main contrib non-free" > /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian-security stretch/updates main contrib non-free" >> /etc/apt/sources.list \
    && echo "Acquire::Check-Valid-Until false;" > /etc/apt/apt.conf.d/99no-check-valid \
    && echo "Acquire::AllowInsecureRepositories true;" >> /etc/apt/apt.conf.d/99no-check-valid \
    && echo "Acquire::AllowDowngradeToInsecureRepositories true;" >> /etc/apt/apt.conf.d/99no-check-valid

RUN apt-get update && apt-get install -y \
    --allow-unauthenticated \
    --fix-missing \
    git \
    curl \
    zip \
    unzip \
    zlib1g-dev \
    libpng-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libxml2-dev \
    libmcrypt-dev \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include \
        --with-jpeg-dir=/usr/include \
    && docker-php-ext-install \
        pdo \
        pdo_mysql \
        mysqli \
        mysql \
        mbstring \
        intl \
        gd \
        mcrypt \
        xml

# Install Composer 1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin \
    --filename=composer \
    --version=1.10.26

WORKDIR /var/www/html