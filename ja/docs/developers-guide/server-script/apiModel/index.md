---
title: apiModel
icon: material/alpha-o-box
category: サーバスクリプト
order: '20000'
status: ''
parts: ''
urlstring: server-script-api-model
translationKey: server-script-api-model
shortname: apiModel
created: 2021-01-22
updated: 2025-04-17
---

## 概要

[サーバスクリプト](../index.md)で「レコード」の内容の読み取りおよび新規作成、更新、削除を行うためのオブジェクトです。

## プロパティ

プロパティについては[model](../model/index.md)のプロパティを参照してください。

## メソッド

|メソッド名|概要|
|:---|:----|
|[Create](server-script-api-model-create.md)|レコードの新規作成|
|[Update](server-script-api-model-update.md)|レコードの更新|
|[Delete](server-script-api-model-delete.md)|レコードの削除|

## 使用例

下記の例では、レコードIDが 123 のレコード情報を取得し、[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を 完了(900) に更新します。

##### JavaScript

```
let records = items.Get(123);
if (records.Length === 1) {
    let record = records[0];
    record.Status = 900;
    record.Update();
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：model](../model/index.md)
-   [開発者ガイド：サーバスクリプト：apiModel.Create](server-script-api-model-create.md)
-   [開発者ガイド：サーバスクリプト：apiModel.Update](server-script-api-model-update.md)
-   [開発者ガイド：サーバスクリプト：apiModel.Delete](server-script-api-model-delete.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)