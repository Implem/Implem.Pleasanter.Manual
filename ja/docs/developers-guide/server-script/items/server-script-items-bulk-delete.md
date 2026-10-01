---
title: items.BulkDelete
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-bulk-delete
translationKey: server-script-items-bulk-delete
shortname: items.BulkDelete
created: 2021-01-27
updated: 2025-09-01
---

## 概要

指定したサイトのレコードを一括削除します。選択条件を指定して削除対象のレコードを絞り込むことができます。

## 構文

```
items.BulkDelete(siteId, data)
```

## パラメータ

| パラメータ | 型     | 必須 | 概要                                                                                                                                                       |
| :--------- | :----- | :--: | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| siteId     | long   |  ○   | 対象テーブルのサイトIDを指定。                                                                                                                             |
| data       | string |  ○   | 一括削除するレコードの条件等をJSON形式で指定。JSONの仕様は [レコード一括削除API](../../api/table-operations/api-table-bulk-delete.md) の「設定値」を参照。 |

## 戻り値

一括削除したレコード数を返却します。削除できなかった場合は0を返却します。

## 使用例 1

以下の例では、サイトID 123 のテーブルにある Status(状況) が 900(完了) のレコードを削除します。

##### JavaScript

```
let data = {
    View: {
        ColumnFilterHash: {
            Status: "[900]"
        }
    }
};
items.BulkDelete(123, JSON.stringify(data));
```

## 使用例 2

以下の例では、サイトID 123 のテーブルにある レコードIDが 1000,1003,1400のレコードを削除します。

##### JavaScript

```
let data = {
    Selected: [1000,1003,1400]
};
items.BulkDelete(123, JSON.stringify(data));
```

## 使用例 3

以下の例では、サイトID 123 のテーブルにある全レコードを削除します。

##### JavaScript

```
let data = {
    All: true
};
items.BulkDelete(123, JSON.stringify(data));
```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)
