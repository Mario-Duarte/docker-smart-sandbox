FROM php:7.4-apache

# Update OS
RUN apt-get update
RUN apt-get install -y wget git zip unzip openssl zlib1g-dev libcurl3-dev libzip-dev libpng-dev libxml2-dev libmcrypt-dev git

# Install PHP extensions needed
RUN docker-php-ext-install -j$(nproc) mysqli pdo_mysql json curl gd zip pcntl exif intl

# Generate self signed certificate
# Please change this line acording to your needs
RUN cd /var/www && mkdir conf
RUN openssl req \
  -newkey rsa:4096 -nodes -sha256 -keyout /var/www/conf/domain.key \
  -x509 -days 365 -out /var/www/conf/domain.crt \
  -subj "/C=UK/ST=London/L=London/O=OrgName/OU=IT Department/CN=dev.sandbox.com" \
  -addext "subjectAltName=DNS.1:dev.sandbox.com"

# Enable common Apache modules
RUN a2enmod headers expires rewrite ssl

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

# Install lataste stable NodeJS version
RUN apt-get install -y nodejs npm
RUN npm install -g n && n stable

# Set working directory
WORKDIR /var/www/html