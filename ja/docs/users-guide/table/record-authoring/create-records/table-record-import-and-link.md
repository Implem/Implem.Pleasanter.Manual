---
title: レコードのインポートとマスタデータのリンク
category: テーブル機能
order: '202'
status: ''
parts: ''
urlstring: table-record-import-and-link
translationKey: table-record-import-and-link
shortname: インポート,リンク
created: 2020-02-26
updated: 2024-12-19
---

## 概要

こちらのページは、インポートの基本的方法「[テーブル機能：レコードのインポート](table-record-import.md)」を理解していただいていることを前提に記載しています。先に以下を参照して、インポートの基本的な使い方を理解しておいてください。このページでは、親テーブルと子テーブルをリンクして使う場合のインポート方法を解説します。例として、顧客管理(親テーブル)と商談管理(子テーブル)とで、共通の顧客CDを使用しリンクさせて扱うものとします。大まかな流れとしては、下記の手順となります。  

1. 「顧客管理」、「商談管理」のエクセルデータを開き「名前を付けて保存」を選択し、ファイル形式で「CSV(コンマ区切り)(.csv)」または「CSV UTF-８（コンマ区切り)(.csv)」を選択して保存してください。
1. 「顧客管理」、「商談管理」記録テーブルの作成と、データ項目の作成
1. 「顧客管理」テーブルのタイトル設定
1. 「顧客管理」テーブルを親、「商談管理」テーブルを子としたリンクの設定
1. 「顧客管理」のCSVデータのインポート
1. 「商談管理」へのCSVデータのインポート 

## 前提条件

1. テーブルの[リンク](../../../hands-on/advanced/advanced-operations-link.md)設定はインポートの前に行っておく  
1. 子テーブルにリンクされた親テーブルの項目名は子テーブルで設定された項目名でインポートする

---

顧客管理(親テーブル)
![顧客管理（親テーブル）のエクセルデータの例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/70e23bda75be4c668322cb58ae4b6bbe.png)

項目名|データの種類|プリザンター項目|設定項目
---|---|---|---
顧客CD|文字列|説明A|スタイル：ノーマル
顧客名|文字列|タイトル
郵便番号|文字列|説明B|スタイル：ノーマル
住所1|文字列|説明C|スタイル：ノーマル
住所2|文字列|説明D|スタイル：ノーマル

商談管理(子テーブル)
![商談管理（子テーブル）のエクセルデータの例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/963c0de8827247268b79faaeb52ef7a5.png)

この場合、商談管理の顧客CDが顧客管理の顧客CDと紐付けて使用されるため、商談管理には顧客名の項目がありません。一意性を保つために親テーブル側では顧客CDと顧客名などをセットで管理し、子テーブル側では顧客CDだけを記録し顧客名は親テーブルを参照するというケースが多くあります。

---

## 1. マスタデータとなる親テーブルと子テーブルをリンクさせる場合の注意

プリザンターのリンク機能は、親テーブルのタイトル項目と子テーブルの分類項目が紐付けられます。今回の例で言うと、一般的には顧客名がタイトルになるケースが多くなりますが、顧客名がタイトルの場合、同名の会社名があった場合、どちらがどちらか判別が難しくなります。

![顧客名をタイトルにした場合の選択肢の表示例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/90a276e4c0314a7592d5484535f69390.png)

一意性を保つために顧客CDをタイトル項目にすると、今度はどのコードがどの顧客かの判別が難しくなります。

![顧客CDをタイトルにした場合の選択肢の表示例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/26dc1a753c9446d3a21f41719114ec7a.png)

そのため、プリザンターでは顧客CDと顧客名など、複数の項目を結合してタイトルとして扱う[タイトル結合](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-title-combination.md)という機能があります。

![顧客CDと顧客名を結合したタイトルの表示例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/c88f41f363de4b29ae029ce6fa6f302f.png)

[タイトル結合](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-title-combination.md)は以下の画面のように[テーブルの管理](../../../../managers-guide/manage-table/index.md)→[エディタ](../edit-records/table-editor.md)から[選択肢一覧](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)にある「顧客CD」を有効化し、現在の設定で、上から「顧客CD」、「顧客名」という並びにします。今回は[タイトル](../../../../managers-guide/tenant-administration/tenant-logo.md)の表示名を「顧客名」に変更して使っています。  

![エディタで「顧客CD」「顧客名」の順に並べたタイトル結合の設定](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/254fe9e5931841779ea9efc6f95027ca.png)

