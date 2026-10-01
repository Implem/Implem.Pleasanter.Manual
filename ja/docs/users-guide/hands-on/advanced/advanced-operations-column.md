---
title: 項目の種類
category: 操作ガイド（応用編）
order: '10'
status: ''
parts: ''
urlstring: advanced-operations-column
translationKey: advanced-operations-column
shortname: 項目の種類
created: 2023-08-07
updated: 2026-08-12
---

## 概要

[テーブル](../../table/index.md)のデータを格納するデータ項目のうち、既定で設定済みの項目の他に[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)を[エディタ](../../table/record-authoring/edit-records/table-editor.md)で自由に配置することができます。

## 分類

フリーテキスト入力および選択肢入力項目として利用します。最大文字数は1024文字です。選択肢入力として利用する場合はドロップダウンリスト形式かラジオボタン形式のどちらかを選択可能です。また選択肢をJSON形式で設定することでフィルタ、ソート、[表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)の設定や[ルックアップ](advanced-operations-link.md)による自動転記が利用できます。[自動採番](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/auto-numbering/index.md)機能を利用して指定フォーマットでの自動採番を行うことができます。

### 表示イメージ

![エディタ上の分類項目の表示イメージ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/f4beda6bd10c4b6887fef2e40790a0e6.png)

## 数値

数値を入力する項目として利用します。フリーテキストの他、上下ボタンで数値変更が可能となる「スピナー」を選択可能です。

### 未入力時の扱い

既定の設定では0が自動登録され、画面表示上も0と表示しますが、[NULL許容](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-nullable.md)チェックONすることでNULLでの登録が可能となります。

### 表示イメージ

![エディタ上の数値項目の表示イメージ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/4d766043e41c46f78fe7a6b701a032d2.png)

## 日付

フリーテキストまたはカレンダーから日付と時刻を入力する項目として利用します。

### 時刻について

エディタの書式で「年月日」を選択した場合、編集画面からの登録更新時は自動的に「00:00:00」として登録します。ただしAPIやサーバスクリプトでの登録更新で意図的に時刻を指定した際はその指定した内容で登録します。

### 表示イメージ

![エディタ上の日付項目の表示イメージ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/d604208fa8114cef8ff2311d5a94ec45.png)

## チェック

チェックボックスとして利用します。チェックONまたはチェックOFFの2つの状態をもちます。

### 表示イメージ

![エディタ上のチェック項目の表示イメージ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/aaef842235784c8dba0fc520dfb12587.png)

## 説明

フリーテキストで文字列を入力する項目として利用します。[マークダウン](../../common/markdown.md)または[リッチテキストエディタ](../../common/richtexteditor.md)を利用した入力や[画像](../../table/record-authoring/edit-records/table-record-upload-picture.md)の登録が可能です。

### 分類項目との違い

分類項目との違いは下記の通りです。ご要件に合わせて使い分けてください。

|項目|分類項目|説明項目|
|:---|:---|:---|
|最大文字数|1024文字|実質無制限|
|設定可能なスタイル|ノーマル<br>ワイド|ノーマル<br>ワイド<br>マークダウン<br>リッチテキストエディタ|
|選択肢項目として利用|可|不可|
|自動採番|利用可|利用可|

#### 表示イメージ

![エディタ上の説明項目の表示イメージ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/67e7ea9f3e884d69a18f01db3d687fc7.png)

## 添付ファイル

各種ファイルを添付する項目として利用します。添付可能なファイル数、ファイルサイズを指定できます。ファイル種類の制限はありません。[添付ファイル](../../table/record-authoring/edit-records/table-record-attachment-delete.md)がブラウザで表示可能な場合、虫眼鏡アイコンをクリックすると別タブでプレビュー表示します。画面上に画像を表示したい場合は[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)ではなく[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)を利用してください。

### 表示イメージ

![エディタ上の添付ファイル項目の表示イメージ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/19274f2ae48246e6800052baf8f1c4da.png)

## 関連情報

-   [応用編：リンク](advanced-operations-link.md)
-   [テーブル機能](../../table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [共通機能：マークダウン](../../common/markdown.md)
-   [共通機能：リッチテキストエディタ](../../common/richtexteditor.md)
-   [テーブル機能：レコードに画像を登録](../../table/record-authoring/edit-records/table-record-upload-picture.md)
-   [テーブル機能：レコードの添付ファイルの削除](../../table/record-authoring/edit-records/table-record-attachment-delete.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動採番](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/auto-numbering/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：NULL許容](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-nullable.md)
