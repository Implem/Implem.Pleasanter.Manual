---
title: レコードの遷移にAjaxを使用
category: エディタ
order: '24000'
status: ''
parts: ''
urlstring: table-management-ajax-transfer
translationKey: table-management-ajax-transfer
shortname: レコードの遷移にAjaxを使用
created: 2021-05-01
updated: 2023-05-12
---

## 概要

「＜前」、「次＞」のボタンでレコードを遷移した場合、「レコードの遷移にAjaxを使用」をチェックした状態では各項目の値のみが更新され、ページ自体の読み込みは行われません。そのためレコードの遷移をスムーズに行うことができます。

## 制限事項

1.  JavaScriptを使用している場合、レコードの遷移時にonloadイベントが動作しないようになります。レコードの遷移時にスクリプトを実行したい場合には[$p.events.on_editor_load](../../../../developers-guide/script/events/script-events-on-editor-load.md)を使用してください。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1.  対象の[テーブル](../../../../users-guide/table/index.md)を開いてください。
1.  「管理」メニューから[テーブルの管理](../../index.md)をクリックしてください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  画面下部にある「レコードの遷移にAjaxを使用」のチェックボックスをオンにしてください。
1.  画面下部の「更新」ボタンをクリックしてください。

## 関連情報

-   [開発者ガイド：スクリプト：$p.events.on_editor_load](../../../../developers-guide/script/events/script-events-on-editor-load.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理](../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
