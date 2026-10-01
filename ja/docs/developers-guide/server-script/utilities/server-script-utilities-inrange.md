---
title: utilities.InRange
icon: material/alpha-m-box
category: サーバスクリプト
order: '6520'
status: ''
parts: ''
urlstring: server-script-utilities-inrange
translationKey: server-script-utilities-inrange
shortname: utilities.InRange
created: 2021-08-20
updated: 2025-01-30
---

## 概要

[サーバスクリプト](../index.md)で指定された日時がプリザンターが扱える日時の有効範囲内かチェックします。

## 構文

```
utilities.InRange(datetime);
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|datetime|DateTime|○|日時|

## 戻り値

有効範囲内を示すbool値を返します。

## 使用例

以下の例では、日付Aに有効な日時が格納されている場合にログを出力します。

##### JavaScript

```
if (utilities.InRange(model.DateA)) {
    context.Log('In range');
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.39.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)