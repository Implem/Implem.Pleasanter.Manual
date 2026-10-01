---
title: 管理者
category: 項目
order: '1200'
status: ''
parts: ''
urlstring: table-management-manager
translationKey: table-management-manager
shortname: 管理者項目
created: 2021-05-05
updated: 2025-12-09
---

## 概要

レコードの「管理者」を格納する入力項目です。[フィルタ](../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)で「自分」をチェックした際には、「ログインユーザ」が「管理者」または「担当者」になっているレコードを抽出します。

## 制限事項

1. [ユーザ](../advanced-settings/general/option-list/table-management-choices-text-users.md)を指定する[選択肢一覧](../advanced-settings/general/option-list/table-management-choices-text-depts.md)を設定する必要があります。[ユーザ](../advanced-settings/general/option-list/table-management-choices-text-users.md)以外の用途には使用できません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![管理者項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/d3a6c921d8314702b857b1417fb03cab.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|管理者|[表示名](../advanced-settings/general/table-management-label-text.md)を設定します。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|スタイル|ノーマル|[入力項目のスタイル](../advanced-settings/general/table-management-field-css.md)を設定します。|
|入力必須|無効|[入力必須](../advanced-settings/general/table-management-required.md)を設定します。|
|一括更新を許可|無効|[一括更新を許可](../advanced-settings/general/table-management-bulk-update.md)を設定します。|
|重複禁止|無効|[重複禁止](../advanced-settings/general/table-management-no-duplication.md)を設定します。|
|既定値でコピー|無効|[既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)を設定します。|
|読取専用|無効|[読取専用](../advanced-settings/general/table-management-readonly.md)を設定します。|
|既定値|[[Self]]|[既定値](../advanced-settings/general/table-management-default-input.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|選択肢一覧|[[Users]]|[選択肢一覧](../advanced-settings/general/option-list/table-management-choices-text-depts.md)を設定します。|
|コントロール種別|ドロップダウンリスト|[コントロール種別](../advanced-settings/general/table-management-control-type.md)を設定します。|
|検索機能を使う|無効|[検索機能を使う](../advanced-settings/general/table-management-use-search.md)を設定します。|
|選択肢にブランクを挿入しない|無効|[選択肢にブランクを挿入しない](../advanced-settings/general/table-management-not-insert-blank-choice.md)を設定します。|
|自動ポストバック|無効|[自動ポストバック](../advanced-settings/general/table-management-auto-postback.md)を設定します。|
|回り込みしない|無効|[回り込みしない](../advanced-settings/general/table-management-no-wrap.md)を設定します。|
|非表示|無効|[非表示](../advanced-settings/general/table-management-hide.md)を設定します。|
|フィールドCSS|(ブランク)|[フィールドCSS](../advanced-settings/general/table-management-extended-field-css.md)を設定します。|
|コントロールCSS|(ブランク)|[コントロールCSS](../advanced-settings/general/table-management-extended-control-css.md)を設定します。|
|フルテキストの種類|表示名|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

## 関連情報

-   [応用編：リンク](../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../advanced-settings/general/option-list/table-management-choices-text-users.md)
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