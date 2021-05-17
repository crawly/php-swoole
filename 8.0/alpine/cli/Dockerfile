FROM php:8.0-alpine

RUN apk add --no-cache $PHPIZE_DEPS git openssl-dev oniguruma-dev libzip-dev curl curl-dev \
  && docker-php-ext-install pcntl sockets opcache

RUN git clone https://github.com/swoole/swoole-src.git \
  && cd swoole-src \
  && git checkout v4.6.7 \
  && phpize \
  && ./configure \
  --enable-sockets \
  --enable-openssl \
  --enable-http2 \
  --enable-swoole-curl \
  --enable-swoole-json \
  && make && make install

RUN touch /usr/local/etc/php/conf.d/swoole.ini && \
    echo 'extension=swoole.so' > /usr/local/etc/php/conf.d/swoole.ini