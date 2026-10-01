---
title: 自動ポストバック
category: エディタ
order: '11500'
status: ''
parts: ''
urlstring: table-management-auto-postback
translationKey: table-management-auto-postback
shortname: 自動ポストバック
created: 2021-05-02
updated: 2026-02-09
---

## 概要

[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)で[項目](../../columns/index.md)を編集後に自動的にサーバにポストバックを行う場合にはオンにします。「自動ポストバック」をオンにすることで[計算式](../../../../formulas/index.md)、[ルックアップ](../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)、[サーバスクリプト](../../../../../../developers-guide/server-script/basics/server-script-conditions.md)等の実行結果をすぐに[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)に反映することができます。「自動ポストバック」がオフの場合には、更新ボタン押下後に画面に反映します。

## 注意事項

1. 画面の[項目](../../columns/index.md)数が多い場合にはパフォーマンスが悪化することがあります。[自動ポストバック時に返却する項目](table-management-columns-returned-when-automatic-postback.md)を指定することで改善を図ることが可能です。

## 制限事項

1. [コメント項目](../../columns/table-management-comments.md)では使用できません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目](../../columns/index.md)
-   [テーブルの管理：計算式](../../../../formulas/index.md)
-   [応用編：リンク](../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [サーバスクリプト](../../../../../../developers-guide/server-script/basics/server-script-conditions.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック時に返却する項目](table-management-columns-returned-when-automatic-postback.md)
-   [テーブルの管理：項目：コメント](../../columns/table-management-comments.md)