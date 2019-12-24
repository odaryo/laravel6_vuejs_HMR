# Nodeイメージ
FROM node:13-alpine as node

# PHPイメージ
FROM php:7.3-alpine

# Laravel環境に必要なパッケージをインストール
RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
        bash \
        git \
        unzip \
        libpng \
        libpng-dev \
        libjpeg \
        icu \
        icu-dev \
        icu-libs \
        libxml2 \
        libxml2-dev \
        openssl \
        openssl-dev \
    && docker-php-ext-install \
        pdo_mysql \
        mysqli \
        gd \
        mbstring \
        intl \
        xml \
        opcache \
    && docker-php-ext-enable intl mbstring \
    && apk --update --no-cache add autoconf g++ make \
    # xdebugインストール
    && pecl install -f xdebug \
    && docker-php-ext-enable xdebug \
    && apk del --purge autoconf g++ make

# Composerのインストール
RUN curl -sS https://getcomposer.org/installer | php ;mv composer.phar /usr/local/bin/composer;
RUN composer global require hirak/prestissimo \
    && composer global require phpunit/phpunit

# Nodeコンテナからyarnとnodeをコピー
COPY --from=node /opt/yarn-v* /opt/yarn
COPY --from=node /usr/local/bin/node /usr/local/bin/

# 使いやすいようにシンボリックリンク作成
RUN ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn \
    && ln -s /opt/yarn/bin/yarnpkg /usr/local/bin/yarnpkg

# ホスト側とuser_id, group_idを合わせる
RUN addgroup -g 1000 -S app-user && \
    adduser -u 1000 -S app-user -G app-user

USER app-user:app-user

# Setup working directory
WORKDIR /app
