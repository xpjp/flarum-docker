# flarum-docker

Dockerized FLARUM

Japanese README is [here](https://github.com/xpjp/flarum-docker/blob/master/README.ja.md).

## Description

[FLARUM](http://flarum.org/) is a forum software made by PHP.

This repository contains dockerized FLARUM and compose files to operate with
nginx - PHP-fpm - MariaDB.

## How to use

Start:

1. Clone or download this repository.
1. Edit `docker-compose.yml` to fit your environment.
1. Start services with `docker-compose up -d data` command, then wait for MariaDB is available.
1. Start services with `docker-compose up -d` command.
1. Open `http://localhost/` with your browser.

Stop:

1. Stop and remove services with `docker-compose down` command.

If you want remove all data (assets, database), add `-v` option.

## Notes

- FLARUM config file usually placed on `/var/www/html/config.php`.
  It is removed on container is recreated. So I set symbolic link from `/var/www/html/assets/config.php`.
- Docker volumes `db-data` and `web-assets` should be persisted.
  Commented sections in `docker-compose.yml` would be helpful.
