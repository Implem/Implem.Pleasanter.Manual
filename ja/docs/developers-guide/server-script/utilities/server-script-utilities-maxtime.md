---
title: utilities.MaxTime
icon: material/alpha-m-box
category: サーバスクリプト
order: '6510'
status: ''
parts: ''
urlstring: server-script-utilities-maxtime
translationKey: server-script-utilities-maxtime
shortname: ''
created: 2025-03-28
updated: 2025-04-08
---

## 概要

[サーバスクリプト](../index.md)でローカル時間における最大日時をUTCで返します。

## 構文

```
utilities.MaxTime()
```

## パラメータ

パラメータはありません。

## 戻り値

ローカル時間における最大日時（「パラメータ設定：General.json」のMaxTimeで指定した日時）をUTCで返却します。MaxTimeが"2100/1/1"の場合、「2099/12/31 15:00:00」が返却されます。

## 使用例

以下の例では、日付Aに最小日時を入力します。サーバスクリプト内ではUTCの日時「2099/12/31 15:00:00」が代入されますが、サーバスクリプト終了後、日付Aにはローカル時刻に変換された日時「2100/01/01 00:00:00」が設定されます。

##### JavaScript

```
model.DateA = utilities.MaxTime();
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