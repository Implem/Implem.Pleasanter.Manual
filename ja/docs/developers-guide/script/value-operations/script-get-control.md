---
title: $p.getControl
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-control
translationKey: script-get-control
shortname: $p.getControl
created: 2019-08-11
updated: 2026-09-07
---

## 概要

__編集画面上__で対象の項目名から要素を取得するメソッドの説明です。  
対象の項目名のid名や値を出力したいときに使用してください。

## 構文

##### JavaScript

```
$p.getControl('項目の名前')
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、編集画面に遷移してください。

##### JavaScript

```
$p.events.on_editor_load = function () {
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: $p.getControl('Title').val()
    }));
}
```