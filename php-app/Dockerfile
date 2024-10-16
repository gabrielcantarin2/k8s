FROM php:8.1-apache # Use the official PHP Apache image

# Install necessary extensions
RUN docker-php-ext-install pdo pdo_mysql

# Set working directory
WORKDIR /var/www/html

# Copy composer files
COPY composer.json composer.lock ./

# Install dependencies
RUN composer install --no-interaction --no-dev --optimize-autoloader

# Copy application code
COPY . .

# Expose port 80
EXPOSE 80

# Start Apache
CMD ["apache2-foreground"]
