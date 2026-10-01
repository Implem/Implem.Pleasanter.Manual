---
title: responses.Reload
icon: material/alpha-m-box
category: サーバスクリプト
order: '80000'
status: ''
parts: ''
urlstring: server-script-responses-reload
translationKey: server-script-responses-reload
shortname: responses.Reload
created: 2022-07-21
updated: 2023-08-22
---

## 概要

[サーバスクリプト](../index.md)で指定した項目の再読み込みを行うメソッドです。

## 構文

```
responses.Reload(type, id)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|type|string|○|再読み込みを行う項目の領域を指定します。|
|id|string|○|再読み込みを行う項目を指定します。|

## 使用例

以下の例では、サイトID: 123456の記録テーブルのレコードを取得し、そのレコード情報(レコードID、分類A)をもとに一覧画面のフィルタにある分類Jの選択肢一覧を作成して再読み込みします。

##### JavaScript

```
if (context.Action === 'index') {
    const records = items.Get(123456);
    for (let record of records) {
        columns.ClassJ.AddChoiceHash(record.ResultId, record.ClassA);
    }
    responses.Reload('Filter', 'ClassJ');
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)