---

## 2. エクセルデータをインポートするテーブルを作成し、リンクを設定する

まずは、エクセルデータと項目名([テーブルの管理](../../../../managers-guide/manage-table/index.md)→[エディタ](../edit-records/table-editor.md)の項目名)を合わせて顧客管理テーブルと商談管理テーブルを作成します。

![エクセルに合わせて項目を設定した顧客管理テーブルの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/48276585c6d3446fac3918e246ecaba0.png)

![エクセルに合わせて項目を設定した商談管理テーブルの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/d676faa0319b4245bab0581e6f3569b6.png)

---

## 3. 親データのエクセルデータをインポートする

まずは親テーブルからデータをインポートします。    
顧客管理テーブルを開き、一覧画面からインポートボタンをクリックしてください。

![顧客管理テーブルの一覧画面と「インポート」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/021f03df231244b5992e5e7597fac3ef.png)

文字コードは正しく選択してください。   
[エクセルデータをプリザンターにインポートする](table-record-import.md)

![文字コードを選ぶインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/200630c95e634dbba970129e1cff6b89.png)

[タイトル結合](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-title-combination.md)の設定通り「顧客CD)顧客名」という形式でデータが結合されています。

---

## 4. 子データのエクセルデータをインポートする

下図では親データの顧客はタイトル、子データの顧客は分類Aを指しています。
子データからリンクさせる親データのタイトルは「顧客CD)顧客名」という形式に結合されているので、元データのままではリンクが正しく設定されません。

![親データのタイトルと子データの「顧客」項目を対比した図](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/4a55687051634093a3c383ab47caf6c1.png)

そのため、インポートする前に子データを親データのタイトルと同様の形式にする必要があります。最初の状態のままのデータをインポートすると正しくリンクが設定されず「顧客」の先頭が？と表示されてしまいます。

![リンクが設定されず「顧客」の先頭が？と表示された一覧](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/73bd893cd3074467b31b16ac7b3401a8.png)

元データがエクセルの場合、VLOOKUP関数などを用いて「顧客CD)顧客名」のように結合したデータを作成してインポートしてください。

![「顧客CD)顧客名」の形式に結合した子データのCSV](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/666bfedb17204744a3e888baf77730e2.png)

項目名|データの種類|プリザンター項目|設定項目
---|---|---|---
顧客|文字列|分類A|スタイル：ノーマル。  顧客CDと顧客名を結合。
案件名|文字列|タイトル
状況|数値|状況|
商談確度|文字列|説明B|スタイル：ノーマル
商談開始日|日付|日付A|
見積提出日|日付|日付B|
期限|日付|完了|
見積金額|数値|数値A
担当者|分類|分類B

タイトルを結合したデータをインポートすると、このように自動的にリンク設定が有効になります。

![リンクが設定された商談管理テーブルの一覧](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/abb4fc847e4640d68c1ff4bb051bcdcd.png)

## 親テーブル(マスタ)をレコードIDで指定する

![「顧客」にレコードIDを指定したデータの例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/e8674aef3a3e4e9f95929b73f6a3661a.png)
上図のように「10100)株式会社アシスト」という「顧客」名ではなくレコードIDの「27287」でもマスタテーブルの項目と紐付けることができます。

## リンクされたテーブルに移動する

リンクが設定されたレコード同士は、編集画面に表示されますので相互に移動することができるようになります。
![編集画面に表示されたリンク先のレコード一覧](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/8317bbd7e8054f70bf20014d6c5b5766.png)

![リンクをたどって移動した先のレコードの編集画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/cbeb3d264b654e5ca2ddc1e7cdb4852c.png)

---

## インポートしたデータがうまくリンクされない場合の確認事項

1. 子テーブルのインポートを行う前にマスタテーブルを先にインポートしてください。先に子テーブルをインポートしてしまった場合は、マスタテーブルへのデータインポート後に、子テーブルのデータをエクスポートし、そのファイルを「IDが一致するレコードを更新する」にチェックを入れてインポートしてください。  
1. 子テーブルのリンク項目名は、親テーブルの項目名ではなく子テーブル側の項目名でインポートしてください。  

## 関連情報

-   [テーブル機能：レコードのインポート](table-record-import.md)
-   [組織管理機能：インポート](../../../../managers-guide/department-administration/dept-import.md)
-   [応用編：リンク](../../../hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：タイトル結合](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-title-combination.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../../managers-guide/tenant-administration/tenant-logo.md)