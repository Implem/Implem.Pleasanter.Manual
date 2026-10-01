---
title: $p.loginId
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-login-id
translationKey: script-login-id
shortname: ''
created: 2019-08-19
updated: 2026-06-29
---

## 概要

ログインIDを取得する関数について説明します。ログインIDを取得したい場合に使用してください。

## 構文

```
$p.loginId()
```    

## 使用例

(1)アカウント管理者でログインし、テーブルを作成します。
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載します。出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します。  

##### JavaScript

```
$p.setMessage('#Message', JSON.stringify({
    Css: 'alert-success',
    Text: 'ログインIDは [' + $p.loginId() + '] です。'
}));
```
(3) 一覧画面に遷移してください。