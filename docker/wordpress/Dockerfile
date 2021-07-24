ARG PHP=7.4
FROM wordpress:php$VERSION-fpm-alpine

COPY --from=wordpress:cli-php7.4 /usr/local/bin/wp /usr/local/bin/wp

RUN apk --no-cache --virtual .build-deps add \
        autoconf gcc make g++ zlib-dev  && \
    docker-php-ext-install -j$(nproc) bcmath mysqli pdo pdo_mysql && \
    pecl install redis && \
    docker-php-ext-enable redis && \
    cp "/usr/local/etc/php/php.ini-production" "/usr/local/etc/php/php.ini" && \
    apk del .build-deps
