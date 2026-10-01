---
title: view.FiltersCleared
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-filters-cleared
translationKey: server-script-view-filters-cleared
shortname: view.FiltersCleared
created: 2022-07-19
updated: 2025-01-30
---

## 概要

[サーバスクリプト](../index.md)で[view.ClearFilters](server-script-view-clear-filters.md)が呼ばれた後はtrueを返します。[view.ClearFilters](server-script-view-clear-filters.md)を呼び出し済みかどうかを確認したい場合に利用できます。

## 注意事項

1. 「ビュー処理時」の条件のみ使用できます。
1. 読取専用のため、`view.FiltersCleared`の値をスクリプトで設定することはできません。
1. こちらはサーバスクリプト機能で使用するオブジェクトです。スクリプト機能では使用できません。

## 使用例

以下の例では、`view.FiltersCleared`をブラウザのコンソールに表示します。

##### JavaScript

``` javascript linenums="1"
view.ClearFilters();
context.Log(view.FiltersCleared); // ClearFilters()呼び出し後なのでtrueになる。
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.13.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：view.ClearFilters](server-script-view-clear-filters.md)
