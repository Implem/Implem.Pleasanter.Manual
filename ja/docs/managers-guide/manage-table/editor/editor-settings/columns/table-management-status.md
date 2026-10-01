---
title: 状況
category: 項目
order: '1100'
status: ''
parts: ''
urlstring: table-management-status
translationKey: table-management-status
shortname: 状況項目,状況
created: 2021-05-05
updated: 2025-12-09
---

## 概要

レコードの状況（ステータス）を格納する入力項目です。「状況項目」の入力値によって、レコードが「完了」か「未完了」かを判定することができます。

## 制限事項

1. 「値」が数値の[選択肢一覧](../advanced-settings/general/option-list/table-management-choices-text-depts.md)を設定する必要があります。  
1.  新しいスタイルを作成する場合、スタイルのクラス名は"status-"で始まる必要があります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![状況項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/955b7a6e4ac64349b1e43c3fb0d7ac0a.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|状況|[表示名](../advanced-settings/general/table-management-label-text.md)を設定します。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|スタイル|ノーマル|[入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)を設定します。|
|入力必須|有効|[入力必須](../advanced-settings/general/table-management-required.md)を設定します。|
|一括更新を許可|無効|[一括更新を許可](../advanced-settings/general/table-management-bulk-update.md)を設定します。|
|重複禁止|無効|[重複禁止](../advanced-settings/general/table-management-no-duplication.md)を設定します。|
|既定値でコピー|無効|[既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)を設定します。|
|読取専用|無効|[読取専用](../advanced-settings/general/table-management-readonly.md)を設定します。|
|既定値|100|[既定値](../advanced-settings/general/table-management-default-input.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|選択肢一覧|※[下記参照](#selection-list)|[選択肢一覧](../advanced-settings/general/option-list/table-management-choices-text-depts.md)を設定します。|
|コントロール種別|ドロップダウンリスト|[コントロール種別](../advanced-settings/general/table-management-control-type.md)を設定します。|
|検索機能を使う|無効|[検索機能を使う](../advanced-settings/general/table-management-use-search.md)を設定します。|
|選択肢にブランクを挿入しない|無効|[選択肢にブランクを挿入しない](../advanced-settings/general/table-management-not-insert-blank-choice.md)を設定します。|
|自動ポストバック|無効|[自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|表示名|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

<a id="selection-list"></a>

### 選択肢一覧の既定値

「状況項目」の[選択肢一覧](../advanced-settings/general/option-list/table-management-choices-text-depts.md)の既定値は下記のとおりです。[選択肢一覧](../advanced-settings/general/option-list/table-management-choices-text-depts.md)は追加、変更、削除が可能です。業務に合わせて適宜変更してください。「値」が 900 以上のものは「完了」として扱われ、 900 未満のものは「未完了」として扱われます。新しい[スタイル](../../../../../developers-guide/style/index.md)を作成することも可能です。

|No|値|表示名|短縮名|スタイル|
|:----|:----|:----|:----|:----|
|1|100|未着手|未|status-new|
|2|150|準備|準|status-preparation|
|3|200|実施中|実|status-inprogress|
|4|300|レビュー|レ|status-review|
|5|900|完了|完|status-closed|
|6|910|保留|留|status-rejected|

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../advanced-settings/general/option-list/table-management-choices-text-depts.md)
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
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロール種別(数値)](../advanced-settings/general/table-management-control-type.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../advanced-settings/general/table-management-use-search.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢にブランクを挿入しない](../advanced-settings/general/table-management-not-insert-blank-choice.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)
-   [開発者ガイド：スタイル](../../../../../developers-guide/style/index.md)