FROM php:7.3-fpm

# Install ldap dependencies
RUN apt-get update && apt-get install -y build-essential \
    curl \
    gifsicle \
    jpegoptim \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libldap2-dev \
    libpng-dev \
    libpq-dev \
    libxml2-dev \
    libzip-dev \
    locales \
    optipng \
    pngquant \
    unzip \
    zip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install exif mbstring pcntl pdo pdo_pgsql soap zip intl
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/
RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/

ENV PHPREDIS_VERSION 3.0.0

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Change current user to www
USER www

EXPOSE 9000
CMD ["php-fpm"]
