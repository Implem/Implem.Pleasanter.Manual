---
title: バッチ処理でCSVファイルを読み込んで対象のレコードを作成または更新したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-csv-import-powershell
translationKey: faq-csv-import-powershell
shortname: ''
created: 2021-09-09
updated: 2025-12-23
---

## 回答

[レコードのインポートAPI](../../developers-guide/api/table-operations/api-import.md)を使用します。

---

## 概要

バッチ処理でCSVファイルを読み込んで対象のレコードを作成または更新したい場合は、[レコードのインポートAPI](../../developers-guide/api/table-operations/api-import.md)を使用します。

例として下表のCSVファイルから読み込んだ項目を、プリザンターの項目に挿入します。id(ClassA)の値が既にプリザンター上に存在している場合は上書き更新されます。idのチェックを行うためClassAの[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)は完全一致に設定する必要があります。インポートするCSVデータはスクリプトファイルと同じフォルダに保存してください。

|CSV項目|プリザンター項目|
|:--:|:--:|
|name|Title|
|id|ClassA|
|mail|ClassE|

## 操作手順

1. プリザンターを開き、テーブルを作成してください
1. [テーブルの管理](../../managers-guide/manage-table/index.md)を開き、[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)タブで分類Aと分類Eを有効化してください。
1. [フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)タブを開き、分類Aを選択してから詳細設定ボタンをクリックし、[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)を完全一致に変更のうえ、変更ボタンをクリックしてください。
1. 更新ボタンをクリックしてください。
1. 戻るボタンで一覧画面に戻ってください。
1. ユーザメニューから「API設定」でAPIキーを作成し、キーをコピーしてください。
1. 対象となるテーブルのサイトIDをメモしてください。
1. 以下のCSVファイル例をコピーして、data.csvという名前でファイルを保存してください。
1. 以下のサンプルコードをコピーして、import.ps1という名前でファイルを保存してください。
1. CSVファイルの文字コードに合わせて、import.ps1の8行目を修正してください。
1. import.ps1の1,2行目にあるサイトIDとAPIキーの箇所を変更して保存してください。  
1. import.ps1を実行してください。

### CSVファイルの作成(data.csv)

````
id,name,mail
1,user1,user1@example.com
2,user2,user2@example.com
3,user3,user3@example.com
4,user4,user4@example.com
5,user5,user5@example.com
6,user6,user6@example.com
7,user7,user7@example.com
8,user8,user8@example.com
9,user9,user9@example.com
10,user10,user10@example.com
````

## サンプルコード

##### PowerShell

````
$url = 'http://localhost/api/items/xxxサイトIDxxx/import'
$apiKey = 'xxxAPIキーxxx'
$filePath = "./data.csv"
$form = @{
    parameters = ConvertTo-Json @{
        ApiVersion = 1.1;
        ApiKey = $apiKey;
        Encoding = "UTF-8";
        UpdatableImport = $true;
        Key = "ClassA";
    };
    file = Get-Item -Path $filePath;
}
Invoke-WebRequest -Uri $url -Method Post -Form $form
````

## 関連情報

-   [開発者ガイド：API：テーブル操作：レコードのインポート](../../developers-guide/api/table-operations/api-import.md)
-   [テーブルの管理：フィルタ：検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)