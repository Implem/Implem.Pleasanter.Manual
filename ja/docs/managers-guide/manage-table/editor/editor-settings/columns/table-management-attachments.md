---
title: 添付ファイル
category: 項目
order: '2100'
status: ''
parts: ''
urlstring: table-management-attachments
translationKey: table-management-attachments
shortname: 添付ファイル項目
ee_notice: columns
created: 2020-06-30
updated: 2025-12-09
---

## 概要

[エディタ](../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)では「添付ファイルA」～「添付ファイルZ」の「添付ファイル項目」を使用できます。「添付ファイル項目」は[添付ファイル](../../../../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)をアップロード/ダウンロード可能な「入力項目」として使用できます。

## 制限事項

1. 「Community Edition」では「添付ファイル項目」を27個以上配置することはできません。
1. 「Pleasanter.net」では「添付ファイル項目」を27個以上配置することはできません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

### [BinaryStorage.json](../../../../../setup/parameters/binary-storage-json.md)のUseStorageSelectがfalse（既定の状態）

![UseStorageSelect が false のときの添付ファイル項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/b3d7a479697440d9a485f1ca212bed53.png)

|設定項目名|初期値|説明|
|:---|:---|:---|
|表示名|添付ファイルA～添付ファイルZ|[表示名](../advanced-settings/general/table-management-label-text.md)を設定します。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|入力必須|無効|[入力必須](../advanced-settings/general/table-management-required.md)を設定します。|
|読取専用|無効|[読取専用](../advanced-settings/general/table-management-readonly.md)を設定します。|
|添付ファイルの削除を許可|有効|[添付ファイルの削除を許可](../advanced-settings/general/table-management-allow-delete-attachments.md)を設定します。|
|履歴に存在するファイルは削除しない|無効|[履歴に存在するファイルは削除しない](../advanced-settings/general/table-management-not-delete-file-with-history.md)を設定します。|
|同名ファイルを上書きする|無効|[同名ファイルを上書きする](../advanced-settings/general/table-management-overwrite-same-file-name.md)を設定します。|
|ファイル数制限|30|[ファイル数制限](../advanced-settings/general/table-management-limit-quantity.md)を設定します。|
|容量制限(MB)|50|[容量制限](../advanced-settings/general/table-management-limit-size.md)を設定します。該当「添付ファイル項目」の[格納先](../advanced-settings/general/table-management-binary-storage-provider.md)が「データベース」または「自動 (データベースまたはローカルフォルダ)」の場合に表示されます。|
|全容量制限(MB)|1024|[全容量制限](../advanced-settings/general/table-management-limit-total-size.md)を設定します。該当「添付ファイル項目」の[格納先](../advanced-settings/general/table-management-binary-storage-provider.md)が「データベース」または「自動 (データベースまたはローカルフォルダ)」の場合に表示されます。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|入力ガイド|(ブランク)|[入力ガイド](../advanced-settings/general/table-management-input-guide.md)を設定します。値を設定した場合、ファイル添付領域の「ファイルをドラッグ＆ドロップしてください」の箇所に設定した値が表示されます。|
|自動ポストバック|無効|[自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|表示名|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

[BinaryStorage.json](../../../../../setup/parameters/binary-storage-json.md)の「UseStorageSelect」をtrueに設定することで、[格納先](../advanced-settings/general/table-management-binary-storage-provider.md)を設定できるようになります。

### [BinaryStorage.json](../../../../../setup/parameters/binary-storage-json.md)のUseStorageSelectがtrue<br>かつ<span style="color:blue;">格納先で「データベース」を選択</span>

![格納先に「データベース」を選んだときの添付ファイル項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/686083e9a0f84b87ada8b66ea1abdd01.png)

|設定項目名|初期値|説明|
|:---|:---|:---|
|容量制限(MB)|50|[容量制限](../advanced-settings/general/table-management-limit-size.md)を設定します。|
|全容量制限(MB)|1024|[全容量制限](../advanced-settings/general/table-management-limit-total-size.md)を設定します。|

### [BinaryStorage.json](../../../../../setup/parameters/binary-storage-json.md)のUseStorageSelectがtrue<br>かつ<span style="color:blue;">格納先で「ローカルフォルダ」を選択</span>

![格納先に「ローカルフォルダ」を選んだときの添付ファイル項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/1a707632eae149929a9f5e0ac8ad13a7.png)

|設定項目名|初期値|説明|
|:---|:---|:---|
|ローカルフォルダ容量制限(MB)|3072|[ローカルフォルダ容量制限](../advanced-settings/general/table-management-local-folder-limit-size.md)を設定します。|
|ローカルフォルダ全容量制限(MB)|30720|[ローカルフォルダ全容量制限](../advanced-settings/general/table-management-local-folder-limit-total-size.md)を設定します。|

### [BinaryStorage.json](../../../../../setup/parameters/binary-storage-json.md)のUseStorageSelectがtrue<br>かつ<span style="color:blue;">格納先で「自動 (データベースまたはローカルフォルダ)」を選択</span>

![格納先に「自動」を選んだときの添付ファイル項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/35aae63683d14e49a14735db668b6fcd.png)

|設定項目名|初期値|説明|
|:---|:---|:---|
|容量制限(MB)|50|[容量制限](../advanced-settings/general/table-management-limit-size.md)を設定します。|
|全容量制限(MB)|1024|[全容量制限](../advanced-settings/general/table-management-limit-total-size.md)を設定します。|
|ローカルフォルダ容量制限(MB)|3072|[ローカルフォルダ容量制限](../advanced-settings/general/table-management-local-folder-limit-size.md)を設定します。|

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブル機能：レコードの添付ファイルの削除](../../../../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../advanced-settings/index.md)
-   [パラメータ設定：BinaryStorage.json](../../../../../setup/parameters/binary-storage-json.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：添付ファイルの削除を許可](../advanced-settings/general/table-management-allow-delete-attachments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：履歴に存在するファイルは削除しない](../advanced-settings/general/table-management-not-delete-file-with-history.md)
-   [テーブルの管理：エディタ：項目の詳細設定：同名ファイルを上書きする](../advanced-settings/general/table-management-overwrite-same-file-name.md)
-   [テーブルの管理：エディタ：項目の詳細設定：ファイル数制限](../advanced-settings/general/table-management-limit-quantity.md)
-   [テーブルの管理：エディタ：項目の詳細設定：容量制限(MB)](../advanced-settings/general/table-management-limit-size.md)
-   [テーブルの管理：エディタ：項目の詳細設定：格納先](../advanced-settings/general/table-management-binary-storage-provider.md)
-   [テーブルの管理：エディタ：項目の詳細設定：全容量制限(MB)](../advanced-settings/general/table-management-limit-total-size.md)
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力ガイド](../advanced-settings/general/table-management-input-guide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)
-   [テーブルの管理：エディタ：項目の詳細設定：ローカルフォルダ容量制限(MB)](../advanced-settings/general/table-management-local-folder-limit-size.md)
-   [テーブルの管理：エディタ：項目の詳細設定：ローカルフォルダ全容量制限(MB)](../advanced-settings/general/table-management-local-folder-limit-total-size.md)
-   [テーブルの管理：項目：分類](table-management-class.md)
-   [テーブルの管理：項目：数値](table-management-num.md)
-   [テーブルの管理：項目：日付](table-management-date.md)
-   [テーブルの管理：項目：チェック](table-management-check.md)
-   [テーブルの管理：項目：説明](table-management-description.md)
-   [Contact](https://implem.co.jp/contact)
