---
title: 複数選択
category: エディタ
order: '11300'
status: ''
parts: ''
urlstring: table-management-multiple-selections
translationKey: table-management-multiple-selections
shortname: 複数選択
created: 2021-02-03
updated: 2026-02-24
---

## 概要

分類項目の選択肢を複数選択できる設定です。

![複数選択を有効にした分類項目の表示例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/16c92bdcd42a4e52ba70866b8c6ad8b3.png)

## 制限事項

1.  親テーブルで複数選択を有効化していて、且つリンク設定をしている分類項目がある場合、子テーブルの編集画面のリンク一覧に表示される親テーブルの分類項目のソート機能が動作しません。

## 操作手順

管理メニューのテーブルの管理をからエディタタブを開きます。有効化欄から複数選択機能を使いたい分類項目を選択し詳細設定ボタンをクリックします。

![エディタタブで分類項目を選び「詳細設定」ボタンを押す画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/16250a703a634d51b44ab051c6241dec.png)

詳細設定画面で「複数選択」にチェックをし変更ボタンをクリックします。エディタ画面に戻り、更新ボタンをクリックします。

![項目の詳細設定の「複数選択」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/8db4900f7222488fb5cc24669a1d14d7.png)

## 使用方法

複数選択が有効になった分類項目は以下の通り、選択肢の行頭にチェックボックスが表示され、複数選択が可能になります。

![複数選択が有効な分類項目。選択肢の行頭にチェックボックスが付く](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/92e37a9fb2aa437db4bd72826256fbe0.png)

検索機能が有効になっている場合には、検索ダイアログ内で複数検索することが可能です。Windowsの場合は ++ctrl++ キーを押しながら、macOSの場合は ++command++ キーを押しながら、選択したい項目を個別にクリックします。++shift++ キーでの範囲選択も可能です。項目選択後は「有効化」「無効化」ボタンをクリックします。「全て有効」「全て無効」ボタンをクリックすると全ての項目を有効または無効にできます。

![複数選択が有効なときの検索ダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/9b6a9c3f69044b689befa8025c22afb2.png)

一覧画面では以下のように複数選択された項目が並んで表示されます。

![複数選択した値が並んで表示される一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/aa23ab45c7c649edb7881cddb20d84ce.png)

## 既定値の設定

複数選択が有効な分類項目では以下の通り、既定値を配列形式で登録する必要があります。

``` json
["山田太郎","鈴木鈴子","佐藤里美"]
```

![複数選択の分類項目に既定値をJSON形式で設定した画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/b05dd5c6560247978f09e715dfc1d616.png)

## エクスポート

複数選択が有効になった分類項目はエクスポートでは以下のように出力されます。

``` json
["石田笑吉"]  
["山田太郎","鈴木鈴子","佐藤里美"]
```  

![複数選択の分類項目をエクスポートしたCSVの内容](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/e5f0c2cf8e294833afaa368a9666a800.png)

## エクスポートの設定

複数選択が有効になった分類項目は項目ごとにチェックの有無を以下のように出力できます。

1.  「管理」メニューの「[テーブルの管理](../../../../index.md)」から「[エクスポート](../../../../export/index.md)」タブを開き、「複数選択」が有効になった項目を選択して「詳細設定」をクリックします。  

    ![エクスポートタブで項目を選び「詳細設定」を押す画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/8388dec628774f56aff22f6e814c6d9a.png)

1.  ダイアログの分類を列に出力チェックボックスをチェックし変更をクリックします。エクスポート画面に戻ったら更新をクリックします。  

    ![エクスポートの詳細設定の「分類を列に出力」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/d243240329ea45b885448e1f1716a1ae.png)

1.  選択肢が個別の列として出力され、選択されている項目に1が書き込まれます。  

    ![選択肢ごとの列に1が書き込まれたエクスポート結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/d899c8687de446709f7d31fef128dbf2.png)

## インポート

エクスポートと同様に、選択されている項目に1と書き込んだ状態でインポートすることで選択された状態となります。

![インポートに使うCSVの内容（1/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/de36e7dfbd3440c7bb8cb2e7b19bde46.png)

![インポートに使うCSVの内容（2/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/e088b94a2759410da0ec9fd77fa149d7.png)

![インポートに使うCSVの内容（3/3）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/4ad8ee12b092482286fbca5cdecd3480.png)

## 対応バージョン

| 対応バージョン | 内容                               |
| :------------- | :--------------------------------- |
| 1.4.12.0 以降  | 「全て有効」「全て無効」ボタン追加 |

## 関連情報

-   [テーブルの管理：エディタ](../../../index.md)  
-   [テーブルの管理：エクスポート](../../../../export/index.md)  
-   [CSVデータをプリザンターにインポートする](../../../../../../users-guide/table/record-authoring/create-records/table-record-import.md)
