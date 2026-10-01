---
title: $p.controller
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-controller
translationKey: script-controller
shortname: ''
created: 2020-10-30
updated: 2023-08-16
---

## 概要

AjaxのPOSTリクエストによるコントローラの種類が取得できるスクリプト機能になります。

## 取得可能な値の一覧

|取得可能な画面|取得値|
|:--|:--|
|テナント管理画面|tenants|
|組織管理画面|depts|
|グループ管理画面|groups|
|ユーザ管理画面|users|
|上記以外の画面|items|

## 構文

##### JavaScript

```
$p.controller();
``` 

## 使用例

(1) フォルダまたテーブルを作成してください(この例ではitemsを取得します)。  
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載し、出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します(Wikiの場合は出力先は「編集」をチェック)。  

##### JavaScript

```
alert('このコントローラーの種類は [' + $p.controller() + '] です。');
``` 

(3) 一覧画面に遷移してください。