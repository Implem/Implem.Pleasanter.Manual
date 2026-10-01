---
title: サーバスクリプト
category: サーバスクリプト
order: '100'
status: ''
parts: ''
urlstring: server-script
translationKey: developers-guide/server-script
shortname: サーバスクリプト
created: 2021-05-22
updated: 2026-05-12
---

## 概要

「サーバスクリプト」を使用するとサーバサイドでJavaScriptを実行し、条件分岐、計算、文字列処理、レコードの操作、メールやチャットへの通知、動的なアクセス制御等を行うことが可能です。JavaScriptの実行エンジンはMicrosoft社の[ClearScript](https://github.com/microsoft/ClearScript)を使用しています。

本カテゴリは以下の内容を含みます。

<div class="grid cards" markdown>

-   [基本](basics/index.md)
-   [context](context/index.md)
-   [logs](logs/index.md)
-   [siteSettings](siteSettings/index.md)
-   [view](view/index.md)
-   [grid](grid/index.md)
-   [columns](columns/index.md)
-   [elements](elements/index.md)
-   [utilities](utilities/index.md)
-   [model](model/index.md)
-   [saved](saved/index.md)
-   [items](items/index.md)
-   [apiModel](apiModel/index.md)
-   [users](users/index.md)
-   [user](user/index.md)
-   [depts](depts/index.md)
-   [dept](dept/index.md)
-   [group](group/index.md)
-   [groups](groups/index.md)
-   [notifications](notifications/index.md)
-   [notification](notification/index.md)
-   [hidden](hidden/index.md)
-   [httpClient](httpClient/index.md)
-   [$ps.CSV](ps-csv/index.md)
-   [$ps.file](ps-file/index.md)
-   [$ps.JSON](ps-json/index.md)
-   [extendedSql](extended-sql/index.md)
-   [$p.JSON](p-json/index.md)
-   [responses.Reload](responses-reload/index.md)
-   [サーバスクリプトによるファイルエクスポートサンプル](server-script-file-export.md)
-   [サーバスクリプトによるファイルインポートサンプル](server-script-file-import.md)

</div>

!!! tip "左ナビゲーションのアイコン"
    左のナビゲーションでは、ページの種別をアイコンで示しています。

    |    アイコン    | 種別         | 内容                           |
    | :------------: | :----------- | :----------------------------- |
    | :material-alpha-o-box: | オブジェクト | 本カテゴリのオブジェクト       |
    | :material-alpha-m-box: | メソッド     | オブジェクトが持つメソッド     |
    | :material-alpha-p-box: | プロパティ   | オブジェクトが持つプロパティ   |

    種別を判別できないページには、アイコンを付けていません。

## 制限事項

1.  外部のスクリプトを読み込む事はできません。
1.  ローカルディスク等、ローカルリソースにアクセスすることはできません。
1.  サーバスクリプト内のDateTimeの値はUTCに変換されます。

## サーバスクリプトの権限に関する注意事項

1.  サーバスクリプトはログインユーザの権限で実行されます。実行にあたり特定のユーザやシステム管理者の権限が必要な場合、そのユーザの[APIキーの作成](../api/basics/api-key.md)を指定する必要があります。

## スクリプトとサーバスクリプトの違い

[スクリプト](../script/index.md)はブラウザ上で動作するJavaScriptを記述することで画面上のデータの加工を行えますが、[API](../api/basics/api.md)によるデータ更新や[レコードのインポート](../../users-guide/table/record-authoring/create-records/table-record-import.md)を行う際のデータの加工が行えません。「サーバスクリプト」ではサーバ上のレコードのモデルに対してJavaScriptによる入出力が行えるため、[API](../api/basics/api.md)や[レコードのインポート](../../users-guide/table/record-authoring/create-records/table-record-import.md)を行う際にもデータの加工などが行えます。

## 部品化機能

「サーバスクリプト」は、共通コードを部品化する[コードの共有](./basics/server-script-shared.md)機能や、[開発者ガイド：拡張機能：拡張サーバスクリプト](../extended-features/extended-server-script.md)のインクルード機能を備えています。

## デバッグ

Visual Studio Codeを使用して「サーバスクリプト」の[デバッグ](./basics/server-script-debug.md)を行うことができます。

## 操作手順

[サーバスクリプト](../../managers-guide/manage-table/server-script/index.md)を参照してください。

## 関連情報

-   [ClearScript](https://github.com/microsoft/ClearScript)
-   [APIキーの作成](../api/basics/api-key.md)
-   [API](../api/basics/api.md)
-   [レコードのインポート](../../users-guide/table/record-authoring/create-records/table-record-import.md)
-   [コードの共有](./basics/server-script-shared.md)
-   [開発者ガイド：拡張機能：拡張サーバスクリプト](../extended-features/extended-server-script.md)
-   [デバッグ](./basics/server-script-debug.md)
-   [サーバスクリプト](../../managers-guide/manage-table/server-script/index.md)
