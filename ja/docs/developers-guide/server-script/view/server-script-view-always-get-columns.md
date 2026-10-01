---
title: view.AlwaysGetColumns
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-always-get-columns
translationKey: server-script-view-always-get-columns
shortname: view.AlwaysGetColumns
created: 2021-10-18
updated: 2025-01-30
---

## 概要

[view](index.md)オブジェクトの「AlwaysGetColumns」です。[サーバスクリプト](../index.md)で「modelオブジェクト」を使用する際に、画面上に無い[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を取得する際に使用します。

## メソッド

|No|Name|Description|
|:---|:---|:---|
|1|Add|読み込む[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の[カラム名](../../dev-column-name.md)を指定します。|

## 使用例

以下の例では、画面上にない[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を[modelオブジェクト](../model/index.md)で取得可能にします。条件は「ビュー処理時」を指定します。

``` javascript
view.AlwaysGetColumns.Add('Status');
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.37.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
