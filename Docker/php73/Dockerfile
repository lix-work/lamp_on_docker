# 公式phpのタグ「7.3-apache」イメージをベースとする
FROM php:7.3-apache

# apacheのrewriteモジュールを有効にする
# llコマンドエイリアス
RUN a2enmod rewrite && alias ll='ls -la'

# 各種パッケージ、PHP拡張モジュールのインストール
RUN apt-get update && apt-get install -y \
    vim \
    libicu-dev \
    zip \
    unzip \
&& docker-php-ext-install -j$(nproc) intl \
&& docker-php-ext-install -j$(nproc) pdo_mysql \
&& docker-php-ext-install -j$(nproc) opcache 

# php.iniへの上書き設定
RUN { \
  echo 'upload_max_filesize = 100M'; \
  echo 'post_max_size = 108M'; \
  echo 'date.timezone=Asia\Tokyo'; \
  echo 'max_file_uploads=100'; \
  echo 'memory_limit=256M'; \
  echo 'max_execution_time=120'; \
} > /usr/local/etc/php/conf.d/overrides.ini

# OSのタイムゾーンを東京にしておく
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# ドキュメントルートの一つ上(\var\www)をapacheユーザ所有にしておく
RUN chown -R www-data:www-data /var/www

# apacheのリロードは不要
#RUN service apache2 reload
