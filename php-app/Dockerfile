# Use PHP 8.2 FPM as the base image
FROM php:8.2-fpm

# Set working directory
WORKDIR /var/www/html

# Install system dependencies
RUN apt-get update && apt-get install -y \
    nginx \
    libmariadb-dev \
    libpq-dev \
    libonig-dev \
    zip \
    unzip \
    git \
    curl \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions required for Laravel
RUN docker-php-ext-install pdo pdo_mysql mbstring

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set environment variable to allow Composer to run as root
ENV COMPOSER_ALLOW_SUPERUSER=1

# Copy the entire application code (including artisan file) first
COPY . .

# Install Laravel dependencies
RUN composer install --no-interaction --no-dev --optimize-autoloader --ignore-platform-reqs

# Set correct ownership for files
RUN chown -R www-data:www-data /var/www/html

# Copy Nginx configuration
COPY nginx.conf /etc/nginx/sites-available/default

# Expose port 80 for Nginx
EXPOSE 80

# Start both PHP-FPM and Nginx
CMD service nginx start && php-fpm
