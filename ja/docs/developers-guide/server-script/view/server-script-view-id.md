---
title: view.Id
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-id
translationKey: server-script-view-id
shortname: view.Id
created: 2022-02-09
updated: 2023-08-25
---

## 概要

[view](index.md)オブジェクトのIdです。[サーバスクリプト](../index.md)で[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)で選択している[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)のIdを取得することができます。

## 注意事項

1. 「ビュー処理時」の条件のみ使用できます。
1. 読取専用のため、`view.Id`の値をスクリプトで設定することはできません。
1. ビューのIdは0から始まります。一覧画面でビュー選択が未選択の場合`view.Id`は０となります。
1. こちらはサーバスクリプト機能で使用するオブジェクトです。スクリプト機能では使用できません。

## 使用例

以下の例では、一覧画面で選択しているビューのIdをコンソールに表示します。

##### JavaScript

```javascript
context.Log("選択ビューのID : " + view.Id);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト：view](index.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [応用編：ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)
