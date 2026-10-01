---
title: $p.groupIds
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-groupIds
translationKey: script-groupIds
shortname: ''
created: 2025-06-27
updated: 2026-09-09
---

## 概要

所属するグループのIDリストを取得する関数について説明します。ログインユーザが所属するグループのIDリストが取得できます。

## 構文

```
$p.groupIds()
```    

## 使用例

(1)アカウント管理者でログインし、テーブルを作成します。
(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載します。出力先には[一覧](../../../managers-guide/manage-table/grid/index.md)をチェックして更新します。  

##### JavaScript

```
$p.setMessage('#Message', JSON.stringify({
    Css: 'alert-success',
    Text: '所属するグループのIDは [' + $p.groupIds().join(', ') + '] です。'
}));
```
(3) 一覧画面に遷移してください。