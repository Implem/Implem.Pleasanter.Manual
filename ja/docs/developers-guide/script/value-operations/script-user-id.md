---
title: $p.userId
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-user-id
translationKey: script-user-id
shortname: ''
created: 2019-08-19
updated: 2026-09-07
---

## 概要

ログインしているユーザのユーザIDを取得する関数について説明します。ユーザIDを取得したい場合に使用してください。

## 使い方

```
$p.userId()
```    

## 事前準備

(1)アカウント管理者でログインし、テーブルを作成します。  
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載します。
出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します。  

##### JavaScript

```
alert('ユーザIDは [' + $p.userId() + '] です。');
```
(3) 一覧画面に遷移してください。