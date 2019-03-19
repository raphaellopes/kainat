FROM php:fpm-alpine

RUN \
  docker-php-ext-install \
  mbstring \
  mysqli

CMD ["php-fpm"]
