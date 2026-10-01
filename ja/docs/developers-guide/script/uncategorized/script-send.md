---
title: $p.send
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-send
translationKey: script-send
shortname: ''
created: 2025-04-23
updated: 2025-05-02
---

## 概要

指定したIDのHTMLタグの入力内容をサーバにAjax通信で送信し、取得したレスポンスを元に該当IDの画面項目を再描画します。

## 構文

##### JavaScript

```
$p.send(<対象HTMLタグのID>)
```    

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|対象HTMLタグのID|HTMLタグのid名を指定します|

## 使用例

下記スクリプトを画面の初期表示時に読み込むと、一覧画面が2秒毎に再描画されるようになります。

##### JavaScript

```
setInterval(function() {
  $p.send($('#Grid'));
}, 2000);
```