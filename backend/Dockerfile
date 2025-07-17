FROM php:8.4-apache

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git curl unzip zip libpng-dev libonig-dev libxml2-dev libzip-dev \
    && docker-php-ext-install pdo pdo_mysql mbstring zip exif pcntl

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Set working directory
WORKDIR /var/www/herca/backend

# Copy app source
COPY backend/ /var/www/herca/backend/

# Permissions
RUN chown -R www-data:www-data /var/www/herca/backend \
    && chmod -R 755 /var/www/herca/backend

# Install Composer
COPY --from=composer:2.7 /usr/bin/composer /usr/bin/composer
RUN composer install --no-interaction --optimize-autoloader

# Expose port 8000
EXPOSE 8000
