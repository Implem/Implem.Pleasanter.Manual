---
title: バージョン
category: 項目
order: '300'
status: ''
parts: ''
urlstring: table-management-ver
translationKey: table-management-ver
shortname: バージョン項目
created: 2021-05-05
updated: 2025-12-09
---

## 概要

「レコード」のバージョン番号を格納する項目です。バージョン番号はバージョンアップ時に1ずつ増加します。旧バージョンの内容は[変更履歴](../../../../../users-guide/table/record-authoring/edit-records/table-record-history-delete.md)から確認することができます。バージョンアップの動作を変更する場合には[自動バージョンアップ](../../automatic-version-upgrade/index.md)の設定を行ってください。

## 制限事項

1. 「バージョン項目」は[読取専用](../advanced-settings/general/table-management-readonly.md)です。変更可能にすることはできません。
1. 手動でバージョンを付与することはできません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![バージョン項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/9b84d890497e4dfeae1fbc6e96382533.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|バージョン|[表示名](../advanced-settings/general/table-management-label-text.md)は[読取専用](../advanced-settings/general/table-management-readonly.md)です。変更可能にすることはできません。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|スタイル|ノーマル|[入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|表示名|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

## 関連情報

-   [テーブル機能：レコードの変更履歴を削除](../../../../../users-guide/table/record-authoring/edit-records/table-record-history-delete.md)
-   [テーブルの管理：エディタ：自動バージョンアップ](../../automatic-version-upgrade/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../advanced-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)