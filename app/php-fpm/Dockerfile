FROM php:7.2-fpm-alpine

RUN apk upgrade --update && \
    apk add --no-cache libpng-dev libjpeg-turbo-dev && \
    docker-php-ext-configure gd \
      --with-gd \
      --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install mbstring \
      mysqli \
      gd


CMD ["php-fpm"]
