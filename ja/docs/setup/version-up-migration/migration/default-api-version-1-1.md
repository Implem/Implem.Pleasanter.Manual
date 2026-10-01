---
title: 既定のAPIバージョン1.1への変更および旧バージョンとの互換性について
category: 移行
order: '0'
status: ''
parts: ''
urlstring: default-api-version-1-1
translationKey: default-api-version-1-1
shortname: 既定のAPIバージョン
created: 2022-07-02
updated: 2024-12-19
---

## 概要

バージョン1.3.13.0において、既定のAPIバージョンが1.0から1.1に変更となり、APIのリクエストおよびレスポンスのデータレイアウトが変更になります。また、バージョン1.3.12.0以前のバージョンに存在した不具合（APIキーを指定しないリクエストでApiVersionが正しくセットされない問題）が解消されることによって同様の変更が発生いたします。旧バージョンで開発したAPI呼び出しの互換性を維持するため、パラメータの調整が必要となります。

## APIバージョン1.0から1.1の変更点

APIリクエストとAPIレスポンスのデータレイアウトが、以下のように変更となります。

### APIバージョン1.0

以下の項目のデータレイアウトがフラットに表現されていました。

-   [分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)

上記項目のレスポンスが、例えば分類項目の場合、ClassA～Class100までとなっていました。Class101以降のレスポンスを取得したい場合は、APIバージョン1.1を利用してください。

```json linenums="1" hl_lines="4-8"
{
    "ApiVersion": 1.0,
    "Title": "API 1.0",
    "ClassA": "ClassA",
    "NumA": 123,
    "DateA": "2022/7/2",
    "DescriptionA": "DescriptionA",
    "CheckA": true
}
```

### APIバージョン1.1

以下の項目のデータレイアウトが、キー・バリュー形式に変更となります。

-   [分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)

```json linenums="1" hl_lines="4-18"
{
    "ApiVersion": 1.1,
    "Title": "API 1.1",
    "ClassHash": {
        "ClassA": "ClassA"
    },
    "NumHash": {
        "NumA": 123
    },
    "DateHash": {
        "DateA": "2022/7/2"
    },
    "DescriptionHash": {
        "DescriptionA": "DescriptionA"
    },
    "CheckHash": {
        "CheckA": true
    }
}
```

## APIバージョンの指定方法

APIバージョンの既定値は[Api.json](../../parameters/api-json.md)のVersionパラメータで設定できます。また、APIのリクエストパラメータで明示的に指定できます。

### Api.jsonのVersionパラメータで指定する

APIバージョンを指定しないAPI呼び出しで使用されるバージョンです。既定値は1.1です。旧バージョンの仕様に変更する場合には、1.0に変更してください。

### リクエストパラメータで指定する

API実行時のリクエストパラメータ`ApiVersion`でAPIバージョンを指定できます。リクエストパラメータを未指定の場合は、API.jsonのVersionパラメータの値が使用されます。旧バージョンの仕様に変更する場合は、1.0を指定してください。

#### [レコード取得API](../../../developers-guide/api/table-operations/api-record-get-multi.md)のリクエスト

``` json linenums="1" hl_lines="2"
{
     "ApiVersion": 1.0,
     "ApiKey": "63Kfk0ds3d4S2DBsa32..."
}
```

#### [$p.apiGet](../../../developers-guide/script/script-api/script-api-get.md)のリクエスト

``` json linenums="1" hl_lines="4"
$p.apiGet({
    id: <サイトID>,
    data: {
        "ApiVersion": 1.0,
        <その他の取得条件>
    },
    done: <任意の処理>,
    fail: <任意の処理>,
    always: <任意の処理>
});
```

## Api.jsonのCompatibility_1_3_12パラメータ

`Compatibility_1_3_12`は、バージョン1.3.12.0以前に存在した不具合[^1]に該当するAPI呼び出しが存在する場合に、互換性を維持するためのパラメータです。既定値は`false`です。

-   該当のAPI呼び出しを使用している場合は、`Compatibility_1_3_12`パラメータを`true`に変更し[Api.json](../../parameters/api-json.md)の`Version`パラメータを1.0に変更してください。
-   .NET Framework版ではこの不具合は発生していません。.NET Framework版からの移行では、`Compatibility_1_3_12`パラメータを`false`に設定してください。

[^1]: APIキーを指定しないリクエストでApiVersionが正しくセットされない問題。

### 該当するAPI呼び出し

バージョン1.3.12.0以前では、`ApiVersion`を指定しているが、`ApiKey`を指定していないケースにおいて、`"ApiVersion": 1.1`の指定が無視され1.0で動作する不具合が存在しました。

バージョン1.3.13.0以降ではこの不具合が解消されるため、APIバージョン1.1の挙動に変更となります。

``` json title="ApiVersionを指定しているが、ApiKeyを指定していないケース"
{
    "ApiVersion": 1.1
    "Title": "1.0"
}
```

### `"Compatibility_1_3_12": false`の挙動

不具合が解消され、指定したAPIバージョンで動作します。

| ApiVersion |  ApiKey  |       挙動        |
| :--------: | :------: | :---------------: |
|  指定なし  |          | Api.jsonのVersion |
|    1.0     | 指定あり |        1.0        |
|    1.0     | 指定なし |        1.0        |
|    1.1     | 指定あり |        1.1        |
|    1.1     | 指定なし |      **1.1**      |

### `"Compatibility_1_3_12": true`の挙動

1.3.12.0 以前のバージョンと同様に ApiVersion の指定が無視されます。

| ApiVersion |  ApiKey  |         挙動          |
| :--------: | :------: | :-------------------: |
|  指定なし  |          |   Api.jsonのVersion   |
|    1.0     | 指定あり |          1.0          |
|    1.0     | 指定なし |          1.0          |
|    1.1     | 指定あり |          1.1          |
|    1.1     | 指定なし | **Api.jsonのVersion** |

## 関連情報

-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [パラメータ設定：Api.json](../../parameters/api-json.md)
-   [開発者ガイド：API：テーブル操作：複数レコード取得](../../../developers-guide/api/table-operations/api-record-get-multi.md)
-   [$p.apiGet](../../../developers-guide/script/script-api/script-api-get.md)
