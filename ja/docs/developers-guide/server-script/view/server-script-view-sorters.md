---
title: view.Sorters
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-sorters
translationKey: server-script-view-sorters
shortname: view.Sorters
created: 2021-01-22
updated: 2023-08-25
---

## 概要

[view](index.md)オブジェクトの「Sorters」です。[サーバスクリプト](../index.md)で「レコード」の[ソート](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)を行うことができます。[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)が使用できます。

## プロパティ

|No|プロパティ名|変更|説明|
|:--|:--|:--|:--|
|1|`[カラム名]`|○|[ソート](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)をかける[カラム名](../../dev-column-name.md)を指定し `"asc"` / `"desc"` / `"release"` を設定。|

## 使用例

以下の例では、NumA（数値A）の値を降順でレコード表示します。

``` javascript
view.Sorters.NumA = 'desc';

```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)
-   [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)
