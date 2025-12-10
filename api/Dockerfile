# api/Dockerfile
FROM php:8.2-fpm-bookworm

# Laravel10に必要なPHP拡張モジュール
# libpq-devは，postgresを使う際に必要なライブラリ
# Laravelインストール時にgit, zip, unzipが必要
RUN apt-get update && apt-get install -y \
  git \
  zip \
  unzip \
  libpq-dev \
  libpng-dev \
  libjpeg-dev \
  # PHP拡張をビルド & インストールするためのスクリプト
  && docker-php-ext-install \
    pdo_pgsql \
    pdo_mysql \
  # 画像処理に必要なGDライブラリ
    gd \
  # インストール済みの不要なキャッシュを削除
  && apt-get clean \
  # APT のパッケージリスト削除
  && rm -rf /var/lib/apt/lists/*

# マルチステージビルドを使って常に最新の`composer`をインストールする
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# composer の memory-limit 無制限
ENV COMPOSER_MEMORY_LIMIT=-1

# Laravelの標準的なドキュメントルート
WORKDIR /var/www/html

# php-fpmはポート番号9000使用する
EXPOSE 9000

# コンテナ起動時に PHP-FPM を開始する（明示的に指定）
CMD ["php-fpm"]
