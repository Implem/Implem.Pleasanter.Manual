---
title: ID
category: 項目
order: '200'
status: ''
parts: ''
urlstring: table-management-id
translationKey: table-management-id
shortname: ID項目
created: 2021-05-05
updated: 2025-12-09
---

## 概要

「レコード」の一意なIDを格納する項目です。IDは自動的に数字の連番が割り当てられます。IDはレコードのURLの一部として使用されます。

## 制限事項

1. 「ID項目」は[読取専用](../advanced-settings/general/table-management-readonly.md)です。変更可能にすることはできません。
1. 一度使用したIDは削除しても再利用できません。
1. 手動でIDを付与することはできません。
1. IDに数字以外のアルファベットや記号を含めることはできません。
1. IDのフォーマットをカスタマイズすることはできません。
1. IDの桁数を制御することはできません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![ID項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/3d3669fd65d546c888f5fd9ba2263f5a.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|ID|[表示名](../advanced-settings/general/table-management-label-text.md)は[読取専用](../advanced-settings/general/table-management-readonly.md)です。変更可能にすることはできません。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|スタイル|ノーマル|[入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)を設定します。|
|インポートのキー|有効|[インポートのキー](../advanced-settings/general/table-management-import-key.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|表示名|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../advanced-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：インポートのキー](../advanced-settings/general/table-management-import-key.md)
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)