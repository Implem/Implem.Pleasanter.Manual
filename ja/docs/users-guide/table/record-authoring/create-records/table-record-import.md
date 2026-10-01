---
title: レコードのインポート
category: テーブル機能
order: '201'
status: ''
parts: ''
urlstring: table-record-import
translationKey: table-record-import
shortname: インポート
keywords:
  - import
  - 'インポート'
created: 2020-01-23
updated: 2025-09-22
---

## 概要

エクセルで管理していた簡易的な社員名簿を、プリザンターで管理できるようにデータのインポートを行うケースとして説明します。  

-   プリザンター1.4.16.0以降

    「作成者」、「作成日時」、「更新者」、「更新日時」の取り込みが可能となる移行モード機能が追加されました。  
    →[移行モードでのレコードのインポート](table-record-import-migrate-mode.md)

-   プリザンター1.3.11.2以降

    キー項目を指定したインポートが可能となりました。
    →[インポート時のキー項目指定](table-record-import-key.md)

## 操作手順

下記手順で進めます。      

<div class="steps" markdown>

1.  社員名簿のエクセルデータを開き「名前を付けて保存」を選択し、ファイル形式で以下のいずれかを選択して保存する

    -   「CSV(コンマ区切り)(.csv)」
    -   「CSV UTF-8（コンマ区切り)(.csv)」

1.  「社員名簿」記録テーブルの作成する  
1.  [エディタ](../edit-records/table-editor.md)で項目を設定する  
1.  「社員名簿.csv」をインポートする  
1.  [一覧](../../../../managers-guide/manage-table/grid/index.md)で一覧画面の表示項目を設定する  

!!! warning "確認事項"
    -   **インポートするCSVデータのタイトル(CSVデータの1行目)と、プリザンターの項目名は一致させること。**  
        ([テーブルの管理](../../../../managers-guide/manage-table/index.md)-[一覧](../../../../managers-guide/manage-table/grid/index.md)ではなく[エディタ](../edit-records/table-editor.md)で表示される項目名に合わせてください)  

    -   **期限付きテーブルの場合「完了」項目は必須項目となります。**  
        (記録テーブルの場合、必須項目はございません)

    -   **年-月-日形式で日付データをインポートする場合、年は4桁（yyyy-mm-dd）としてください。**  
        年を2桁とした場合、仕様により正しくインポートできません。

</div>

### インポートの手順  

下記のエクセルデータの構成を例として説明します。  

![インポート元となる社員名簿のエクセルデータの例](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/8cfa5359da6b4ddb8ac2f4a5b990fbe7.png)

<div class="steps" markdown>

1.  「管理」→[テーブルの管理](../../../../managers-guide/manage-table/index.md)→[エディタ](../edit-records/table-editor.md)タブを選択します。  
1.  プリザンターの仕様上「ID」、「バージョン」は無効化できませんので、その2つの項目は残して、それ以外を無効化し、以下の通り各項目を有効化してください。

    プリザンターの「エディタ」設定画面  
    ![有効化する項目を設定したエディタの設定画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/cb71e899df9440c0bee306aec992640f.png)

1.  有効化した項目は以下の通り設定を変更します。有効化した項目を選択状態にして、「詳細設定」ボタンをクリックして各設定を行います。

    |項目名|データの種類|プリザンター項目|設定項目|
    |---|---|---|---|
    |社員ID|文字列|説明A|スタイル：ノーマル|
    |氏名|文字列|タイトル|
    |出身地|文字列|説明B|スタイル：ノーマル|
    |性別|文字列|分類A|選択肢一覧：男 (改行) 女|
    |生年月日|日付|日付A|
    |年齢|数値|数値A|

1.  「性別」分類Aの選択肢一覧の記載内容を、以下のように設定します。  

    ![分類Aの選択肢一覧に「男」「女」を記述した設定](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/2b7c07e555e147199a9fe2aa664f65f4.png) 

    項目名設定後のエディタ画面  
    ![項目名を設定した後のエディタ画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/8fc6bdc63fea47f6abe6007264e82f32.png)

1.  プリザンターにデータをインポートするために、元データ(CSV)の項目名とプリザンターの項目名を一致させます。

    ![CSVの項目名とプリザンターの項目名の対応を示した図](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/c687e4a466fd460c92e818f5e3247763.png)

    !!! warning
        プリザンター側の項目名は[一覧](../../../../managers-guide/manage-table/grid/index.md)ではなく[エディタ](../edit-records/table-editor.md)で設定してください。  

        ![項目名を設定するエディタの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/811fa3cc610643e5b90db7216cd1c654.png)

        プリザンターの項目種別と、項目名を間違わないように注意してください。

1.  項目の設定が完了したら、設定を「更新」をクリックして一覧画面に戻りインポートボタンをクリックします。   
1.  ダイアログが表示されたら、インポートするCSVファイルを選択します。  
1.  該当するCSVファイルの文字コードを選択し、インポートボタンをクリックします。   

    !!! warning "確認事項"
        インポートするCSVデータがShift-JISで保存されているか、UTF-8形式か確認し、下記のプリザンターのインポートダイアログに表示される「文字コード」欄にて保存されている形式を選んでください。

        ![CSVファイルと文字コードを選ぶインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/98ffe0cbe925431b8bcf61db9ce5fae5.png)

