---
title: レコードの一覧編集
category: テーブル機能
order: '154'
status: ''
parts: ''
urlstring: table-record-editongrid
translationKey: table-record-editongrid
shortname: 一覧編集
created: 2019-10-01
updated: 2025-09-19
---

## 概要

通常、項目の内容を編集する際、編集画面にて行う必要がありますが、この一覧編集機能を設定することで一覧画面にて編集を行うことが可能になります。一覧編集機能で[添付ファイル項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)に添付ファイルを追加・削除することも可能です。

## 前提条件

1. [テーブル](../../index.md)の「変更権限」が必要です。
1. [一覧編集種別](../../../../managers-guide/manage-table/grid/table-management-grid-editor-type.md)を「一覧画面で編集」に設定する必要があります。
1. [サイト統合](table-site-integration.md)を使用しているテーブルでは一覧編集機能は使えません。
1. 「タイトル/内容項目」は編集できません。
1. [コメント項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)は登録・編集できません。
1. [リンク](../../../hands-on/advanced/advanced-operations-link.md)された[テーブル](../../index.md)から[一覧画面](../data-analysis/table-grid.md)に表示した項目は編集できません。
1. 「カスタムデザイン」を使用している項目は登録・編集できません。

## 操作手順

1. 対象テーブルへ移動してください。
1. 画面下部にある「編集モード」ボタンをクリックしてください。
![一覧画面下部の「編集モード」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/81fdb7b3a9554de2941ec607fb886d34.png)
1. 項目の設定値を編集してください。※この手順では[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目の設定を編集しています。
![一覧上で状況項目の値を編集している画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/1914c72093e94dd6bc17629a4bd6fec3.png)
1. 編集が完了したら、画面下部にある「更新」ボタンをクリックしてください。
![一覧編集中の画面下部の「更新」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/32d9a57974c640adab1f4f187d13d60b.png)
1. 一覧画面に戻す場合は、「一覧モード」ボタンをクリックしてください。
![画面下部の「一覧モード」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/066326f9e63c4aa69fafc2fe14d327a4.png)
1. 画面が一覧画面になったことを確認してください。
![一覧モードに戻った一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/6509cd99059042e48e965e4e45efe1c1.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.1.0以降|一覧編集画面で添付ファイルの追加・削除を行える機能を追加|

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [テーブル機能](../../index.md)
-   [テーブルの管理：一覧画面：一覧編集種別](../../../../managers-guide/manage-table/grid/table-management-grid-editor-type.md)
-   [テーブル機能：サイト統合](table-site-integration.md)
-   [テーブルの管理：項目：コメント](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [応用編：リンク](../../../hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)
-   [テーブルの管理：項目：状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)