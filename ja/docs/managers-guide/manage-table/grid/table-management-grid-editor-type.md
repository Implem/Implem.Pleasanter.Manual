---
title: 一覧編集種別
category: 一覧画面
order: '254'
status: ''
parts: ''
urlstring: table-management-grid-editor-type
translationKey: table-management-grid-editor-type
shortname: 一覧編集種別
created: 2021-05-06
updated: 2025-01-30
---

## 概要

「一覧編集種別」は一覧画面上でレコードを編集可能にする設定です。既定では[一覧編集](../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)が無効化されています。「一覧画面で編集」と「ダイアログ編集」を選択すると[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)に遷移せずにレコードの編集が行えます。[添付ファイル項目](../editor/editor-settings/columns/table-management-attachments.md)に添付ファイルを追加・削除することも可能です。

## 制限事項

1. 「タイトル/内容項目」は編集できません。
1. [コメント項目](../editor/editor-settings/columns/table-management-comments.md)は登録・編集できません。
1. 「ダイアログ編集」で新規登録を行うことはできません。
1. 「ダイアログ編集」でリンク元テーブル、リンク先テーブルは表示・編集できません。
1. [リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)された[テーブル](../../../users-guide/table/index.md)から[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)に表示した項目は編集できません。
1. 「一覧画面で編集」で「カスタムデザイン」を使用している項目は登録・編集できません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. 画面下部にある「一覧編集種別」のセレクトボックスから任意の設定を選択してください。
1. 画面下部の「更新」ボタンをクリックしてください。

## 動作イメージ（一覧画面で編集）

「一覧編集種別」を「一覧画面で編集」に設定すると、一覧画面下部のコントロールエリアに「編集モード」というボタンが表示されます。  

![一覧画面下部のコントロールエリアに「編集モード」ボタンが出た状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/74093180a301405bbe96d79bb8f29d95.png)

**一覧編集モード**  
![一覧編集モードでレコードをその場で編集できる一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/f37dcebb28ca46a785ff75c5d209c214.png)

**アイコン説明**  
![一覧編集モードで使うアイコンの説明](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/96f54d65578748ecb39a51935e656182.png)

先に誰かが更新した場合、そのレコードの更新はできません。その際は、更新アイコンを押してレコードの情報を最新にしてください。  
![先に他の人が更新したため更新できないレコードの表示](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/dec4d3e6a9f74e239abfbe528f11bb0a.png)

### [一覧上に履歴を表示](table-management-history-on-grid.md)をチェックし、一覧画面で「履歴も表示」をチェックした状態

![「履歴も表示」をチェックして履歴を含めて表示した一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/75df27d802a346e28702c4ef4230fbfb.png)

## 動作イメージ（ダイアログ編集）

「一覧編集種別」を「ダイアログで編集」に設定すると、一覧画面からレコードをクリックすると編集画面がダイアログとして表示されます。レコード移動時に一覧画面の再読み込みをしないので複数レコードを編集する場合に使用できます。  
![レコードをクリックしてダイアログで編集している一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/aa174eb9a6ae4c61ad81ff9cd5927eff.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.1.0以降|一覧編集画面で添付ファイルの追加／削除を行える機能を追加|

## 関連情報

-   [テーブル機能：レコードの一覧編集](../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目：添付ファイル](../editor/editor-settings/columns/table-management-attachments.md)
-   [テーブルの管理：項目：コメント](../editor/editor-settings/columns/table-management-comments.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：一覧画面](index.md)
-   [テーブルの管理：一覧画面：一覧上に履歴を表示](table-management-history-on-grid.md)