1.  インポートが無事に完了すると下図のように一覧画面に表示されます。  

    ![インポートしたレコードが並ぶ一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/3f9047d5c6794181b0a8183ed142a2e5.png)

1.  次に、一覧画面を、エクセルで管理していたときと同じ内容が表示されるように設定して行きます。  

1.  「管理」→「[テーブルの管理](../../../../managers-guide/manage-table/index.md)」→「 [一覧](../../../../managers-guide/manage-table/grid/index.md)」タブを選択します。初期状態では以下の設定になっています。  

    ![テーブルの管理の「一覧」タブの初期状態](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/cd8d3a865c124d2b8a505dc7b68cd17c.png)

    以下のように、今回インポートした全項目を表示するように設定します。今回のデータ例では以下の項目を有効化します。（それ以外は無効化します。）

    -   社員ID
    -   氏名
    -   出身地
    -   性別
    -   生年月日
    -   年齢

1.  項目の有効化を終えたら「更新」ボタンをクリックし、その後 「戻る」をクリックして一覧画面を表示します。  

    ![インポートした全項目を有効化した「一覧」タブの設定](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/c970c65567614cbdbf853bbd2492e382.png)

1.  元のエクセルデータのような一覧表示ができました。  

    ![全項目が表示された一覧画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/12ce27c9b4604617893bc92725ee1e5d.png)

</div>

以上で、エクセルのデータをプリザンターに移行することができました。

## インポートがうまく行かない場合の確認事項

### データがインポートできない、または一部しかインポートされていない

- [x] 「[テーブルの管理](../../../../managers-guide/manage-table/index.md)」→「[一覧](../../../../managers-guide/manage-table/grid/index.md)」ではなく「[エディタ](../../../../managers-guide/manage-table/editor/index.md)」で設定した項目名とCSVデータのタイトルが一致しているか確認してください。

    ![エディタで設定した項目名とCSVのタイトル行を見比べる図](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/f4cbe4fe0413465fa78daaacd7cf2fc3.png)

- [x] インポート時の文字コードが正しく選択されているか確認してください。

    ![インポートのダイアログの「文字コード」欄](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/d50e194b4a044757a8a30af778155196.png)

    英数字は取り込めて、日本語がうまく取り込めないという場合は文字コードが正しくないケースが考えられますので、うまくいかない場合は、もう一方を試してみてください。

- [x] 期限付きテーブルの場合「完了」項目は値が必須です。

    期限付きテーブルにデータをインポートする場合は「完了」項目には必ず値を入れてください。[^1]

    [^1]: 記録テーブルの場合には「完了」項目はありません。  

- [x] Pleasanter.netでは一度のインポート処理で取り込めるレコード数が10,000行となっています。

    10,000行を超える量のデータをインポートする場合は、10,000行ごとに区切ってインポートしてください。  

- [x] CSVファイルで値を設定してもインポートしない項目があります。

    詳細は以下の表を確認してください。  

    |項目名|レコード追加時|レコード更新時|
    |:---:|:---|:---|
    |ID|プリザンターで自動採番|更新しない|
    |バージョン|プリザンターで自動採番|プリザンターで自動採番|
    |作成者|インポート操作を行ったユーザ [^2]|更新しない|
    |作成日時|インポート操作を行った日時 [^2]|更新しない|
    |更新者|インポート操作を行ったユーザ [^2]|インポート操作を行ったユーザ|
    |更新日時|インポート操作を行った日時 [^2]|インポート操作を行った日時|
    |コメント|CSVファイルの値 [^3]|[JSON形式](../../../../developers-guide/json-data-layout/api-comment.md)の場合は洗い替え方式で更新<br>文字列形式の場合は更新しない|

    [^2]: 移行モードでは、CSVファイルに設定されている値でインポートすることが可能です。詳細は「[テーブル機能：移行モードでのレコードのインポート](table-record-import-migrate-mode.md)」を参照してください。
    [^3]: JSON形式のデータレイアウトの値でインポートすることが可能です。詳細は[JSONデータレイアウト：コメント](../../../../developers-guide/json-data-layout/api-comment.md)を参照してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.18.0 以降|CSVインポートでレコード更新時にコメントを更新する機能を追加|

## 関連情報

-   [テーブル機能：インポート時のキー項目指定](table-record-import-key.md)
-   [テーブル機能：レコードのエディタ画面](../edit-records/table-editor.md)
-   [テーブルの管理：一覧画面](../../../../managers-guide/manage-table/grid/index.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [組織管理機能：インポート](../../../../managers-guide/department-administration/dept-import.md)
-   [JSON形式](../../../../developers-guide/json-data-layout/api-comment.md)
-   [開発者ガイド：JSONデータレイアウト：コメント](../../../../developers-guide/json-data-layout/api-comment.md)
