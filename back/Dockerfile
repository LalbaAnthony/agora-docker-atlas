FROM php:8.2-fpm

# Set working directory
WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev \
    libonig-dev \
    libxml2-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath gd soap

# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set proper permissions for the application directory
RUN chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html

# Copy application files
COPY --chown=www-data:www-data . /var/www/html

# Switch to non-root user for Composer operations
USER www-data

# Create .env
RUN if [ ! -f .env ]; then cp .env.example .env; fi
RUN if [ ! -f .env ]; then touch .env; fi
RUN if [ ! -f .env ]; then echo "APP_KEY=base64:$(openssl rand -base64 32)" >> .env; fi

# Install dependencies
RUN composer install --no-interaction --no-progress

# Generate application key if needed
RUN php artisan key:generate --force || true

# Create storage link if needed
RUN php artisan storage:link || true

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
