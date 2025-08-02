FROM webdevops/php-apache:8.2

WORKDIR /app

# Copy Laravel project files
COPY . .

# Install PHP extensions needed for PostgreSQL and zip
RUN apt-get update && apt-get install -y unzip zip libzip-dev libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel PHP dependencies
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Set Laravel app key and default .env
RUN cp .env.example .env && php artisan key:generate

# Apache will run automatically in this image
EXPOSE 80
