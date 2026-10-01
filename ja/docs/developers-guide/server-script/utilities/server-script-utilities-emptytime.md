---
title: utilities.EmptyTime
icon: material/alpha-m-box
category: サーバスクリプト
order: '6510'
status: ''
parts: ''
urlstring: server-script-utilities-emptytime
translationKey: server-script-utilities-emptytime
shortname: utilities.EmptyTime
created: 2025-03-28
updated: 2025-04-08
---

## 概要

[サーバスクリプト](../index.md)で未設定を表す日時「0001/01/01 0:00:00」を返します。

## 構文

```
utilities.EmptyTime()
```

## パラメータ

パラメータはありません。

## 戻り値

未設定を表す日時「0001/01/01 0:00:00」

## 使用例

以下の例では、日付Aに「0001/01/01 0:00:00」の値を設定します。この値は設定可能な日付の範囲外の値となるため、サーバ側では未設定値として扱われます。

##### JavaScript

```
model.DateA = utilities.EmptyTime();
```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.15.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：スクリプト](../../../managers-guide/manage-table/scripts/index.md)