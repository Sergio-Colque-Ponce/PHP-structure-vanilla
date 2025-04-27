FROM php:8.2-apache

# Install common PHP extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Set working directory
WORKDIR /var/www/html

# Copy custom Apache config if needed (optional)
# COPY apache-config.conf /etc/apache2/sites-available/000-default.conf