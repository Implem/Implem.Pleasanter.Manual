---
title: $p.selectedIds
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-selected-ids
translationKey: script-selected-ids
shortname: $p.selectedIds
created: 2021-11-09
updated: 2025-08-13
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)でチェックを入れた対象レコードのIDの配列を取得するメソッドに関する説明です。

## 構文

##### JavaScript

```
$p.selectedIds();
``` 

## 使用例

1. テーブルの管理画面のスクリプトタブより出力先を[一覧](../../../managers-guide/manage-table/grid/index.md)として以下を設定します。

##### JavaScript

```
$p.events.before_send_OpenExportSelectorDialogCommand = function (args) {
    console.log($p.selectedIds());
}
``` 

2. 一覧画面で任意のレコードにチェックを入れます。
3. エクスポートボタンを押下します。

##### 結果

一覧画面でチェックを入れた対象レコードのIDの配列が取得されます。

```text
[
    11111,
    33333,
    55555
]
``` 

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.14.0 以降|機能追加|

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：一覧画面](../../../managers-guide/manage-table/grid/index.md)