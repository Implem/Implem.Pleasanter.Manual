---
title: レコードに画像を登録
category: テーブル機能
order: '911'
status: ''
parts: ''
urlstring: table-record-upload-picture
translationKey: table-record-upload-picture
shortname: 画像,05.レコード作成
created: 2019-04-30
updated: 2025-10-24
---

## 概要

[内容項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[コメント項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)に任意の「画像」を登録 / 表示します。

## 制限事項

1. Internet Explorerではコピー＆ペーストによる登録は行えません。
1. テーブルがロックされている場合には「更新」ボタンが表示されず操作が行えません。
1. レコードがロックされている場合には「更新」ボタンが表示されず操作が行えません。
1. 読取専用のレコードは「更新」ボタンが表示されず操作できません。

## 前提条件

1. 「読み取り権限」と「削除権限」が必要です。
1. 項目の詳細設定で[画像の登録を許可](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-allow-adding-img.md)がオンになっている必要があります。
1. Androidでカメラ撮影した画像を登録するには、「パラメータ設定：Mobile.json」でEnableMobileCameraをtrueに設定する必要があります。これにより「画像ファイル選択ボタン」の右側に「カメラ起動ボタン」が表示されます。

    |画像ファイル選択ボタン|カメラ起動ボタン|
    |:-:|:-:|
    |![「画像ファイル選択」ボタンのアイコン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/2caaef36c8484d0083689ba741189fca.png)|![「カメラ起動」ボタンのアイコン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/0b9c8c120e4c4207bad11c144e9d4cae.png)|

1. Androidでプリザンターからカメラを使用するには、カメラアプリとChromeに「使用中のみ許可」、または「常に許可」権限を設定する必要があります。
1. 項目に登録した画像をクリックした際にポップアップ表示させるには、「パラメータ設定：General.json」でEnableLightBoxの値をtrueに設定する必要があります（初期値はtrueです）。falseに設定した場合は、新しく開いた別のタブに画像が表示されます。

## 1. PC

<details markdown="1">
<summary>画像ファイルを選択して登録</summary>

1. テキストエリア内の画像を挿入したい箇所にカーソルを置き、テキストエリア左下の「画像ファイル選択」ボタンをクリックしてください。
   ![テキストエリア左下の「画像ファイル選択」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/98911ea919f143e9a40b49d5b6ea4477.png)
1. 任意の画像ファイルを選択してください。
1. 項目に画像が登録されます。
</details>

<details markdown="1">
<summary>コピー＆ペーストで登録</summary>

1. 任意の画像をクリップボードにコピーしてください。
2. テキストエリア内の画像を挿入したい箇所にカーソルを置き、ペーストしてください。
3. 画像へのパスを示す文字列が挿入されます。
4. 編集を終了すると画像が表示されます。

![貼り付けた画像が項目に表示された状態](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/8b5fe63e9dea4f8993f25a2baa3fa402.png)
</details>

<details markdown="1">
<summary>カメラで撮影した画像を登録</summary>

<a id="bootcamera"></a>
1. テキストエリア左下のカメラ起動ボタンをクリックしてください。
   ![テキストエリア左下の「カメラ起動」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/2cc2ab1297c045129509a725b48af209.png)
1. 撮影するカメラを選択し、許可方法を選択してください。
   ![使用するカメラと許可方法を選ぶ画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/c50e84a82a924b13b504800b09a13554.png)
1. 「撮影」ボタンをクリックしてください。
   ![「撮影」ボタンがあるカメラの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/8d57126b87ad4c7d83ee108d9379b0a4.png)
1. 項目に画像が登録されます。
</details>

<details markdown="1">
<summary>登録した画像を表示</summary>

登録した画像をクリックすると、下図のように登録した画像をポップアップ表示で確認することができます。

![登録した画像をクリックしたときのポップアップ表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/4cb6be06651743aca4e60475d385d81f.png)
</details>

## 2. iPhone

<details markdown="1">
<summary>画像ファイルを選択して登録</summary>

1. テキストエリア内の画像を挿入したい箇所にカーソルを置き、テキストエリア左下の「画像ファイル選択」ボタンをタップしてください。
1. 「写真ライブラリ」をタップしてください。
   ![iPhoneで表示される「写真ライブラリ」を含む選択メニュー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/d78fc8e564a84376b279a869e0ec929c.png)
1. 任意の画像ファイルを選択してください。
1. 項目に画像が登録されます。
</details>

<details markdown="1">
<summary>コピー＆ペーストで登録</summary>

1. 任意の画像をコピーしてください。
2. テキストエリア内の画像を挿入したい箇所にカーソルを置き、ペーストしてください。
3. 画像へのパスを示す文字列が挿入されます。
4. 編集を終了すると画像が表示されます。
</details>

<details markdown="1">
<summary>カメラで撮影した画像を登録</summary>

1. テキストエリア内の画像を挿入したい箇所にカーソルを置き、テキストエリア左下の「画像ファイル選択」ボタンをタップしてください。
1. 「写真を撮る」をタップしてください。
   ![iPhoneで表示される「写真を撮る」を含む選択メニュー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/84f8ebaedf244eb9b44f4c128de10c2d.png)
1. 撮影が完了すると、画面下部に「再撮影」と「写真を使用」が表示されます。「写真を使用」をタップしてください。  
   ![撮影後に「再撮影」「写真を使用」が表示されたiPhoneの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/84ab36a3fa834905b130bb2c5fe02e04.png)
1. 項目に画像が登録されます。
</details>

<details markdown="1">
<summary>登録した画像を表示</summary>

項目に登録した画像をタップすると、登録した画像をポップアップ表示で確認できます。
</details>

## 3. Android

<details markdown="1">
<summary>画像ファイルを選択して登録</summary>

1. テキストエリア内の画像を挿入したい箇所にカーソルを置き、テキストエリア左下の「画像ファイル選択」ボタンをタップしてください。  
   ![Androidのテキストエリア左下の「画像ファイル選択」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/fad66971e4ec4417b170029257a3fa8d.png)
1. 任意の画像ファイルを選択してください。
1. 項目に画像が登録されます。
</details>

<details markdown="1">
<summary>コピー＆ペーストで登録</summary>

1. 任意の画像をコピーしてください。
2. テキストエリア内の画像を挿入したい箇所にカーソルを置き、ペーストしてください。
3. 画像へのパスを示す文字列が挿入されます。
4. 編集を終了すると画像が表示されます。
</details>

<details markdown="1">
<summary>カメラで撮影した画像を登録</summary>

1. テキストエリア内の画像を挿入したい箇所にカーソルを置き、テキストエリア左下の「カメラ起動」ボタンをタップしてください。  
   ![Androidのテキストエリア左下の「カメラ起動」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/f7a1a0ae65df471b99c062a4d595d927.png)
1. 必要に応じて、「カメラ切替」ボタンをクリックし、撮影に使用するカメラを切り替えてください。
1. 「撮影」ボタンをタップすると、項目に画像が登録できます。  
   ![Androidのカメラ画面の「撮影」ボタン](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/a63ae77e181f44fc8a2cfbd800bd3958.png)
</details>

<details markdown="1">
<summary>登録した画像を表示</summary>

項目に登録した画像をタップすると、登録した画像をポップアップ表示で確認できます。
</details>

## 関連情報

-   [テーブルの管理：項目：内容](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：説明](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：コメント](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：画像の登録を許可](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-allow-adding-img.md)