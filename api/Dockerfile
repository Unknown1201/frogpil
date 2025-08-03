
FROM webdevops/php-apache:8.2

# Set working directory
WORKDIR /app

# Copy all project files
COPY . .

# Install PHP extensions and system packages
RUN apt-get update && apt-get install -y unzip zip libzip-dev libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel dependencies
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Set permissions for Laravel to write
RUN chown -R application:application /app \
    && chmod -R 775 storage bootstrap/cache

# Laravel setup during build (safe for Render Free plan)
RUN cp .env.example .env \
    && php artisan config:clear \
    && php artisan key:generate \
    && php artisan migrate --force \
    && php artisan db:seed --force \
    && php artisan storage:link

EXPOSE 80
