---
title: レコードに添付ファイルをアップロード
category: テーブル機能
order: '901'
status: ''
parts: ''
urlstring: table-record-attachment-upload
translationKey: table-record-attachment-upload
shortname: 添付ファイル,05.レコード作成
created: 2019-04-30
updated: 2024-06-07
---

## 概要

テーブルのレコードに[添付ファイル](table-record-attachment-delete.md)を[アップロード](../../../../setup/additional/web-server/iis-large-file-100.md)し登録することができます。

## 制限事項

1. 大容量のファイルをアップロードする場合には事前の設定が必要な場合があります。関連情報を参照してください。
1. 添付ファイルの種類を制限する機能はございません。
1. テーブルのデフォルトの設定では、同じファイル名のファイルをアップロードすると、上書きされずに別ファイルとして追加されます。上書きを行いたい場合は、[同名ファイルを上書きする](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-overwrite-same-file-name.md)を設定してください。
1. 添付ファイルの項目の詳細設定で設定された[ファイル数制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-quantity.md)を超えてファイルをアップロードして更新しようとした場合「添付可能のファイル数は nn 件までです。」と表示され更新が行えません。nn には[ファイル数制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-quantity.md)の数値が表示されます。
1. 添付ファイルの項目の詳細設定で設定された[容量制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-size.md)を超えるファイルをアップロードして更新しようとした場合「制限容量 nn Mbyteを超えているファイルがあります。」と表示され更新が行えません。nn には[容量制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-size.md)の数値が表示されます。
1. 添付ファイルの項目の詳細設定で設定された[全容量制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-total-size.md)を超えてファイルをアップロードして更新しようとした場合「添付可能な容量は nn Mbyteまでです。」と表示され更新が行えません。nn には[全容量制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-total-size.md)の数値が表示されます。

## 前提条件

1. 「更新権限」が必要です。
1. [添付ファイル](table-record-attachment-delete.md)項目がエディタで有効化されている必要があります。
1. クラウドサービス [Pleasanter.net](https://pleasanter.net) では別途ストレージ容量のご契約が必要です。（専用環境の場合を除く）

## 操作手順

1. 対象のテーブルに移動してください。
1. [一覧画面](../data-analysis/table-grid.md)から対象のレコードを検索してください。
1. 対象のレコードをクリックしてください。
1. エクスプローラー等でファイルを選択し「ファイルをドラッグ＆ドロップしてください」のエリアにドロップしてください。複数のファイルを同時にアップロードできます。エリアをクリックした場合にはアップロードするファイルを選択するダイアログが表示されます。ダイアログからのファイル選択によっても同様にアップロードが可能です。
1. 添付ファイルがアップロードされたら「更新」をクリックしてください。

![ファイルをドラッグ＆ドロップして添付する領域があるエディタ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/9b368bd8cff242299c235ef508de6540.png)

## 関連情報

-   [テーブル機能：レコードの添付ファイルの削除](table-record-attachment-delete.md)
-   [IISで100MB以上のファイルをアップロードする場合の事前設定](../../../../setup/additional/web-server/iis-large-file-100.md)
-   [テーブルの管理：エディタ：項目の詳細設定：同名ファイルを上書きする](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-overwrite-same-file-name.md)
-   [テーブルの管理：エディタ：項目の詳細設定：ファイル数制限](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-quantity.md)
-   [テーブルの管理：エディタ：項目の詳細設定：容量制限(MB)](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-size.md)
-   [テーブルの管理：エディタ：項目の詳細設定：全容量制限(MB)](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-limit-total-size.md)
-   [Pleasanter.net](https://pleasanter.net)
-   [テーブル機能：レコードの一覧画面](../data-analysis/table-grid.md)