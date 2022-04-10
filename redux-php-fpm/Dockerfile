FROM php:fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libonig-dev \
        libzip-dev \
        sendmail \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-install zip

RUN sed -i \
-e 's/^;\(security.limit_extensions = .php .php3 .php4 .php5 .php7\)/\1 .phtml/' \
/usr/local/etc/php-fpm.d/www.conf

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini 

RUN sed -i '/#!\/bin\/sh/aservice sendmail restart' /usr/local/bin/docker-php-entrypoint

RUN sed -i '/#!\/bin\/sh/aecho "$(hostname -i)\t$(hostname) $(hostname).localhost" >> /etc/hosts' /usr/local/bin/docker-php-entrypoint

EXPOSE 9000
