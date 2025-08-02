# ✅ Use correct base image with Apache
FROM webdevops/php-apache:8.2

# Set working directory
WORKDIR /app

# Copy code
COPY . .

# Install system dependencies and PHP extensions
RUN apt-get update && apt-get install -y unzip zip libzip-dev libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel dependencies
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Set permissions
RUN chown -R application:application /app

# Laravel setup
RUN cp .env.example .env && php artisan key:generate

# Expose default web port
EXPOSE 80

# Start Apache (already handled by this image, no CMD needed)
