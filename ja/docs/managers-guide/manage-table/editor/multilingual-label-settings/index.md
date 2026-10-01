---
title: 多言語ラベルのインポート／エクスポート
category: エディタ
order: '0'
status: ''
parts: ''
urlstring: table-management-multilingual-label-settings
translationKey: table-management-multilingual-label-settings
shortname: 多言語ラベルのインポート／エクスポート
created: 2025-12-17
updated: 2026-02-10
---

## 概要

[項目の詳細設定：多言語タブ](../editor-settings/advanced-settings/multilingual/index.md)の設定情報を、テーブル単位で、CSVファイルとしてインポートまたはエクスポートします。[項目の詳細設定：多言語タブ](../editor-settings/advanced-settings/multilingual/index.md)では項目ごとに設定が必要ですが、「多言語ラベル設定」ではサイト（テーブル）単位で一括設定が可能です。

本機能でインポートしたデータは、「項目の詳細設定：多言語」タブの設定を上書きします。

インポート、エクスポートされるのは、以下の形式のCSVファイルです。

``` csv title="CSVファイルの例"
ColumnName,Attributes,ja,en,zh,de,ko,es,vn
ClassA,LabelText,支店名,Branch name,分店名称,Filialname,지점명,Nombre de Sucursal,Tên Chi Nhánh
ClassA,Description,「XX支店」と入力,"Enter as ""XX branch""","输入""XX支店""","Geben Sie ""XX-Filiale"" ein","""XX지점""을 입력","Ingrese como ""Sucursal XX""","Nhập ""Chi nhánh XX"""
NumA,LabelText,合計金額,Total Amount,合计金额,Gesamtbetrag,총액,Importe total,Tổng số tiền
```

CSVファイルの各列の意味は以下の通りです。

| No  |     列     | 指定 | 説明                                                                                                      |
| :-: | :--------: | :--- | :-------------------------------------------------------------------------------------------------------- |
|  1  | ColumnName | 必須 | ClassA、NumAのような[カラム名](../../../../developers-guide/dev-column-name.md)を設定。                   |
|  2  | Attributes | 必須 | 以下のうち、いずれか1つを設定。<br>・LabelText：表示名<br>・Description：説明<br>・InputGuide：入力ガイド |
|  3  |     ja     | 任意 | 日本語で表示文言を設定。                                                                                  |
|  4  |     en     | 任意 | 英語で表示文言を設定。                                                                                    |
|  5  |     zh     | 任意 | 中国語で表示文言を設定。                                                                                  |
|  6  |     de     | 任意 | ドイツ語で表示文言を設定。                                                                                |
|  7  |     ko     | 任意 | 韓国語で表示文言を設定。                                                                                  |
|  8  |     es     | 任意 | スペインで表示文言を設定。                                                                                |
|  9  |     vn     | 任意 | ベトナム語で表示文言を設定。                                                                              |

## CSV設定の省略

翻訳データの設定が必要ない場合、以下のようにCSVファイルの記述を省略できます。

1.  特定言語の翻訳データ設定を省略できます。

    以下の例では、英語の[表示名](../editor-settings/advanced-settings/general/table-management-label-text.md)のみを設定しています。

    ``` csv
    ColumnName,Attributes,en
    ClassA,LabelText,Branch name
    ```

    ただし、少なくとも1つ言語について設定が必要です。

    **以下のCSVはインポート時にエラーとなります**。

    ``` csv
    ColumnName,Attributes
    ClassA,LabelText
    ```

1.  翻訳データを空文字列とすることで、翻訳データの設定を省略できます。

    以下の例では、日本語の[表示名](../editor-settings/advanced-settings/general/table-management-label-text.md)の設定を省略しています。

    ``` csv
    ColumnName,Attributes,ja,en
    ClassA,LabelText,,Branch name
    ```

## 操作手順

1.  対象のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [テーブルの管理](../../index.md)をクリックしてください。
1.  「 エディタ 」タブをクリックしてください。

    「多言語ラベル設定」は、「 エディタ 」タブの下部に配置されています。

    ![エディタタブ下部の「多言語ラベル設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/73ea9b48c6b0432a9bf89d571d217384.png)

    なお、テーブルの編集後、コマンドボタンエリアの「更新」ボタンをクリックせずにインポートまたはエクスポートしようとすると、コマンドボタンエリアの上に以下のアラートが表示されます。

    ![更新せずにインポート・エクスポートしたときのアラート](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/f94dcc0a55874881b56aeb5380ee5d45.png)

    コマンドボタンエリアの「更新」ボタンをクリックするか、ページをリロードして編集をキャンセルしてからインポートまたはエクスポートを実行してください。

### エクスポート

1.  「多言語ラベル設定」の「 エクスポート 」ボタンをクリックしてください。
1.  「文字コード」を選択してください。「UTF-8」（既定）または「Shift-JIS」を選択できますが、**日本語と英語以外の言語を設定する場合は「UTF-8」を選択**してください。

    ![エクスポートの文字コードを選ぶダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/22c695003ea542f5bb73d96089ed8ce6.png)

1.  「 エクスポート 」ボタンをクリックしてください。  

    ![「エクスポート」ボタンをクリックした後の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/3cde6f77606449b4b44b15998bb48ba4.png)

### インポート

1.  「多言語ラベル設定」の「 インポート 」ボタンをクリックしてください。
1.  「ファイルを選択」をクリックし、インポートするCSVファイルを選択してください。

    ![インポートするCSVファイルを選ぶダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/d15e03b8f9924a9e9f134453a11553f0.png)

1.  インポートするCSVファイルの「文字コード」を選択してください。「UTF-8」（既定）または「Shift-JIS」を選択できますが、**日本語と英語以外の言語を設定する場合は「UTF-8」を選択**してください。

    ![インポートの文字コードを選ぶダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/da7a3f585a2940c3955a4c3968066af6.png)

1.  「 インポート 」ボタンをクリックしてください。

    ![「インポート」ボタンをクリックした後の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/multilingual-label-settings/assets/d7552c5c26ee4b10bbb914aea6a28eb4.png)

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.1.0以降    | 機能追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：多言語](../editor-settings/advanced-settings/multilingual/index.md)
-   [項目名とデータベース上のカラム名の対応](../../../../developers-guide/dev-column-name.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../editor-settings/advanced-settings/general/table-management-label-text.md)
-   [テーブルの管理](../../index.md)
