---
title: コメント
category: 項目
order: '2800'
status: ''
parts: ''
urlstring: table-management-comments
translationKey: table-management-comments
shortname: コメント項目,コメント
created: 2021-05-05
updated: 2025-12-09
---

## 概要

「レコード」の[コメント](../../../../../users-guide/common/comment.md)を格納する「入力項目」です。フリーテキストで文字列を入力できます。「コメント項目」には[マークダウン](../../../../../users-guide/common/markdown.md)を使用した入力や[画像](../../../../../users-guide/table/record-authoring/edit-records/table-record-upload-picture.md)の登録が可能です。既定ではコメントの編集は行えません。コメントの編集を許可するには[コメントの編集を許可](../../allow-editing-comments/index.md)の設定を行ってください。

## 制限事項

1. 「コメント項目」は画像を除く2GBまでの文字列を登録可能ですが、実際にはWebサーバのリクエストサイズの上限などにより2GBの文字を登録することはできません。
1. 「コメント項目」の[エディタ](../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)上の配置は変更できません。画面右に表示されます。
1. 「ダイアログ編集」および[一覧編集](../../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)ではコメントを追加できません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 詳細設定

詳細設定については[入力項目の詳細設定](../advanced-settings/index.md)を参照してください。

![コメント項目の詳細設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/columns/assets/0dd7440b947e48f494c5c683b61f6aa0.png)

|設定項目名|初期値|説明|
|---|---|---|
|表示名|コメント|[表示名](../advanced-settings/general/table-management-label-text.md)を設定します。|
|配置|左寄せ|[配置](../advanced-settings/general/table-management-textalign.md)を設定します。|
|最大文字数|(ブランク)|[最大文字数](../advanced-settings/general/table-management-maxlength.md)を設定します。|
|既定値でコピー|無効|[既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)を設定します。|
|読取専用|無効|[読取専用](../advanced-settings/general/table-management-readonly.md)を設定します。|
|画像の登録を許可|有効|[画像の登録を許可](../advanced-settings/general/table-management-allow-adding-img.md)を設定します。|
|サムネイルサイズ|(ブランク)|[サムネイルサイズ](../advanced-settings/general/table-management-thumbnail.md)を設定します。|
|説明|(ブランク)|項目の[ツールチップ](../../../../../users-guide/common/user-tooltip.md)に表示する文字列（[説明](../advanced-settings/general/table-management-column-description.md)）を設定します。|
|入力ガイド|(ブランク)|[入力ガイド](../advanced-settings/general/table-management-input-guide.md)を設定します。|
|フルテキストの種類|表示名|[フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)を設定します。|

## コメントの追加・更新・削除

1. コメントの追加はレコードに対する「更新権限」が必要です。
1. コメントの編集は[コメントの編集を許可](../../allow-editing-comments/index.md)の設定が必要です。編集できるコメントは自分自身が登録したコメントのみです。他ユーザが登録したコメントは編集できません。
1. コメントの削除はレコードに対する「更新権限」が必要です。なお、更新権限をもつユーザは自分自身が登録したコメントだけでなく、他ユーザが登録したコメントも削除できます。

## 関連情報

-   [共通機能：コメントを追加](../../../../../users-guide/common/comment.md)
-   [共通機能：マークダウン](../../../../../users-guide/common/markdown.md)
-   [テーブル機能：レコードに画像を登録](../../../../../users-guide/table/record-authoring/edit-records/table-record-upload-picture.md)
-   [テーブルの管理：エディタ：コメントの編集を許可](../../allow-editing-comments/index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブル機能：レコードの一覧編集](../../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../advanced-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：最大文字数](../advanced-settings/general/table-management-maxlength.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値でコピー](../advanced-settings/general/table-management-copy-by-default.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：画像の登録を許可](../advanced-settings/general/table-management-allow-adding-img.md)
-   [テーブルの管理：エディタ：項目の詳細設定：サムネイルサイズ](../advanced-settings/general/table-management-thumbnail.md)
-   [共通機能：ユーザ、組織選択時のツールチップ表示](../../../../../users-guide/common/user-tooltip.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../advanced-settings/general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力ガイド](../advanced-settings/general/table-management-input-guide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../advanced-settings/general/table-management-full-text-type.md)