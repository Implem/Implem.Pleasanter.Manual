---
title: $p.getField
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-field
translationKey: script-get-field
shortname: ''
created: 2019-10-16
updated: 2023-08-07
---

## 概要

対象の項目名からFieldを取得するメソッドです。対象の項目をラベルごと表示/非表示切り替えしたいとき等に使用してください。

## 構文

##### JavaScript

```
$p.getField('項目の名前')
```    

## 使用例

チェックボックスのON/OFFで項目の表示/非表示を切り替えます。

(1)以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、エディタタブから
チェックA項目と分類A項目を有効化してください。

(2)編集画面でチェック項目AのON/OFFを切り替えてください。

##### JavaScript

```
$p.events.on_editor_load = function () {
  $p.on('change', 'CheckA', function () {
    let classAField = $p.getField('ClassA')[0].id;
    document.getElementById($p.tableName() + '_CheckA').checked
      ? $('#' + classAField).hide()
      : $('#' + classAField).show()
  });
}
```