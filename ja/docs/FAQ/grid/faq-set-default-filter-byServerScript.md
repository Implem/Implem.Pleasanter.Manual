---
title: 一覧画面を開いた時にビューを使わずにフィルタを有効にしたい（サーバスクリプト）
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-set-default-filter-byServerScript
translationKey: faq-set-default-filter-byServerScript
shortname: ''
created: 2024-03-11
updated: 2024-04-29
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)の[view.Filters](../../developers-guide/server-script/view/server-script-view-filters.md)を使用してください。

---

## 制限事項

[サーバスクリプト](../../developers-guide/server-script/index.md)により[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)を設定した項目は[一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)の[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)操作が動作しません。[サーバスクリプト](../../developers-guide/server-script/index.md)により上書きされます。

## 概要

ビューを使用せず、フィルタの検索条件を入力した状態で一覧画面を表示したい場合は、[サーバスクリプト](../../developers-guide/server-script/index.md)で実現可能です。
詳しくは「[開発者ガイド：サーバスクリプト：view.Filters](../../developers-guide/server-script/view/server-script-view-filters.md)」を参照ください。

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：サーバスクリプト：view.Filters](../../developers-guide/server-script/view/server-script-view-filters.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能：レコードの一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)