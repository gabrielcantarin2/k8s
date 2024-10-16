FROM php:8.1-apache

# Install necessary extensions (add more if needed)
RUN docker-php-ext-install pdo pdo_mysql mbstring

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html

# Copy only necessary files first to leverage Docker cache
COPY composer.json composer.lock ./
RUN composer install --no-interaction --no-dev --optimize-autoloader

COPY . .

# Generate application key
RUN php artisan key:generate

# Run database migrations (if needed)
# RUN php artisan migrate --force

# Expose port 80
EXPOSE 80

# Start Apache
CMD ["apache2-foreground"]
