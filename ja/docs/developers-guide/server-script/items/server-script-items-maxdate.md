---
title: items.MaxDate
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-maxdate
translationKey: server-script-items-maxdate
shortname: items.MaxDate
created: 2025-05-09
updated: 2025-05-13
---

## 概要

[itemsオブジェクト](index.md)の「MaxDateメソッド」です。指定したテーブルにある対象の日付項目の最大値を取得します。選択条件を指定して集計対象のレコードを絞り込むことができます。

## 制限事項

1. [日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)以外では使用できません。

## 構文

```
items.MaxDate(siteId, columnName, view)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|siteId|object|○|対象テーブルのサイトIDを指定|
|columnName|string|○|計算対象の日付項目を指定|
|view|string|-|選択するレコードの条件を指定|

## 戻り値

対象テーブルの指定した日付項目の最大値を返却します。

指定した日付項目が見つからなかった場合は[utilities.EmptyTime](../utilities/server-script-utilities-emptytime.md)を返却します。

## 使用例①

以下の例では、サイトIDが 2 のテーブルに登録されているレコードでA（日付A）の最大値を取得します。

##### JavaScript

```
let maxDate = items.MaxDate(2, 'DateA');
```

## 使用例②

以下の例では、サイトIDが 2 のテーブルでStatus(状況)が200(実施中)のレコードでDateA(日付A)の最大値を取得します。

##### JavaScript

```
let view = {
    "View": {
        "ColumnFilterHash": {
            "Status": "[\"200\"]"
        }
    }
};
let maxDate = items.MaxDate(2, 'DateA', JSON.stringify(view));
context.Log(maxDate);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト：items](index.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [開発者ガイド：サーバスクリプト：utilities.EmptyTime](../utilities/server-script-utilities-emptytime.md)