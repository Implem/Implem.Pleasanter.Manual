---
title: 複数項目の一括更新
category: 一覧画面
order: '281'
status: ''
parts: ''
urlstring: table-management-bulk-update-multi-columns
translationKey: table-management-bulk-update-multi-columns
shortname: 複数項目の一括更新
created: 2022-04-11
updated: 2025-08-13
---

## 概要

一覧画面上で複数項目を一括更新する機能です。

## 制限事項

1. [添付ファイル項目](../editor/editor-settings/columns/table-management-attachments.md)は登録・編集できません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. 画面下部にある[一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)のセクションから、「新規作成」ボタンをクリックしてください。
1. 表示されたダイアログに、一括更新の設定をして「追加」をクリックしてください。
1. 画面下部の「更新」ボタンをクリックしてください。

## 設定イメージ

「一括更新の設定」セクションから「新規作成」をクリックします。
![テーブルの管理の「一括更新の設定」セクションと「新規作成」ボタン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/46f22a933f494ebd86205c14c0eff277.png)

表示されたダイアログにて一括で更新したい項目を有効化します。
![一括更新の設定ダイアログ。一括更新したい項目を有効化する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/e49755ce73754ba38d00d9401539255e.png)

「詳細設定」より項目ごとに一括更新の詳細設定ができます。
![一括更新の項目ごとの詳細設定ダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/7f88c66c56824c3ba665ac95fa20c6e0.png)

## 動作イメージ

一括更新したいデータを選択し、[一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)をクリックします。
![一覧画面でレコードを選択して「一括更新」をクリックするところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/9544a74bcbca496eab3cd8b047f68af5.png)

表示されたダイアログに一括更新の設定で有効化された項目が表示されるので対象項目に値を入力し、[一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)をクリックします。
![一括更新のダイアログ。有効化した項目に値を入力する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/grid/assets/72196b399fc6477d8c8762a7c58fc480.png)
入力した値で、一覧で選択したレコード全てに更新されます。

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../editor/editor-settings/columns/table-management-attachments.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：一覧画面](index.md)
-   [テーブル機能：レコードの一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)