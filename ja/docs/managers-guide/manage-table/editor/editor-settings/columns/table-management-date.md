---
title: 日付
category: 項目
order: '1800'
status: ''
parts: ''
urlstring: table-management-date
translationKey: table-management-date
shortname: 日付項目
ee_notice: columns
created: 2020-06-30
updated: 2025-12-09
---

## 概要

[エディタ](../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)では「日付A」～「日付Z」の「日付項目」を使用できます。「日付項目」はフリーテキストまたはカレンダーから日付と時刻を入力可能な「入力項目」として使用できます。

## 制限事項

1. 「Community Edition」では「日付項目」を27個以上配置することはできません。
1. 「Pleasanter.net」では「日付項目」を27個以上配置することはできません。
1. 1900/1/1～2099/12/31 23:59:59の範囲外の日時は入力できません。
1. カレンダーから入力する場合1950年～2050年の範囲外の年は選択できません。
1. AzureのSQL Databaseを使用した環境では日時がUTCで保存されます。他のアプリケーションからデータベースに直接アクセスする場合にはJSTに変換してご使用いただく必要があります。
1. 第1世代ユーザインターフェースはバージョン1.4.18.0 で変更になった日時入力UIライブラリの対象外となり、UseOldDatepickerパラメータの変更も無効です。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![日付項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/a0051eed1a8942df8e3137c439449035.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|日付A～日付Z|[表示名](../advanced-settings/general/table-management-label-text.md)を設定します。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|スタイル|ノーマル|[入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)を設定します。|
|入力必須|無効|[入力必須](../advanced-settings/general/table-management-required.md)を設定します。|
|一括更新を許可|無効|[一括更新を許可](../advanced-settings/general/table-management-bulk-update.md)を設定します。|
|重複禁止|無効|[重複禁止](../advanced-settings/general/table-management-no-duplication.md)を設定します。|
|既定値でコピー|無効|[既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)を設定します。|
|読取専用|無効|[読取専用](../advanced-settings/general/table-management-readonly.md)を設定します。|
|エディタの書式|年月日|[エディタの書式](../advanced-settings/general/table-management-editor-format.md)を設定します。|
|既定値|(ブランク)|[既定値](../advanced-settings/general/table-management-default-input.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|入力ガイド|(ブランク)|[入力ガイド](../advanced-settings/general/table-management-input-guide.md)を設定します。|
|自動ポストバック|無効|[自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|無し|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

## 日時入力UIについて

バージョン1.4.18.0より、第2世代ユーザインターフェースのテーマ利用時の日時入力UIライブラリが変更になりました。

旧日時入力UIライブラリに戻したい場合は[general.json](https://pleasanter.org/ja/manual/general.json)のUseOldDatepickerをtrueにしてください。

|新ライブラリ| 旧ライブラリ|
|:---:|:---:|
| ![新しい日時入力UIライブラリの日付選択](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/766349b59175462da9e82e40ed8d76cc.png) | ![旧日時入力UIライブラリの日付選択](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/662a63236dc74350878206f3e5e9f874.png) |

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../advanced-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：一括更新を許可](../advanced-settings/general/table-management-bulk-update.md)
-   [テーブルの管理：エディタ：項目の詳細設定：重複禁止](../advanced-settings/general/table-management-no-duplication.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：エディタの書式](../advanced-settings/general/table-management-editor-format.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値](../advanced-settings/general/table-management-default-input.md)
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力ガイド](../advanced-settings/general/table-management-input-guide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)
-   [general.json](https://pleasanter.org/ja/manual/general.json)
-   [テーブルの管理：項目：分類](table-management-class.md)
-   [テーブルの管理：項目：数値](table-management-num.md)
-   [テーブルの管理：項目：チェック](table-management-check.md)
-   [テーブルの管理：項目：説明](table-management-description.md)
-   [Contact](https://implem.co.jp/contact)
