
# 初期設定

## リモートリポジトリを変更する

このリポジトリは `git clone git@github.com:Takuma-Ikeda/docker-LAMP.git` で使うことができますが、
そのままだとリモートリポジトリ `origin` は上記 SSH を指したままになってしまいます。

`git clone` したあと、自分の新しい GitHub リポジトリでプロジェクトを管理したい場合...

1. 名前がややこしいのでプロジェクトのフォルダ名を `docker-LAMP` から変更する
    - たとえば `lamp-lessons` などに変更する
1. GitHub に新しいリポジトリを作成する
    - たとえば `lamp-lessons` で新しいリポジトリを作成する
1. 以下コマンドを実行する

 ```sh
# 現在のリモートリポジトリを確認する ※ git@github.com:Takuma-Ikeda/docker-LAMP.git のはず
git remote -v

# リモートリポジトリ origin に新しいリポジトリの SSH を設定する
git remote set-url origin {new url}

git add .
git commit -m 'first commit'

# -u オプション: 今後の git push は今の origin をデフォルトとする
git push -u origin master
```

# このリポジトリについて

## Docker LAMP 環境

LAMP とは「Linux, Apache, MySQL, PHP」を組み合わせた開発環境のことです。
Docker というアプリで簡単に LAMP 開発環境を構築しようと思います。

今回は「MySQL」「phpMyAdmin」「Apache / PHP」という 3 つの Docker コンテナを作成します。

- MySQL
    - v5.7.31
    - Debian
- phpMyAdmin
    - Debian
- Apache / PHP (同環境)
    - Apache
        - v2.4.38
    - PHP
        - v7.4.10
    - Debian

## Docker コンテナ起動方法

`docker-compose.yml` のあるディレクトリで以下コマンドを実行します。

```sh
# Docker コンテナ起動
docker-compose up -d

# Docker コンテナ終了
docker-compose down
```

### ブラウザ URL アクセス方法

- PHP ファイルアクセス ※ 80 番ポート ( 80 番ポートは省略することもできる)
    - `index.html` にアクセス
        - http://localhost/index.html:80 または http://localhost/index.html または http://localhost または localhost
    - `index.php` にアクセス
        - http://localhost/index.php:80 または http://localhost/index.php または http://localhost または localhost
    - `phpinfo.php` にアクセス
        - http://localhost/phpinfo.php
- phpMyAdmin ※ 8080 番ポート
    - http://localhost:8080/

## Docker コンテナにログインする方法

### MySQL

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

#### phpMyAdmin

ブラウザから GUI で MySQL 操作できる phpMyAdmin をサーバに配置しました。
MySQL の初期ログイン情報でアクセス可能です。

- ユーザ
    - `root`
- パスワード
    - `password`

### PHP / Apache

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

コンテナ内の `/var/www/html` (ドキュメントルート) に html や php ファイルを配置すると、
Apache がファイルを配信してくれるので Google Chrome でアクセスできるようになります。
