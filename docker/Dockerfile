#FROM php:8.1-apache

#RUN apt-get update && apt-get install -y \
#    git \
#    unzip \
#    libzip-dev \
#    && docker-php-ext-install pdo_mysql zip

#WORKDIR /var/www/html

#COPY . /var/www/html

# Serve from /web directory
#RUN sed -i 's|DocumentRoot /var/www/html|DocumentRoot /var/www/html/web|g' /etc/apache2/sites-available/000-default.conf

# Add DirectoryIndex and permissions
#RUN mkdir -p /var/www/html/runtime /var/www/html/web/assets && \
#    chown -R www-data:www-data /var/www/html/runtime /var/www/html/web/assets && \
#    chmod -R 775 /var/www/html/runtime /var/www/html/web/assets

#RUN a2enmod rewrite

# Fix DirectoryIndex issue
#RUN echo "<Directory /var/www/html/web>\n\
#    Options Indexes FollowSymLinks\n\
#    AllowOverride All\n\
#    Require all granted\n\
#    DirectoryIndex index.php index.html\n\
#</Directory>" >> /etc/apache2/apache2.conf

#EXPOSE 80
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

