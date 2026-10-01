---
title: $p.getGridRow
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-grid-row
translationKey: script-get-grid-row
shortname: ''
created: 2019-09-02
updated: 2023-08-07
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)にて、レコードの表示名のデータが何列目にあるか取得するメソッドの説明をします。

## 概要

```
$p.getGridRow(レコードID)
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定すると、一覧画面を読み込んだときにレコードID:123のタイトルが表示されます（一覧画面にてタイトル項目を3番目に設置しているとします）
```
$p.events.on_grid_load = function () {
    $p.clearMessage();
    $p.setMessage('#Message', JSON.stringify({
        Css: 'alert-success',
        Text: $p.getGridRow(123)[0].children[2].textContent
    }));
}
```