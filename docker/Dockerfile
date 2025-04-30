FROM php:8.1-apache

# Install PHP extensions needed by Yii2
RUN apt-get update && apt-get install -y \
    libpng-dev libjpeg-dev libonig-dev libxml2-dev unzip git \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Enable Apache rewrite module
RUN a2enmod rewrite

# Set working directory
WORKDIR /var/www/html

# Copy Yii2 app into container
COPY ../ /var/www/html/

# Set proper permissions (skip errors if dirs don't exist)
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 775 /var/www/html/runtime /var/www/html/web/assets || true

# Fix Apache config
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf \
 && sed -i "s|DocumentRoot /var/www/html|DocumentRoot /var/www/html/web|g" /etc/apache2/sites-available/000-default.conf

