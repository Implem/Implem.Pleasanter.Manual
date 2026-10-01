---
title: インポート
category: インポート
order: '0'
status: ''
parts: ''
urlstring: table-management-import
translationKey: table-management-import
shortname: インポート
created: 2022-06-20
updated: 2026-03-10
---

## 概要

インポートを行う際のオプションを設定します。

## 前提条件

1. この操作は「サイトの管理権限」が必要です。

## 注意事項

1. [インポート](../../../users-guide/table/record-authoring/create-records/table-record-import.md)によりレコードを追加・更新するときは、CSVから読み込む項目を制限しても、インポートするすべての項目に対して入力検証が実行されます。インポートの対象外とした項目に入力検証が設定されており、検証エラーに該当するデータが含まれる場合は、インポートダイアログにその旨のエラーが表示されます。

## 操作手順

1. 対象のテーブルを開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. インポートタブを開いてください。
1. 設定後、画面下部の「更新」ボタンをクリックしてください。

## 設定内容

![テーブルの管理の「インポート」タブの設定項目](https://pleasanter.org/files/images/ja/managers-guide/manage-table/import/assets/8376a696c8be4a0c92fdc0171cd398fe.png)

|項目名|説明|設定方法|
|:---|:---|:---|
|文字コード|CSVファイルの既定の文字コードを選択| [Shift-JIS] または [UTF-8] から選択|
|キーが一致するレコードを更新する|キーが一致するレコードを更新するかの既定の動作を指定|チェックON/OFFを指定|
|既定のインポートキー|既定のインポートキーとする項目を選択|テーブル設定の[インポートのキー](../editor/editor-settings/advanced-settings/general/table-management-import-key.md)でチェックした項目のリストから選択|
|入力必須項目の空白をエラーにする|チェックを付けた場合、CSVファイル内に入力必須項目が空白のレコードが存在する、または入力必須項目の列が存在しない場合にインポートエラーとなります|チェックON/OFFを指定|
|移行モードを許可|チェックを付けた場合、移行モードでのインポートが利用可能となります|チェックON/OFFを指定|

## 動作イメージ

上記の各設定は、対象のテーブルでインポート操作を行ったとき表示されるインポートダイアログの既定値として反映されます。 
![設定が既定値として反映されたインポートダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/import/assets/c3af308e9823482f9c05aa058439b52b.png)
インポートのキーについては[インポート時のキー項目指定](../../../users-guide/table/record-authoring/create-records/table-record-import-key.md)を参照ください。

### 移行モードを許可について

「移行モードを許可」にチェックを付けた場合のみ、インポートダイアログに「移行モード」チェックボックスが表示されます。
![「移行モード」チェックボックスが表示されたインポートダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/import/assets/1d95f3e7028747098be7373d5d3956a2.png)
移行モードについては[移行モードでのレコードのインポート](../../../users-guide/table/record-authoring/create-records/table-record-import-migrate-mode.md)を参照ください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.11.2 以降|インポート時のキーを選択可能にする機能を追加|
|1.4.15.0 以降|「入力必須項目の空白をエラーにする」チェックボックスを追加|
|1.4.16.0 以降|「移行モードを許可」チェックボックスを追加|

## 関連情報

-   [組織管理機能：インポート](../../department-administration/dept-import.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：インポートのキー](../editor/editor-settings/advanced-settings/general/table-management-import-key.md)
-   [テーブル機能：インポート時のキー項目指定](../../../users-guide/table/record-authoring/create-records/table-record-import-key.md)
-   [テーブル機能：移行モードでのレコードのインポート](../../../users-guide/table/record-authoring/create-records/table-record-import-migrate-mode.md)