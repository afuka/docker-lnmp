ARG PHP_VERSION
ARG PHP_REDIS_VERSION
ARG SWOOLE_VERSION
ARG AMQP_VERSION

FROM daocloud.io/php:$PHP_VERSION-fpm-alpine

COPY config/php.ini /usr/local/etc/php

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN cd ~ \
    && wget https://github.com/swoole/swoole-src/archive/v$SWOOLE_VERSION.tar.gz --no-check-certificate \
    && tar -zxvf v$SWOOLE_VERSION.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv swoole-src-$SWOOLE_VERSION /usr/src/php/ext/swoole \
    && docker-php-ext-install swoole

RUN cd ~ \
    && wget https://pecl.php.net/get/amqp-$AMQP_VERSION.tgz --no-check-certificate \
    && tar -zxvf amqp-$AMQP_VERSION.tgz \
    && mv amqp-$AMQP_VERSION /usr/src/php/ext/amqp \
    && apk add rabbitmq-c-dev \
    && docker-php-ext-install amqp \
    && apk add libstdc++ libpng-dev

RUN cd ~ \
    && wget https://github.com/phpredis/phpredis/archive/$PHP_REDIS_VERSION.tar.gz --no-check-certificate \
    && tar -zxvf $PHP_REDIS_VERSION.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-$PHP_REDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis 

RUN docker-php-ext-install pdo_mysql mysqli pcntl gd sockets soap

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
