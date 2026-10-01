---
title: PostgreSQL データベース バックアップ・リストア手順(Docker利用)
category: FAQ：バックアップ、リストア
order: '300'
status: ''
parts: ''
urlstring: faq-postgresql-backup-restore-docker
translationKey: faq-postgresql-backup-restore-docker
shortname: ''
created: 2025-05-08
updated: 2026-07-17
---

## 前提条件

1.  本手順はユーザマニュアルのインストール手順でDockerに構築したプリザンターのデータベース(Implem.Pleasanter)を対象としています。
1.  Linuxに直接インストールしたPostgreSQLのデータベース バックアップ・リストア手順は[FAQ：PostgreSQL データベース バックアップ・リストア手順](faq-postgresql-backup-restore.md)を参照してください。

## 概要

バックアップを取得した環境と同じ環境にリストアを行う場合は以下の通りです。本手順では、ダンプファイルをコンテナ外でも保存・利用できるように、ホスト側のフォルダにもダンプファイルを出力します。

## 操作手順

1.  バックアップ
1.  リストア

### 1. バックアップ

1.  以下コマンドを実行し、DBのコンテナを停止します。

    ``` bash
    docker compose stop db
    ```

1.  compose.yamlにバックアップファイルを出力するフォルダおよびボリュームの情報を追記します。この手順では /backup ディレクトリ配下に取得します。

    ``` yaml title="compose.yaml"
    services:
    db:
        volumes:
        - ./backup:/backup  # この記述を追記する。
    ```

1.  バックアップファイルを取得するホスト側のフォルダを作成します。

    ![ホスト側に作成したバックアップ用フォルダ](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/690731496b004e26b43149e5148ede1c.png)

1.  以下コマンドを実行し、ボリュームに/backupディレクトリを追加して再作成・再起動します。

    ``` bash
    docker compose up -d db
    ```

1.  以下コマンドを実行し、DBのコンテナ内に入ります。

    ``` bash
    docker compose exec -u postgres db bash
    ```

1.  コマンドを実行しバックアップファイルを取得します。

    ``` bash
    pg_dump -Fc Implem.Pleasanter > /backup/Implem.Pleasanter.dump
    ```

1.  以下コマンドを実行し、コンテナのディレクトリにバックアップファイルが作成されたことを確認します。

    ``` bash
    ls -la /backup/Implem.Pleasanter.dump
    ```

    ``` bash title="実行結果例"
    -rw-r--r-- 1 postgres postgres 648849 May 08 06:25 /backup/Implem.Pleasanter.dump
    ```

1.  ホストのフォルダにバックアップファイルが作成されたことを確認します。

    ![ホスト側のフォルダにダンプファイルが出力されている状態](https://pleasanter.org/files/images/ja/FAQ/backup-restore/assets/cf2fd4da29aa434a8b3253e7a1b76a4d.png)

1.  DBのコンテナから退出します。

    ``` bash
    exit
    ```

### 2. リストア

1.  以下コマンドを実行し、プリザンターのコンテナのみ停止します。

    ``` bash
    docker compose stop pleasanter
    ```

1.  以下コマンドを実行し、DBのコンテナ内に入ります。

    ``` bash
    docker compose exec -u postgres db bash
    ```

1.  リストア後切り戻せるように、上記バックアップ手順と同様のコマンドでバックアップを取得します。

    ``` bash
    pg_dump -Fc Implem.Pleasanter > 【リストア前に取得するバックアップファイルの出力先パス/ファイル名】
    ```

1.  SQLでデータベース（Implem.Pleasanter）を削除、再作成を行います。

    ``` bash
    psql -U postgres -c 'drop database "Implem.Pleasanter";'
    psql -U postgres -c 'create database "Implem.Pleasanter";'
    ```

1.  リストアのコマンドを実行します。この手順では /backup ディレクトリ配下のバックアップファイルでデータベースを復元します。

    ``` bash
    pg_restore -d Implem.Pleasanter /backup/Implem.Pleasanter.dump
    ```

1.  DBのコンテナから退出します。

    ``` bash
    exit
    ```

1.  プリザンターのコンテナを再起動します。

    ``` bash
    docker compose start pleasanter
    ```
