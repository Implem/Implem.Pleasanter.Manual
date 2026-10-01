---
title: $p.tableName
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-table-name
translationKey: script-table-name
shortname: ''
created: 2020-10-30
updated: 2023-08-16
---

## 概要

AjaxのPOSTリクエストによるスクリプトを配置したフォルダまたはテーブルの種類が取得できる機能になります。

## 取得可能な値の一覧

|テーブル種類|取得値|
|:--|:--|
|フォルダ|Sites|
|記録テーブル|Results|
|期限付きテーブル|Issues|
|Wiki|Wikis|

## 構文

##### JavaScript

```
$p.tableName();
``` 

## 使用例

(1) フォルダまたテーブルを作成してください  
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載し、出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します(Wikiの場合は出力先は「編集」をチェック)。  

##### JavaScript

```
alert('このテーブルの種類は [' + $p.tableName() + '] です。');
``` 

(3) 一覧画面に遷移してください(Wikiの場合は編集画面に遷移)。
