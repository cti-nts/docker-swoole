FROM php:8.2-cli-alpine3.20

COPY --from=composer:2.8 /usr/bin/composer /usr/bin/

RUN \
    set -ex && \
    apk update && \
    apk add --no-cache libstdc++ libpq && \
    apk add --no-cache --virtual .build-deps $PHPIZE_DEPS curl-dev linux-headers brotli-dev postgresql-dev openssl-dev pcre-dev pcre2-dev zlib-dev && \
# PHP extension pdo_mysql is included since 4.8.12+ and 5.0.1+.
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install sockets && \
    docker-php-source extract && \
    mkdir /usr/src/php/ext/swoole && \
    curl -sfL https://github.com/swoole/swoole-src/archive/v5.0.3.tar.gz -o swoole.tar.gz && \
    tar xfz swoole.tar.gz --strip-components=1 -C /usr/src/php/ext/swoole && \
    docker-php-ext-configure swoole \
        --enable-mysqlnd      \
        --enable-swoole-pgsql \
        --enable-brotli       \
        --enable-openssl      \
        --enable-sockets --enable-swoole-curl && \
    docker-php-ext-install -j$(nproc) swoole && \
    rm -f swoole.tar.gz && \
    docker-php-source delete && \
    apk del .build-deps

WORKDIR "/var/www/"
