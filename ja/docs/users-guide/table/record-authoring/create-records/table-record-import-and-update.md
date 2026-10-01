---
title: レコードのインポートによる既存レコードの更新
category: テーブル機能
order: '203'
status: ''
parts: ''
urlstring: table-record-import-and-update
translationKey: table-record-import-and-update
shortname: インポート
created: 2020-03-03
updated: 2024-06-07
---

**バージョン1.3.11.2 以降では[インポート時のキー項目指定](table-record-import-key.md)を利用することができます。**

## 概要

CSVデータを[インポート](table-record-import.md)して既存データを更新する場合の方法と注意点を説明します。以下のようなCSVデータをインポートします。  

![インポートするCSVデータの例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/84f1faef5fe3465aa806995b6a71ffbf.png)  

![インポートしたレコードが登録された一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/2ec55385af8b4d81afdbfc2a363d69e8.png)

プリザンターに登録されたレコードには一意のIDが割り振られます。  

先ほどインポートしたデータをエクスポートしたデータが以下のCSVファイルとなります。  

![インポート後にエクスポートしたCSVファイル。IDが入っている](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/1e53131d60a14040bd49930f55dd4859.png)

以下の通りデータを追加、更新します。  緑色に塗ったセル3個所が更新行として扱われ下の桃色に塗った2行が新規追加となります。

![更新行を緑、新規追加行を桃色に塗り分けたCSVデータ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/ed24c6fe6b4249068435889629ca7e9e.png)

「IDが一致するレコードを更新する」をチェックして更新したCSVデータをインポートします。  

![「IDが一致するレコードを更新する」をチェックしたインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/58b4dec58c9f462abad97ac77d2942f9.png)

![更新と追加が反映された一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/6dd0e9f4b7ec4123ad01e7ca5870186b.png)

その後、更にもう1件追加したい、となった場合に先ほどインポートしたデータに新しく1行追加して「IDが一致するレコードを更新する」にチェックを入れてインポートすると以下のように重複してしまいます。  
![新しく1行追加したCSVデータ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/9d95457db71d499c9c7c7cf57500623d.png)

![レコードが重複して登録された一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/a243107828b54ba983ed248b7334cfe6.png)

[ID項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)が未入力のレコードは常に新規データとして扱われてしまいますので、既存データの更新と新規データの追加を同時に行うような場合は、既存データにプリザンターのレコードIDを追記しておくか、プリザンターからエクスポートしたデータをベースに編集・追加を行ってください。

## 関連情報

-   [テーブル機能：インポート時のキー項目指定](table-record-import-key.md)
-   [組織管理機能：インポート](../../../../managers-guide/department-administration/dept-import.md)
-   [テーブルの管理：項目：ID](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)