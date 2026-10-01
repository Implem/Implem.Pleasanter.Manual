---
title: $p.on
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-on
translationKey: script-on
shortname: ''
created: 2020-10-21
updated: 2026-09-07
---

## 概要

監視項目がイベント発火した時に、記述した任意処理を実行する機能になります。

## 構文

##### JavaScript

```
$p.on(<イベント名>, <監視項目>, <任意の処理>)
```    

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|イベント名|Ajaxのイベント名|  
|監視項目|対象となる項目の[データベース上のカラム名](../../dev-column-name.md)|
|任意処理|イベント発火時の処理|

## 記述例

##### JavaScript

```
$p.on('change', 'ClassA', function () {
    console.log('分類Aの値が変更されました。')
})
```