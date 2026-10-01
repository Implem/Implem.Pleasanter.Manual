---
title: PostgreSQLフルテキストインデックスを生成する
category: 追加設定：DBサーバ
order: '200'
status: ''
parts: ''
urlstring: postgre-create-fulltext-index
translationKey: postgre-create-fulltext-index
shortname: ''
created: 2024-07-01
updated: 2024-12-19
---

## 概要

PostgreSQL環境においてフルテキストインデックスを手動生成する手順を説明します。

フルテキストインデックスは、[共通機能：横断検索](../../../users-guide/common/crosssearch.md)や[テーブルの管理：検索：検索の設定：検索の種類](../../../managers-guide/manage-table/search/table-management-search-type.md)で「フルテキスト」を選択した場合のフリーテキスト検索のパフォーマンスを向上させます。

本手順が必要かどうかは、**初期構築時のバージョン**によって異なります。以下の早見表で利用環境を確認してください。

| DB         | 初期構築時バージョン | 作業の<br>必要性 | 本手順を実施しなかった場合の影響                                                                                     | 備考                                                                                                  |
| ---------- | -------------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| SQL Server | すべてのバージョン   | 不要             | ―                                                                                                                   | ―                                                                                                     |
| PostgreSQL | 1.4.6.0以前          | **必要**         | 横断検索や検索の種類で「フルテキスト」を選択した場合のフリーテキスト検索において、検索結果の表示に時間がかかります。 | 初期構築後にバージョンアップしていても、初期構築時のバージョンが1.4.6.0以前であれば本手順が必要です。 |
| PostgreSQL | 1.4.7.0以降          | 不要             | ―                                                                                                                   | インストール時点でフルテキストインデックスが自動生成されます。                                        |
| MySQL      | すべてのバージョン   | 不要             | ―                                                                                                                   | ―                                                                                                     |

## 注意事項

- プリザンターの構成やデータの件数によって、フルテキストインデックスを生成するSQLの実行に時間がかかる場合があります。
- 検索パフォーマンスを更に向上させたい場合は、サーバの性能向上も検討してください。

## 前提条件

- データベースにPostgreSQLを使用していること。
- 初期構築時のバージョンが1.4.6.0以前であること（現在のバージョンは問いません）。

## 設定手順

1.  プリザンターのデータベースに接続し、下記のSQLを実行してください。

    ``` sql linenums="1"
    select *
    from   pg_indexes
    where  tablename = 'Items'
        and indexdef like '%FullText%'; 
    ```

    検索結果が1件以上表示される場合、既にフルテキストカラムに対するインデックスが生成されているため、以降の手順は不要です。

1.  プリザンターが導入されているサーバへログインし、 プリザンターを停止してください。
1.  プリザンターのデータベースに「Implem.Pleasanter_Owner」でログインして接続しください。以下はPostgreSQLに付属するpsqlで接続した一例です。

    ``` cmd
    # psql -U Implem.Pleasanter_Owner -d Implem.Pleasanter -p 5432
    ```

1.  下記のSQLを実行して、フルテキストインデックスを生成します。

    ``` sql linenums="1"
    create index "ftx" on "Items" using gin ("FullText" gin_trgm_ops);
    ```

1.  下記のSQL（上記1.と同じ）を実行して、フルテキストインデックスが生成されていることを確認してください。

    ```sql linenums="1"
    select *
    from    pg_indexes
    where   tablename = 'Items'
        and indexdef like '%FullText%';
    ```

    下図の通り検索結果が表示されている場合、フルテキストインデックスが生成されています。

    ![pg_indexesの検索結果。フルテキストインデックスが表示されている](https://pleasanter.org/files/images/ja/setup/additional/db-server/assets/d9aa188fabec46afaa592fee697174f9.png)

1. プリザンターを開始してください。PostgreSQLの再起動は不要です。

## 関連情報

-   [共通機能：横断検索](../../../users-guide/common/crosssearch.md)
-   [テーブルの管理：検索：検索の設定：検索の種類](../../../managers-guide/manage-table/search/table-management-search-type.md)
