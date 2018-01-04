# flarum-docker

FLARUMをDocker化します

英語バージョンは[こちら](https://github.com/xpjp/flarum-docker/blob/master/README.md)

## Description

[FLARUM](http://flarum.org/)はPHP製のフォーラムソフトウェアです。

このリポジトリにはFLARUMをDocker化するDockerfileや`nginx - PHP-fpm - MariaDB`の構成で
動作させるためのDocker compose関連ファイルがあります。

## 使い方

起動:

1. このリポジトリをCloneまたはダウンロードします。
1. 環境に合わせて`docker-compose.yml`を編集します。
1. `docker-compose up -d database`コマンドを実行し、MariaDBを起動します。
   データベースが利用可能になるまで少々時間がかかります。
1. `docker-compose up -d`コマンドを実行します。
1. ちょっと待ってからブラウザで`http://localhost/`を開きます。

終了:

1. `docker-compose down`コマンドを実行します。

assetsやデータベースのデータを削除するには`-v`オプションを追加します。

## メモ

- FLARUMの設定ファイルは通常`/var/www/html/config.php`に作られます。
  そこはコンテナを作り変える度に消えてしまうので、`/var/www/html/assets/config.php`から
  シンボリックリンクを貼ることでassetsに設定ファイルの実体が置かれるようにしています。
- Dockerボリュームの`db-data`と`web-assets`は永続化(消えないように)するべきです。
  `docker-compose.yml`を参考にしてください。
