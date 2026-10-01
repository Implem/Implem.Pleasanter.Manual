---
title: レコードのインポート
category: 操作ガイド（基本編）
order: '60'
status: ''
parts: ''
urlstring: basic-operations-import
translationKey: basic-operations-import
shortname: ''
created: 2019-08-31
updated: 2024-04-09
---

[<< 操作ガイド目次に戻る](basic-operations.md)

## レコードの一括追加

CSVインポート・エクスポート機能を使用して、レコードを一括で追加・更新します。

## 事前準備

レコードを一括で追加・更新するには、テーブルが必要になります。
まだ作成していない場合は[テーブル作成](basic-operations-table.md)を参考に作成してください。

## マニュアル

1.  対象テーブルへ移動し、画面下部の[エクスポート](../../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしてください。  

    ![一覧画面下部の「エクスポート」ボタン](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/4065fde330244fc6a05c44c0497dd1ef.png)

1.  ダイアログで[書式](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-format.md)を選択し、[エクスポート](../../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしてください。  

    ![書式を選ぶエクスポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/37d6e4847fea48489309e6adedf9ef69.png)

1.  ファイルがダウンロードされたことを確認します。（ダウンロードファイルの確認方法はご利用のブラウザによって異なります）  

    ![CSVファイルがダウンロードされたことを示すブラウザの表示](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/3df86eb1ace14daebed5c6b6c8314a9c.png)

1.  エクスポートしたファイルへ追加するレコードを追記し、保存します。

    ![レコードを追記したエクスポート済みCSVファイルの中身](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/cd574ee26d4b4a07af3ed8afb9e3314b.png)

1.  画面下部にある[インポート](../../table/record-authoring/create-records/table-record-import.md)ボタンをクリックしてください。  

    ![一覧画面下部の「インポート」ボタン](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/19ac1db6ba5847b8a7b04db9b627fed3.png)

1.  ダイアログで「CSVファイル」、「文字コード」を設定、「IDが一致するレコードを更新する」のチェックボックスをオンにし、[インポート](../../table/record-authoring/create-records/table-record-import.md)ボタンをクリックしてください。  

    ![CSVファイルと文字コードを指定するインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/bac4b09c69f74b7281e4951ed264cc36.png)

1.  メッセージを確認できたら完了です。

    ![インポート完了のメッセージが表示された画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/basics/assets/1278fb53cddc4ef39fcab341443ad64f.png)

!!! warning "Pleasanter.netにおけるレコードインポート数の上限"
    Pleasanter.netでは一度のインポート処理で取り込めるレコード数が10,000行となっています。10,000行を超える量のデータをインポートする場合は、10,000行ごとに区切ってインポートしてください。

レコードの一括更新に関する詳細は下記を参照してください。

-   [基本操作ガイド 目次](basic-operations.md)
-   [テーブル作成](basic-operations-table.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../../developers-guide/api/table-operations/api-export.md)
-   [テーブルの管理：エディタ：項目の詳細設定：書式](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-format.md)
-   [組織管理機能：インポート](../../../managers-guide/department-administration/dept-import.md)

[<< 操作ガイド目次に戻る](basic-operations.md)
