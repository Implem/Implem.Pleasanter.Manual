---
title: view.FilterNegative
icon: material/alpha-p-box
category: サーバスクリプト
order: '4040'
status: ''
parts: ''
urlstring: server-script-view-filter-negative
translationKey: server-script-view-filter-negative
shortname: view.FilterNegative
created: 2022-11-15
updated: 2025-01-30
---

## 概要

[view](index.md)オブジェクトの「FilterNegative」です。[サーバスクリプト](../index.md)で項目を否定の条件でフィルタする際に使用します。

## 前提条件

[否定フィルタを使用する](../../../managers-guide/manage-table/filter/table-management-filter-use-negative-filter.md)のチェックがオンになっていることが必要です。

## 使用例

以下の例では、分類Aを否定の条件でフィルタします。

##### JavaScript

```javascript linenums="1"
view.Filters.ClassA = '東京都中野区';
view.FilterNegative('ClassA');
```

### 使用前

![view.FilterNegativeを使う前の一覧画面](https://pleasanter.org/files/images/ja/developers-guide/server-script/view/assets/d01b007eb6f64b68baeedf779bcbfc0e.png)

### 使用後

一覧画面で自動的にフィルタがセットされ、否定の条件でレコードが表示されます。

![否定の条件でフィルタされた一覧画面](https://pleasanter.org/files/images/ja/developers-guide/server-script/view/assets/a1999e34bf9441c9a95d7b58be8358f0.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.21.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：フィルタ：否定フィルタを使用する](../../../managers-guide/manage-table/filter/table-management-filter-use-negative-filter.md)
