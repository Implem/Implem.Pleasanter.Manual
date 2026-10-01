---
title: インポート時のキー項目指定
category: テーブル機能
order: '202'
status: ''
parts: ''
urlstring: table-record-import-key
translationKey: table-record-import-key
shortname: インポート時のキー項目指定
created: 2022-07-28
updated: 2025-03-13
---

## 概要

キー項目を指定することで、テーブル内の既にあるレコードとCSVファイル内のレコード行とを対応させてインポートすることができます。

## 前提条件

事前にテーブルの管理で[インポートのキー](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-import-key.md)を指定する必要があります。

## 制限事項

1. [説明項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[タイトル項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)、[内容項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[分類項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)の各項目に対して設定可能です。
1. CSVの項目名とプリザンターの項目名を一致させる必要があります。[レコードのインポートがうまくいかない場合の確認事項](table-record-import-fail.md)を確認ください。
1. ユーザテーブル、組織テーブル、グループテーブルには利用できません。
1. 本機能で ID 以外のキーによって多量のデータを取り込む場合、処理に長い時間を要し、期待する応答性能とならない可能性がございます。多量のデータを取り込む場合には ID をキーとする取り込みをご検討ください。ご利用の RDBMS によってはキーとする項目にインデクスを設定することによって、性能改善できる可能性もございます。

## 注意事項

インポートのキーに重複があると、インポート時にエラーとなります。そのため、インポートのキーに指定する項目には、あわせて[重複禁止](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-no-duplication.md)設定することを推奨します。

## 説明

既存のテーブルの項目をキー項目に指定してインポートすることで、テーブル内のレコードとインポートするCSVの行を対応付けてインポートすることができます。

例えば、顧客テーブルに"顧客番号"項目がある場合にキー項目として"顧客番号"項目を指定してインポートすることで、 既存の顧客テーブル内の"顧客番号"項目とCSVファイル内の"顧客番号"が一致する場合に、そのCSVのレコード行の内容を反映して顧客テーブルの該当レコードが更新されます。CSVファイル内の"顧客番号"が顧客テーブルの"顧客番号"項目に存在しない場合は、新規レコードとして追加されます。

## 操作方法

インポートのダイアログで下図のように"キーが一致するレコード"をチェックし、"キー"プルダウンで所望のキー項目を選択してからインポートを実行します。
![「キーが一致するレコード」とキーを指定するインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/bf7f96b133134596bc2b127ab4d81e4b.png)

インポート操作について詳しくは「[テーブル機能：レコードのインポート](table-record-import.md)」を参照ください。

キー項目の既定値を設定することが可能です。 [テーブルの管理：インポート](../../../../managers-guide/manage-table/import/index.md)"を参照ください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.11.2 以降|機能追加|

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：インポートのキー](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-import-key.md)
-   [テーブルの管理：項目：説明](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：タイトル](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)
-   [テーブルの管理：項目：内容](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブル機能：レコードのインポートがうまくいかない場合の確認事項](table-record-import-fail.md)
-   [テーブルの管理：エディタ：項目の詳細設定：重複禁止](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-no-duplication.md)
-   [テーブルの管理：インポート](../../../../managers-guide/manage-table/import/index.md)