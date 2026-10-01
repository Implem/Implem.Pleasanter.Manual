---
title: grid
icon: material/alpha-o-box
category: サーバスクリプト
order: '5000'
status: ''
parts: ''
urlstring: server-script-grid
translationKey: server-script-grid
shortname: server-script-grid
created: 2022-07-19
updated: 2025-01-30
---

## 概要

[サーバスクリプト](../index.md)で一覧表示の情報を取得します。

## 制限事項

1. 「画面表示の前」の[条件](../../../FAQ/editor/faq-condition-mode-range.md)のみ使用できます。

## プロパティ

|No|Name|Get|Set|Type|Description|
|:----|:----|:----|:----|:----|:----|
|1|TotalCount|○|-|int|一覧のレコード総数|

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|[SelectedIds](server-script-grid-selected-ids.md)|[サーバスクリプト](../index.md)で一覧画面上の選択しているレコードのIDを取得します。|

## 使用例

以下の例ではレコード総数をブラウザのコンソールに出力します。

##### JavaScript

``` javascript
context.Log('レコード総数=' + grid.TotalCount);
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.13.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [SelectedIds](server-script-grid-selected-ids.md)
