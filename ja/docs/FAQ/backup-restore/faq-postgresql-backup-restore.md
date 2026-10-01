---
title: PostgreSQL データベース バックアップ・リストア手順
category: FAQ：バックアップ、リストア
order: '300'
status: ''
parts: ''
urlstring: faq-postgresql-backup-restore
translationKey: faq-postgresql-backup-restore
shortname: ''
created: 2020-06-10
updated: 2023-12-20
---

本手順はユーザマニュアルのインストール手順で構築したプリザンターのデータベース（Implem.Pleasanter）を対象としております。

## 同じ環境へリストアを行う場合

バックアップを取得した環境と同じ環境にリストアを行う場合は以下の通りです。

### バックアップ

バックアップファイルを取得します。この手順では /backup ディレクトリ配下に取得します。

``` bash
su - postgres
pg_dump -Fc Implem.Pleasanter > /backup/Implem.Pleasanter.dump
```

### リストア

上記のコマンドでバックアップを取得したうえで、SQLでデータベース（Implem.Pleasanter）を削除、再作成を行い、pg_restoreコマンドでリストアを行います。

``` bash
psql -U postgres -c 'drop database "Implem.Pleasanter";'
psql -U postgres -c 'create database "Implem.Pleasanter";'
pg_restore -d Implem.Pleasanter /backup/Implem.Pleasanter.dump
```

## 異なる環境へリストアを行う場合

バックアップを取得した環境（移行元）とは異なる環境（移行先）でリストアを行う場合は以下の通りです。

### バックアップ

移行元でロールとデータベースのバックアップを取得します。※データベースを復元する際にロール情報が必要となるため、ロールのバックアップも取得します。

``` bash
pg_dumpall --roles-only > /backup/Implem.Pleasanter_role.dump
pg_dump -Fc Implem.Pleasanter > /backup/Implem.Pleasanter.dump
```

### リストア

移行先に上記のバックアップで取得した2つのバックアップファイルをコピーして、各ファイルを用いてリストアを行います。下記の手順ではバックアップファイルを /backup ディレクトリにコピーしていることを前提としております。

#### データベースの作成

下記コマンドでデータベースの作成および、全文検索用モジュール（pg_trgm）を追加します。

``` bash
psql -U postgres -c 'create database "Implem.Pleasanter";'
psql -U postgres -c 'create extension if not exists pg_trgm;'
```

#### データベースのリストア

下記コマンドで、ロールおよびデータベースを復元します。

``` bash
psql -f /backup/Implem.Pleasanter_role.dump
pg_restore -d Implem.Pleasanter /backup/Implem.Pleasanter.dump
```

!!! info
    下記コマンドの実行前にCodeDefiner実行によるデータベースの構成は不要です。

## 定期的にバックアップ

定期的にバックアップおよびバックアップファイルの削除を行いたい場合は、下記のようにcronを設定してください。

### 毎日2:00にデータベースのバックアップを取得

``` cron
00 02 * * * /bin/pg_dump -Fc "Implem.Pleasanter" > /backup/`date "+%Y%m%d"`_Implem.Pleasanter.dump
```

### 毎日1:00に一週間以上前のファイルを削除

``` cron
00 01 * * * /bin/find /backup -maxdepth 1 -mtime +7 -type f -delete
```

### 実行コマンド

``` bash
sudo crontab -u postgres -e
```
