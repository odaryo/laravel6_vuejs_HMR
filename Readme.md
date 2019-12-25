# Laravel6 + Vue.js + HMR on Docker

Docker環境（非Laradock）でLaravel-Mixを使用したホットリロードを行うサンプル

# インストール方法

## download

```bash
$ git clone https://github.com/odaryo/laravel6_vuejs_HMR.git
```

## docker起動

```bash
$ cd laravel6_vuejs_HMR
$ docker-compose build
$ docker-compose up -d
```

## laravel設定

```bash
$ docker-compose run --rm app composer install
$ docker-compose run --rm app cp .env.example .env
$ docker-compose run --rm app php artisan key:generate
```

一度docker再起動

```bash
$ docker-compose up -d
```

## node_moduleインストール

```bash
$ docker-compose exec app yarn 
```

## HMR起動

```bash
$ docker-compose exec app yarn hot
```

# 確認

http://localhost:8080
