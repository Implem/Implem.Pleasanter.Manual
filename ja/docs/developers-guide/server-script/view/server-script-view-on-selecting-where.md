---
title: view.OnSelectingWhere
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-on-selecting-where
translationKey: server-script-view-on-selecting-where
shortname: view.OnSelectingWhere
created: 2021-10-18
updated: 2025-01-30
---

## 概要

[view](index.md)オブジェクトの[OnSelectingWhere](../../../FAQ/grid/faq-extended-sql-selecting-where.md)です。[サーバスクリプト](../index.md)で[拡張SQL](../../extended-features/extended-sql/index.md)の[OnSelectingWhere](../../../FAQ/grid/faq-extended-sql-selecting-where.md)を動的に指定する際に使用します。

## 使用例

以下の例では、ユーザID 3 以外のユーザに Name が SelectingWhereName の[拡張SQL](../../extended-features/extended-sql/index.md)を適用します。

##### JavaScript

``` javascript linenums="1"
if (context.UserId !== 3) {
    view.Filters.OnSelectingWhere = 'SelectingWhereName';
}
```

##### JSON

``` json
{
    "Name": "SelectingWhereName",
    "SpecifyByName": true,
    "OnSelectingWhere": true,
    "CommandText": "([Issues].[Status]=900)"
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.2.0 以降|機能追加|

## 関連情報

-   [FAQ：一覧表示するレコードを所属組織別に分けたい](../../../FAQ/grid/faq-extended-sql-selecting-where.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../extended-features/extended-sql/index.md)
