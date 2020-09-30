
# Docker LAMP 環境

LAMP とは「Linux, Apache, MySQL, PHP」を組み合わせた開発環境のこと

- MySQL
    - v5.7.31
    - Debian
- phpMyAdmin
- Apache / PHP (同環境)
    - Apache
        - v2.4.38
    - PHP
        - v7.4.10
    - Debian

## ブラウザ URL アクセス方法

- PHP ファイルアクセス ※ 80 番ポート
    - `index.html` にアクセス
        - http://localhost/index.html:80 または http://localhost/index.html または http://localhost または localhost
    - `index.php` にアクセス
        - http://localhost/index.php:80 または http://localhost/index.php または http://localhost または localhost
    - `phpinfo.php` にアクセス
        - http://localhost/phpinfo.php
- phpMyAdmin ※ 8080 番ポート
    - http://localhost:8080/

# Docker 仮想環境のログイン方法

## MySQL

- ユーザ
    - `root`
- パスワード
    - `password`

```sh
# コンテナ名を確認
docker-compose ps

# bash というシェルで docker-lamp_mysql_1 コンテナにログインする
docker exec -it docker-lamp_mysql_1 bash

# MySQL バージョン確認
mysql --version

# MySQL に root ユーザでログイン -> パスワード入力
mysql -u root -p

# パスワードも一緒に入力する場合
# mysql -u root -ppassword
```

### phpMyAdmin

ブラウザから GUI で MySQL 操作できる phpMyAdmin をサーバ配置している
MySQL のログイン情報でアクセス可能

- ユーザ
    - `root`
- パスワード
    - `password`

## PHP / Apache

```sh
# コンテナ名を確認
docker-compose ps

# bash というシェルで docker-lamp_php-apache_1 コンテナにログインする

docker exec -it docker-lamp_php-apache_1 bash

# PHP のバージョン確認
php -v

# Apache のバージョン確認
apache2ctl -v
```

`/var/www/html` (ドキュメントルート) にファイルを配置すると、Apache がファイル展開してくれる
