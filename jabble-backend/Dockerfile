# Base image
FROM serversideup/php:8.3-fpm-nginx as base

# Development Image
FROM base as development
ARG USER_ID
ARG GROUP_ID

# Switch to root to change permissions and set user ID
USER root

# Set the "www-data" user to the same user and group that is running docker
RUN docker-php-serversideup-set-id www-data ${USER_ID}:${GROUP_ID}

# Switch back to the "www-data" user
USER www-data

# Set working directory
WORKDIR /var/www/html

# Copy the rest of the application files
COPY --chown=www-data:www-data . /var/www/html

RUN composer install


# Production Image
FROM base as production

# Set environment variable to enable OPcache
ENV PHP_OPCACHE_ENABLE=1

# Set working directory
WORKDIR /var/www/html

# Copy the application files
COPY --chown=www-data:www-data . /var/www/html

# Run Composer install for production
RUN composer install --no-dev --optimize-autoloader

