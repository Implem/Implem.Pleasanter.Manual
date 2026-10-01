---
title: エクスポート
category: エクスポート
order: '0'
status: ''
parts: ''
urlstring: table-management-export
translationKey: table-management-export
shortname: エクスポート,エクスポートの書式設定
created: 2019-12-05
updated: 2026-03-10
---

## 概要

[テーブルの管理](../index.md)画面の[エクスポート](../../../developers-guide/api/table-operations/api-export.md)タブでは、エクスポート時の書式を設定できます。

## 前提条件

1. エクスポートの書式設定には「サイトの管理権限」が必要です。
1. エクスポートの実行には「エクスポート権限」が必要です。

## 制限事項

1. 「標準」書式をユーザが編集することはできません。
1. 「標準」書式では「バージョン」項目はエクスポートされません。
1. 「標準」書式では「エクスポートする項目」が[非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)に設定されていても、エクスポートされます。

## エクスポートの書式一覧

[テーブルの管理](../index.md)画面の[エクスポート](../../../developers-guide/api/table-operations/api-export.md)タブには、作成・追加した書式の一覧が表示されます。

書式一覧は、最初、空の状態です。書式を追加すると一覧に書式が並びます。追加した書式をクリックすると、追加済みの書式を編集できます。

![テーブルの管理の「エクスポート」タブに並ぶ書式の一覧](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/assets/c4e9521be2a34adbb71972e3b0fb3ac7.png)

一覧の左端に表示されたチェックボックスで書式を選択することで、以下の操作を行えます。

|No|ボタン名|機能|
|:-:|:-:|:--|
|<span class="pl-callout">❶</span>|上|選択した書式を1つ上に移動します。|
|<span class="pl-callout">➋</span>|下|選択した書式を1つ下に移動します。|
|<span class="pl-callout">❸</span>|コピー|選択した書式を複製します。<br>複製された書式は一覧の一番下へ追加されます。|
|<span class="pl-callout">➍</span>|削除|選択した書式を一覧から削除します。<br>[削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)ボタンをクリックすると、確認ダイアログが表示されます。<br>「OK」ボタンをクリックすると、一覧から削除されます。|

#### 新規作成

「新規作成」ボタンをクリックすると、[エクスポート：全般](general/index.md)タブが表示されます。

#### 標準エクスポートを許可

エクスポートダイアログの「 書式」欄に、「標準」書式を表示させる・表示させないを切り替えます。

[エクスポート](../../../developers-guide/api/table-operations/api-export.md)ダイアログは、[一覧](../grid/index.md)画面を開き、コマンドボタンエリアの[エクスポート](../../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしたときに表示される画面です。

|「標準エクスポートを許可」が<br>有効の場合|「標準エクスポートを許可」が<br>無効の場合|
|:-:|:-:|
|![「標準エクスポートを許可」が有効のときのエクスポートダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/assets/e8b6c8603f7240cea41ece1e8831c7c9.png)|![「標準エクスポートを許可」が無効のときのエクスポートダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/assets/bbf06d1bb7d34aa7afb7336f3b34e7d7.png)|

「標準エクスポートを許可」を無効化した状態で、「標準」書式以外に当該ユーザがアクセス権を持つ書式が存在しない場合、コマンドボタンエリアの[エクスポート](../../../developers-guide/api/table-operations/api-export.md)ボタンは表示されません。

「標準エクスポートを許可」の既定値は設定ファイル[General.json](../../../setup/parameters/general.json.md)のパラメータAllowStandardExportで変更できます。

#### 標準エクスポート種別

バージョン1.5.2.0以降では、従来の「標準」書式に加え、2つの書式パターン（一覧、エディタ）を選択できます。

|標準エクスポート種別|エクスポートされる項目|
|:--|:--|
|既定|[一覧](../grid/index.md)画面または[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)画面の「現在の設定」の項目<br>（※バージョン1.5.1.0以前の「標準」書式と同じです）|
| 一覧|[一覧](../grid/index.md)画面の「現在の設定」の項目|
| エディタ|[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)画面の「現在の設定」の項目|

「標準エクスポート種別」の既定値は設定ファイル[General.json](../../../setup/parameters/general.json.md)のパラメータStandardExportTypeで変更できます。

## テーブルの管理：エクスポート：全般タブ

全般タブについては、[エクスポート：全般](general/index.md)を参照してください。

## テーブルの管理：エクスポート：アクセス制御タブ

アクセス制御タブについては、[エクスポート：アクセス制御](access-controls/index.md)を参照してください。

## 関連情報

-   [テーブルの管理](../index.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../../developers-guide/api/table-operations/api-export.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../editor/editor-settings/advanced-settings/general/table-management-hide.md)
-   [テーブル機能：レコードの削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)
-   [テーブルの管理：エクスポート：全般タブ](general/index.md)
-   [テーブルの管理：一覧画面](../grid/index.md)
-   [パラメータ設定：General.json](../../../setup/parameters/general.json.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エクスポート：アクセス制御タブ](access-controls/index.md)