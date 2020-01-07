FROM php:7.4.1-fpm

RUN apt-get update
RUN apt-get install -y libyaml-dev zstd libzstd-dev
RUN docker-php-ext-install pdo_mysql opcache
RUN pecl install zstd-0.7.7 \
  && docker-php-ext-enable zstd
RUN pecl install msgpack-2.0.3 \
  && docker-php-ext-enable msgpack
RUN pecl install yaml-2.0.4 \
  && docker-php-ext-enable yaml
RUN pecl download redis-5.1.1  \
  && tar xzvf redis-5.1.1.tgz \
  && cd redis-5.1.1 \
  && phpize \
  && ./configure --enable-redis-zstd --enable-redis-msgpack \
  && make \
  && make install \
  && docker-php-ext-enable redis
RUN pecl install xdebug-2.8.1 \
  && docker-php-ext-enable xdebug
RUN pecl install apcu-5.1.18 \
  && docker-php-ext-enable apcu

RUN echo 'error_reporting = E_ALL' >> /usr/local/etc/php/conf.d/99_myconf.ini
RUN echo 'date.timezone = Asia/Tokyo' >> /usr/local/etc/php/conf.d/99_myconf.ini