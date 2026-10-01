---
title: API
category: API
order: '1'
status: ''
parts: ''
urlstring: api
translationKey: api
shortname: API
created: 2021-06-12
updated: 2023-08-16
---

## 概要

「API」を使用して他システムとデータの入出力を行うことが可能です。

## 目次

=== "基礎知識"

    <div class="grid cards" markdown>

    - [API](api.md)
    - [APIのURL](api-url.md)
    - [APIキーの作成](api-key.md)

    </div>

=== "テーブル操作"

    <div class="grid cards" markdown>

    - [レコード作成](../table-operations/api-record-create.md)
    - [レコード一括作成・更新](../table-operations/api-record-bulkupsert.md)
    - [レコード作成・更新](../table-operations/api-record-upsert.md)
    - [レコード削除](../table-operations/api-record-delete.md)
    - [レコード一括削除](../table-operations/api-table-bulk-delete.md)
    - [単一レコード取得](../table-operations/api-record-get.md)
    - [複数レコード取得](../table-operations/api-record-get-multi.md)
    - [添付ファイル取得](../table-operations/api-attachment-get.md)
    - [レコード更新](../table-operations/api-record-update.md)
    - [レコードのインポート](../table-operations/api-import.md)
    - [テーブルのエクスポート](../table-operations/api-export.md)

    </div>

=== "サイト操作"

    <div class="grid cards" markdown>

    - [サイトコピー](../site-operations/api-site-copy.md)
    - [サイト作成](../site-operations/api-site-create.md)
    - [サイト削除](../site-operations/api-site-delete.md)
    - [サイト取得](../site-operations/api-site-get.md)
    - [サイト名検索で該当サイトに最も近いサイトID取得](../site-operations/api-site-get-closest-siteid.md)
    - [サイト更新](../site-operations/api-site-update.md)
    - [サイト設定の更新（部分追加/更新/削除）](../site-operations/api-update-sitesettings.md)
    - [サマリ同期](../site-operations/api-synchronize-summaries.md)
    - [検索インデックス再構築](../site-operations/api-rebuild-search-indexes.md)

    </div>

=== "ユーザ操作"

    <div class="grid cards" markdown>

    - [インポート](../user-operations/api-user-import.md)
    - [ユーザ作成](../user-operations/api-user-create.md)
    - [ユーザ削除](../user-operations/api-user-delete.md)
    - [ユーザ取得（全て）](../user-operations/api-user-get-all.md)
    - [ユーザ取得（選択）](../user-operations/api-user-get.md)
    - [ユーザ更新](../user-operations/api-user-update.md)

    </div>

=== "組織操作"

    <div class="grid cards" markdown>

    - [組織作成](../department-operations/api-dept-create.md)
    - [組織削除](../department-operations/api-dept-delete.md)
    - [組織取得](../department-operations/api-dept-get.md)
    - [組織更新](../department-operations/api-dept-update.md)

    </div>

=== "グループ操作"

    <div class="grid cards" markdown>

    - [インポート](../group-operations/api-group-import.md)
    - [グループ作成](../group-operations/api-group-create.md)
    - [グループ削除](../group-operations/api-group-delete.md)
    - [グループ取得](../group-operations/api-group-get.md)
    - [グループ更新](../group-operations/api-group-update.md)

    </div>

=== "メール"

    <div class="grid cards" markdown>

    - [メール送信](../mail/index.md)

    </div>

## 前提条件

1. 「API」を使用するためには[APIキー](api-key.md)を作成する必要があります。ログインしているブラウザのセッションからアクセスする場合には[APIキー](api-key.md)を指定せずに使用可能です。
1. [Api.json](../../../setup/parameters/api-json.md)の Enabled パラメータが true に設定されている必要があります。

## 関連情報

-   [開発者ガイド：API：APIキーの作成](api-key.md)
-   [パラメータ設定：Api.json](../../../setup/parameters/api-json.md)