---
title: $p.id
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-id
translationKey: script-id
shortname: ''
created: 2019-08-10
updated: 2026-09-07
---

## 概要

サイトIDまたはレコードIDを取得します。

## 構文

##### JavaScript

```
$p.id()
```    

## 使用例

(1)アカウント管理者でログインし、テーブルを作成します。

(2) [スクリプト](../../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載してください。出力先には「全て」をチェックして更新します。  

##### JavaScript  

```
$p.events.after_set_Update = function () {
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: 'このレコードIDは [' + $p.id() + '] です。'
        })
    );
}
```
(3) 任意のレコードを更新して、画面下部にメッセージが表示されることを確認します。