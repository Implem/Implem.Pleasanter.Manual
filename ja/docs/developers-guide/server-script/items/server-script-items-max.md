---
title: items.Max
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-max
translationKey: server-script-items-max
shortname: items.Max
created: 2021-01-27
updated: 2026-05-01
---

## 概要

[itemsオブジェクト](index.md)の「Maxメソッド」です。指定したテーブルにある対象の数値項目の最大値を取得します。選択条件を指定して集計対象のレコードを絞り込むことができます。

## 制限事項

1. [数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)以外では使用できません。

## 構文

```
items.Max(siteId, columnName, view)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|siteId|object|○|対象テーブルのサイトIDを指定|
|columnName|string|○|計算対象の数値項目を指定|
|view|string|-|選択するレコードの条件を指定|

## 戻り値

対象テーブルの指定した数値項目の最大値を返却します。

## 使用例①

以下の例では、サイトIDが 2 のテーブルに登録されているレコードでNumA（数値A）の最大値を取得します。

##### JavaScript

```
let max = items.Max(2, 'NumA');
```

## 使用例②

以下の例では、サイトIDが 2 のテーブルでStatus(状況)が200(実施中)のレコードでNumA(数値A)の最大値を取得します。

##### JavaScript

```
let view = {
    "View": {
        "ColumnFilterHash": {
            "Status": "[\"200\"]"
        }
    }
};
let max = items.Max(2, 'NumA', JSON.stringify(view));
context.Log(max);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト：items](index.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)