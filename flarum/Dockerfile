FROM php:7.1-fpm

ARG \
  FLARUM_VERSION=v0.1.0-beta.7
ENV \
  COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/tmp

RUN \
  echo "memory_limit=-1" > "$PHP_INI_DIR/conf.d/memory-limit.ini" && \
  echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "$PHP_INI_DIR/conf.d/date_timezone.ini" && \
  \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    libgd-dev unzip && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install -j$(nproc) pdo_mysql gd && \
  \
  php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');" && \
  php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
  php -r "unlink('/tmp/composer-setup.php');" && \
  \
  chown www-data:www-data /var/www/html

USER www-data
WORKDIR /var/www/html

# Add flarum
RUN \
  composer create-project flarum/flarum=${FLARUM_VERSION} . --stability=beta && \
  composer clear-cache

# Symlink config.php to move into Docker volume
RUN \
  ln -s assets/config.php config.php

VOLUME ["/var/www/html", "/var/www/html/assets"]
