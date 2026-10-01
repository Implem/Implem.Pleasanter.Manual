---
title: $p.getGridCell
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-grid-cell
translationKey: script-get-grid-cell
shortname: ''
created: 2019-09-02
updated: 2026-07-01
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)のtdタグの要素を取得するメソッドに関する説明をします。

## 構文

##### JavaScript

```
$p.getGridCell(レコードID,' 一覧レコード上の表示名')
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、一覧画面を読み込んだときにレコードID:123となるレコードが存在する場合、画面下部にそのレコードのタイトルが表示されます。

##### JavaScript

```
$p.events.on_grid_load = function () {
    $p.clearMessage();
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: $p.getGridCell(123, 'タイトル/内容')[0].textContent
    }));
}
```