---
title: 移行モードでのレコードのインポート
category: テーブル機能
order: '202'
status: ''
parts: ''
urlstring: table-record-import-migrate-mode
translationKey: table-record-import-migrate-mode
shortname: 移行モードでのレコードのインポート
created: 2025-05-08
updated: 2026-08-28
---

## 概要

移行モードでは、インポートによるレコード作成時に、「作成者」、「作成日時」、「更新者」、「更新日時」の値を取り込むことができます。

移行モードを有効化しても、レコードの履歴をインポートすることはできません。

## 前提条件

1. [テーブルの管理](../../../../managers-guide/manage-table/index.md)画面の[インポート](../../../../managers-guide/manage-table/import/index.md)タブで「移行モードを許可」を有効化してください。

## 説明

移行モードで「作成者」、「作成日時」、「更新者」、「更新日時」の項目を設定したCSVファイルをインポートすると、それらの値が追加レコードに反映されます。通常のインポート時との違いは、以下の表のとおりです。

|項目名|通常のインポート<br>（レコード追加時）|移行モード|
|:--|:--|:--|
|作成者|インポート操作を行ったユーザ|CSVに設定したユーザ|
|作成日時|インポート操作を行った日時|CSVに設定した日時|
|更新者|インポート操作を行ったユーザ|CSVに設定したユーザ|
|更新日時|インポート操作を行った日時|CSVに設定した日時|

ただし、「キーが一致するレコードを更新」する設定の場合、値が反映されるのは追加レコードのみで、更新レコードには反映されません。

### 無効な値の場合の設定値

CSVに対象の項目が存在しない、または無効な値が設定されていた場合に追加レコードに設定される値を以下に示します。

|項目|無効な値|設定値|
|-|-|-|
|作成者|存在しないユーザのIDまたは名前|空白|
|作成日時|日時に変換できない文字列、または[General.json](../../../../setup/parameters/general.json.md)の「MinTime」「MaxTime」の範囲外の日時|現在の日時|
|更新者|存在しないユーザのIDまたは名前|空白|
|更新日時|日時に変換できない文字列、または[General.json](../../../../setup/parameters/general.json.md)の「MinTime」「MaxTime」の範囲外の日時|現在の日時|

### 更新レコードの設定値

更新レコードの場合は移行モードは適用されず、通常のインポートと同様の値が設定されます。

## 操作方法

インポートのダイアログで"移行モード"をチェックした状態でインポートを実行します。
![「移行モード」をチェックしたインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/e4f45cae6a8e45c0b6ec41cbec130dc6.png)

インポート操作について詳しくは「[テーブル機能：レコードのインポート](table-record-import.md)」を参照ください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.16.0 以降|機能追加|

## 関連情報

-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [組織管理機能：インポート](../../../../managers-guide/department-administration/dept-import.md)
-   [パラメータ設定：General.json](../../../../setup/parameters/general.json.md)