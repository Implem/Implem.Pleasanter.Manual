---
title: PostgreSQLが14以前のバージョンで、1.3.43.0以前のプリザンターをLinuxの環境へ導入したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-postgresql-14-install-pleasanter-for-linux
translationKey: faq-postgresql-14-install-pleasanter-for-linux
shortname: ''
created: 2023-07-25
updated: 2026-03-22
---

## 回答

PostgreSQLのデータベース作成および、全文検索用モジュール(pg_trgm)のインストールを手動で行ってください。

---

## 概要

PostgreSQLが14以前のバージョンで、1.3.43.0以前のプリザンターをLinuxの環境へ導入したい場合の手順です。

## 操作手順

基本的な導入手順については下記マニュアルに記載の内容で行います。

-   [プリザンターをUbuntuにインストールする | Pleasanter](../../setup/installation/install-manually/getting-started-pleasanter-ubuntu.md)
-   [プリザンターをRed Hat Enterprise Linuxにインストールする | Pleasanter](../../setup/installation/install-manually/getting-started-pleasanter-rhel.md)
-   [プリザンターをAlmaLinuxにインストールする | Pleasanter](../../setup/installation/install-manually/getting-started-pleasanter-almalinux.md)

バージョン1.3.43.0以前のプリザンターをインストールする場合、PostgreSQLのデータベース作成および、全文検索用モジュール（pg_trgm）のインストールを手動で行う必要があります。PostgreSQLのインストール後、以下の手順に沿ってデータベース作成、全文検索用モジュールのインストールを行い、上記マニュアルに記載の後続の手順を実施してください。

### PostgreSQLユーザの設定

PostgreSQL管理用のユーザ"postgres"（OSのユーザ）にパスワードを設定します。

``` bash
sudo passwd postgres
```

``` bash
sudo su - postgres
psql -U postgres
```

PostgreSQLの管理ユーザ"postgres"のパスワードを設定

``` sql
postgres=# alter role postgres with password '<新しいパスワード>';
```

### プリザンター用のデータベース作成

データベース"Implem.Pleasanter"を作成します。

``` sql
postgres=# create database "Implem.Pleasanter";
```

以下のコマンドで作成したDBの確認を行います。

``` sql
postgres=# \l
```

### 全文検索用モジュール（pg_trgm）のインストール

テキストの全⽂検索に必要なモジュール（pg_trgm）をインストールします。

``` sql
postgres=# \c "Implem.Pleasanter"
Implem.Pleasanter=# create extension pg_trgm;
```
