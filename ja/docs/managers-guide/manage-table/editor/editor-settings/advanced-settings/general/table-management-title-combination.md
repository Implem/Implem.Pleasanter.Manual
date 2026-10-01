---
title: タイトル結合
category: エディタ
order: '16900'
status: ''
parts: ''
urlstring: table-management-title-combination
translationKey: table-management-title-combination
shortname: タイトル結合
created: 2020-02-26
updated: 2024-04-09
---

## 概要

複数の項目を結合してタイトルとして扱う方法を説明します。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

顧客管理を行うアプリを作成する場合を例とします。  

### 背景

下図のような顧客名簿があった場合、顧客名が重複してしまう可能性があります。

![顧客名が重複している顧客名簿の一覧](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/8c08b7ae257d4f1bbad01d7391a9cd86.png)

顧客リストをマスタデータとして他のテーブルとリンクして使いたい場合、顧客名が重複してしまうとどちらがどちらか判別ができなくなります。

![顧客名が重複していてリンク先で判別できない例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/95b130389f964c05856c23bcc0cc3417.png)

このようなケースの対策として、一意性のあるコード（顧客を識別する番号や文字列）を付与して管理する方法が用いられます。下図で言うと、株式会社アシストという同名の会社が2つありますが、それぞれ10100と30300という異なった顧客CDを付与してセットで管理することで一意性を保っています。

![顧客CDを付与して一意性を保っている顧客名簿の一覧](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/c08d9baf3638487cb71e4e149730de38.png)

プリザンターでは、タイトル項目の一意性を保つために（標準では値の重複は禁止されていません）、複数の項目を結合してタイトルとして扱うタイトル結合という機能があります。

### 操作

1.  タイトル結合を設定したいテーブルを開いてください。
1.  ナビゲーションメニューより「管理」→[テーブルの管理](../../../../index.md)→[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)を開いてください。
1.  「現在の設定」欄から「顧客名」を選択し（説明の便宜上、項目名に(タイトル)をつけています）、「詳細設定」をクリックしてください。

    ![タイトル項目の「顧客名」を選び「詳細設定」を開いた画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/56a73d368ddb4fd89eb414f3cdc68a27.png)

1.  選択肢一覧から「顧客CD」を選択して「有効化」し、下図のように上から「顧客CD」、「顧客名」と並び替えてください。

    ![タイトル結合の設定で「顧客CD」「顧客名」の順に並べた状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/82de54da839b4802af5fa89d7b49c769.png)

1.  既にデータが入っている場合は「同期」ボタンをクリックすることで、テーブル内の全てのデータのタイトルを設定に従って作り直します。

    各項目を区切る「タイトル区切り文字」は必要であれば変更してください。

    !!! warning
        「タイトル区切り文字」に,(カンマ)は使用しないでください。

1.  「更新」ボタンをクリックし、一覧画面を開いてください。設定が完了すると、下図のように「顧客CD)顧客名」という形式で表示されます。

    ![「顧客CD)顧客名」の形式で表示された一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/fc3378cdeea743d0a113ed83cc75a629.png)

    顧客CDと顧客名を区切っている文字、この場合は「)」は先ほどの詳細画面「タイトル区切り文字」で設定できます。  

## 識別するための顧客CDなどがない場合の一意性の確保  

プリザンターでは、レコードごとに一意のIDが割り当てられますので、指定のコード等がない場合は下図のようにIDと結合させることで一意性を確保することができます。  

![IDと結合してタイトルの一意性を確保する設定（1/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/ac6e28345daa41818a386fa0bca7aa0d.png)

![IDと結合してタイトルの一意性を確保する設定（2/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/9393683c1b1b467c92f4c2f771d0af57.png)

## 既にデータが存在する状態でタイトル結合を設定（更新）した場合

![既にデータがある状態でタイトル結合を設定した場合の表示](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/64412a7b285249bb9b45ffb4a7ce9a6c.png)

「同期」ボタンをクリックするとテーブル内の全データに設定を反映させ同期することができます。設定を変更してもタイトルが変わらないという場合は「同期」処理を行ってください。

## 関連情報

-   [テーブルの管理](../../../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
