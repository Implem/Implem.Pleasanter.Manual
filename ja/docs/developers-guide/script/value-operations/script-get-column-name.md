---
title: $p.getColumnName
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-column-name
translationKey: script-get-column-name
shortname: ''
created: 2019-08-10
updated: 2023-07-20
---

## 概要

対象項目のカラム名（データベースの列名）を取得するメソッドの説明をします。

## 構文

##### JavaScript

```
$p.getColumnName('項目名')
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、編集画面に遷移してください。

##### JavaScript

```
$p.events.on_editor_load = function () {
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: $p.getColumnName('タイトル')
    }));
}
```