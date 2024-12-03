FROM php:8.0-cli

ENV DEBIAN_FRONTEND=noninteractive
ENV TERM=xterm-color

ARG DEV_MODE
ENV DEV_MODE=$DEV_MODE

COPY --from=composer:2.8 /usr/bin/composer /usr/bin/
COPY ./rootfilesystem/ /

RUN \
    set -ex && \
    apt-get update  && \
    apt-get install -y \
        libcurl4-openssl-dev       \
        libbrotli-dev              \
        libpq-dev                  \
        libssl-dev                 \
        libzip-dev                 \
        libicu-dev                 \
        libpq-dev                  \
        supervisor                 \
        unzip                      \
        zip                        \
        zlib1g-dev                 \
        --no-install-recommends && \
# Enable pgsql
    docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install -j$(nproc) \
# PHP extension pdo_mysql is included since 4.8.12+ and 5.0.1+.
            zip \
            intl \
            pgsql \
            pdo_mysql \
            pdo_pgsql && \
    install-swoole.sh 5.0.3 \
        --enable-mysqlnd      \
        --enable-swoole-pgsql \
        --enable-brotli       \
        --enable-openssl      \
        --enable-sockets --enable-swoole-curl && \
    mkdir -p /var/log/supervisor && \
    rm -rf /var/lib/apt/lists/* /usr/bin/qemu-*-static

ENTRYPOINT ["/entrypoint.sh"]
CMD []

WORKDIR "/var/www/"
