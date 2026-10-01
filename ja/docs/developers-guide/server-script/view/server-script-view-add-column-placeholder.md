---
title: view.AddColumnPlaceholder
icon: material/alpha-m-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-add-column-placeholder
translationKey: server-script-view-add-column-placeholder
shortname: view.AddColumnPlaceholder
created: 2021-10-18
updated: 2025-01-30
---

## 概要

[view](index.md)オブジェクトの「AddColumnPlaceholderメソッド」です。[サーバスクリプト](../index.md)で[拡張SQL](../../extended-features/extended-sql/index.md)の[OnSelectingWhere](../../../FAQ/grid/faq-extended-sql-selecting-where.md)のプレースホルダに動的な[カラム名](../../dev-column-name.md)を指定する際に使用します。

## 制限事項

1. [カラム名](../../dev-column-name.md)以外の文字列を指定することはできません。

## 構文

``` javascript
view.AddColumnPlaceholder(placeholder, columnName);
```

## パラメータ

|No|パラメータ|型|必須|概要|
|:--|:----------|:----------|:---:|:---------------------------|
|1|placeholder|string|○|プレースホルダ|
|2|columnName|string|○|[カラム名](../../dev-column-name.md)|

## 戻り値

戻り値はありません。

## 使用例

以下の例では、ユーザID 3 以外のユーザに Name が SelectingWhereName の[拡張SQL](../../extended-features/extended-sql/index.md)を適用します。また、SQL内にある `{{DynamicColumn}}` のプレースホルダ文字列を ClassA に置換して実行します。

##### 拡張SQL

``` json linenums="1" hl_lines="5"
{
    "Name": "SelectingWhereName",
    "SpecifyByName": true,
    "OnSelectingWhere": true,
    "CommandText": "(\"Results\".\"Status\"=900 and \"Results\".\"ClassB\"={{DynamicColumn}})"
}
```

##### JavaScript

``` javascript linenums="1"
if (context.UserId !== 3) {
    view.OnSelectingWhere = 'SelectingWhereName';
    view.AddColumnPlaceholder('DynamicColumn', 'ClassA');
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.2.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../extended-features/extended-sql/index.md)
-   [FAQ：一覧表示するレコードを所属組織別に分けたい](../../../FAQ/grid/faq-extended-sql-selecting-where.md)
-   [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)
