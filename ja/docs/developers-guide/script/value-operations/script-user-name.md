---
title: $p.userName
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-user-name
translationKey: script-user-name
shortname: ''
created: 2019-08-19
updated: 2026-06-29
---

## 概要

ログインしているユーザの名前を取得する関数について説明します。ログインしているユーザの名前を取得したい場合に使用してください。

## 構文

```
$p.userName()
```    

## 使用例

(1) アカウント管理者でログインし、テーブルを作成します。

(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載します。
出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します。  

##### JavaScript

```
alert('ログインIDは [' + $p.userName() + '] です。');
```
(3) 一覧画面に遷移してください。