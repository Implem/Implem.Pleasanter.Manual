---
title: $p.siteId
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-site-id
translationKey: script-site-id
shortname: ''
created: 2019-08-15
updated: 2026-09-07
---

## 概要

リンクされたテーブルのサイトのIDを取得します。

## 構文

```
$p.siteId(<サイト名>)
```    

## サンプルコード

以下のサンプルコードをプリザンターのスクリプトへ設定し、出力先を「新規作成」にするとレコードの新規作成画面で該当サイトのサイトIDがアラート表示されます。

##### JavaScript

```
alert($p.siteId('課題管理'));
```