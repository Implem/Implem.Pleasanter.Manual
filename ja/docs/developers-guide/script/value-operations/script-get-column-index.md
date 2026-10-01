---
title: $p.getGridColumnIndex
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-column-index
translationKey: script-get-column-index
shortname: ''
created: 2019-09-02
updated: 2026-07-01
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)にて、レコードの表示名のデータが何列目にあるか取得するメソッドの説明をします。

## 構文

##### JavaScript

```
$p.getGridColumnIndex('(表示名)')
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定し、出力先を「編集」にした後、一覧画面に遷移してください。

##### JavaScript

```
$p.events.on_grid_load = function () {
    $p.clearMessage();
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: $p.getGridColumnIndex('タイトル/内容')
    }));
}
```