---
title: 作業量
category: 項目
order: '800'
status: ''
parts: ''
urlstring: table-management-work-value
translationKey: table-management-work-value
shortname: 作業量項目
created: 2021-05-05
updated: 2025-12-09
---

## 概要

「レコード」の「作業量」を格納する「入力項目」です。[バーンダウンチャート](../../../../../users-guide/table/record-authoring/data-visualize/table-burndown-chart.md)の「縦軸」に使用されます。標準の単位は「h」となっていますが、他の単位に変更して使用することができます。

## 制限事項

1. 「期限付きテーブル」でのみ使用可能です。  
1. 「最大」に設定可能な最大値は「2,147,483,647」です。最大値を超える値を設定するとエラーになります。  
1. 「最小」に設定可能な最小値は「-2,147,483,647」です。最低値未満の値を設定するとエラーになります。  

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![作業量項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/7b4d37c41edb43cf8fed38ef20408362.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|作業量|[表示名](../advanced-settings/general/table-management-label-text.md)を設定します。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|スタイル|ノーマル|[入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)を設定します。|
|入力必須|無効|[入力必須](../advanced-settings/general/table-management-required.md)を設定します。|
|一括更新を許可|無効|[一括更新を許可](../advanced-settings/general/table-management-bulk-update.md)を設定します。|
|重複禁止|無効|[重複禁止](../advanced-settings/general/table-management-no-duplication.md)を設定します。|
|既定値でコピー|無効|[既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)を設定します。|
|読取専用|無効|[読取専用](../advanced-settings/general/table-management-readonly.md)を設定します。|
|既定値|(ブランク)|[既定値](../advanced-settings/general/table-management-default-input.md)を設定します。|
|書式|標準|[書式](../advanced-settings/general/table-management-format.md)を設定します。|
|単位|h|[単位](../advanced-settings/general/table-management-unit.md)を設定します。|
|小数点以下桁数|1|[小数点以下桁数](../advanced-settings/general/table-management-decimal-places.md)を設定します。|
|端数処理種類|四捨五入|[端数処理種類](../advanced-settings/general/table-management-rounding-type.md)を設定します。|
|コントロール種別|スピナー|[コントロール種別](../advanced-settings/general/table-management-control-type.md)を設定します。|
|最小|0|[最小](../advanced-settings/general/table-management-min-and-max.md)の数値を設定します。|
|最大|100|[最大](../advanced-settings/general/table-management-min-and-max.md)の数値を設定します。|
|ステップ|0.1|[ステップ数](../advanced-settings/general/table-management-min-and-max.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|自動ポストバック|無効|[自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|無し|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

## 関連情報

-   [テーブル機能：レコードのバーンダウンチャート表示](../../../../../users-guide/table/record-authoring/data-visualize/table-burndown-chart.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../advanced-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：一括更新を許可](../advanced-settings/general/table-management-bulk-update.md)
-   [テーブルの管理：エディタ：項目の詳細設定：重複禁止](../advanced-settings/general/table-management-no-duplication.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値](../advanced-settings/general/table-management-default-input.md)
-   [テーブルの管理：エディタ：項目の詳細設定：書式](../advanced-settings/general/table-management-format.md)
-   [テーブルの管理：エディタ：項目の詳細設定：単位](../advanced-settings/general/table-management-unit.md)
-   [テーブルの管理：エディタ：項目の詳細設定：小数点以下桁数](../advanced-settings/general/table-management-decimal-places.md)
-   [テーブルの管理：エディタ：項目の詳細設定：端数処理種類](../advanced-settings/general/table-management-rounding-type.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロール種別(数値)](../advanced-settings/general/table-management-control-type.md)
-   [テーブルの管理：エディタ：項目の詳細設定：最小、最大、ステップ](../advanced-settings/general/table-management-min-and-max.md)
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)