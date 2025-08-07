# Gunakan image PHP-FPM sebagai base
FROM php:8.2-fpm

# Instal dependensi sistem yang dibutuhkan
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    libicu-dev \
    libssl-dev \
    libjpeg-dev \
    libfreetype-dev \
    libmcrypt-dev \
    locales

# Menginstal ekstensi PHP yang dibutuhkan
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd intl soap opcache \
    && docker-php-ext-enable pdo_mysql opcache \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Konfigurasi locale
RUN echo "id_ID.UTF-8 UTF-8" >> /etc/locale.gen \
    && dpkg-reconfigure --frontend=noninteractive locales \
    && locale-gen id_ID.UTF-8 \
    && /usr/sbin/update-locale LANG=id_ID.UTF-8

# Menginstal Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Atur direktori kerja di dalam container
WORKDIR /var/www/html

# Salin kode aplikasi dari host ke container
COPY . .

# Instal dependensi Composer
RUN composer install --no-dev --optimize-autoloader

# Menjalankan migrasi database dan seeder
RUN php artisan migrate --force --seed

# Beri izin kepada direktori penyimpanan dan cache
RUN chown -R www-data:www-data /var/www/html/storage \
    && chown -R www-data:www-data /var/www/html/bootstrap/cache \
    && chmod -R 775 /var/www/html/storage \
    && chmod -R 775 /var/www/html/bootstrap/cache

# Atur Nginx
COPY ./nginx/nginx.conf /etc/nginx/sites-available/default
RUN ln -sf /etc/nginx/sites-available/default /etc/nginx/sites-enabled/
RUN rm /etc/nginx/sites-available/default
RUN rm /etc/nginx/sites-enabled/default

# Expose port
EXPOSE 9000

# Jalankan PHP-FPM
CMD ["php-fpm"]