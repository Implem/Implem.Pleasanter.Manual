---
title: .NET Core版で横断検索時にエラーが発生する
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-postgresql-pg-trgm-not-installed
translationKey: faq-postgresql-pg-trgm-not-installed
shortname: ''
created: 2020-06-08
updated: 2025-05-08
---

-   本FAQは.NET Core版かつPostgreSQL 12環境のプリザンターの運用を継続し、かつ、横断検索時にエラーが発生する場合のみ参照してください。
-   PostgreSQL 12は製品サポートが終了したデータベースであるため、postgresql12-contribのインストールは推奨しません。
-   現在の（.NET Core版と.NET Framework版の区分がなくなった）プリザンターはインストール時に横断検索が有効になるように問題が解消されているため、本FAQの参照は不要です。

## 回答

拡張モジュールpostgresql12-contribをインストールしてください。

---

## 概要

プリザンターの画面右上にある横断検索を実行した際に、下記のエラーが表示されて正しく実行されない場合、拡張モジュールを正しくインストールする必要があります

``` text
アプリケーションで問題が発生しました。
```

以下の手順に沿って実行してください。

## 操作手順

1.  拡張モジュールpostgresql12-contribをインストールします。

    ``` bash
    sudo yum -y install postgresql12-contrib
    ```

1.  データベース"Implem.Pleasanter"に接続し、下記SQLを実行します。

    ``` sql
    CREATE EXTENSION pg_trgm;
    ```
