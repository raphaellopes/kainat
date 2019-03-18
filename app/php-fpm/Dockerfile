FROM php:fpm-alpine
MAINTAINER Raphael <ph.campanario07@gmail.com>
LABEL description="WP Base PHP FPM"

RUN \
  docker-php-ext-install \
  mbstring \
  mysqli

CMD ["php-fpm"]
