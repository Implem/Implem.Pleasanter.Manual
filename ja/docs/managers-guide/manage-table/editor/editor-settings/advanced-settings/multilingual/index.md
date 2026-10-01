---
title: 多言語
category: エディタ
order: '0'
status: ''
parts: ''
urlstring: table-management-multilingual
translationKey: table-management-multilingual
shortname: 項目の詳細設定：多言語タブ
created: 2025-11-25
updated: 2025-12-17
---

## 概要

項目の詳細設定：多言語タブでは、以下の詳細設定項目について翻訳データを登録し、ユーザプロファイルの言語設定に応じた動的な表示言語切替を可能にします。

1.  [表示名](../general/table-management-label-text.md)
1.  [説明](../general/table-management-column-description.md)
1.  [入力ガイド](../general/table-management-input-guide.md)

![項目の詳細設定の「多言語」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/multilingual/assets/ba9ffc6eea4d43d98e87612509c68b51.png)

## 前提条件

1.  必要のない言語は設定を省略できます。
1.  必要のないパラメータは設定を省略できます。
1.  「多言語」タブの設定は「全般」タブの設定を上書きします。（たとえば、同じ言語について「全般」タブと「多言語」タブとで異なる[表示名](../general/table-management-label-text.md)を設定した場合、「多言語」タブの[表示名](../general/table-management-label-text.md)が表示されます。）
1.  「全般」タブで[既定値](../general/table-management-default-input.md)を設定した項目では、「多言語」タブで[入力ガイド](../general/table-management-input-guide.md)を設定しても無視されます。
1.  「数値」項目では、「多言語」タブで[入力ガイド](../general/table-management-input-guide.md)を設定しても無視されます。
1.  [一覧](../../../../grid/index.md)画面の「詳細設定」で[表示名](../general/table-management-label-text.md)を変更した場合、[エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)画面の表示名とは独立して管理されます。

## 対応言語

本機能は、日本語を含む、以下の7言語の表示をサポートしています。

| No. | 言語             | プリザンター内部の言語コード |
| --: | :--------------- | :--------------------------- |
|   1 | 英語             | en                           |
|   2 | 中国語（簡体字） | zh                           |
|   3 | 日本語           | ja                           |
|   4 | ドイツ語         | de                           |
|   5 | 韓国語           | ko                           |
|   6 | スペイン語       | es                           |
|   7 | ベトナム語       | vn                           |

## 説明用のユーザ

以下の説明では、次の2名のログインユーザを使用します。

| ログインユーザ | プロファイルの言語設定 |
| :------------- | :--------------------- |
| 斎藤 美樹      | Japanese               |
| Wilson Daniel  | English                |

## 多言語タブの設定

以下のような分類項目を作成し、上記の各ユーザがログインした場合の表示を比較します。

### 1. 斎藤 美樹がログインした場合の表示

「多言語」タブを設定していないため、「全般」タブの設定で表示します。

![斎藤 美樹がログインしたときの分類項目の表示](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/multilingual/assets/d64ae1e9608b459486d1d6234130f25e.png)

### 2. Wilson Danielがログインした場合の表示

プロファイルの言語設定は「English」ですが、「多言語」タブを設定していないため、「全般」タブの設定で表示します。

![Wilson Daniel がログインしたときの分類項目の表示（多言語タブ未設定）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/multilingual/assets/a3b5fa44c11d43e2804a24a13f517660.png)

### 3. Wilson Danielがログインした場合の表示

プロファイルの言語設定が「English」で、かつ「多言語」タブで設定しているため、「多言語」タブの設定で表示します。詳細は以下の「パラメータ」を参照してください。

![Wilson Daniel がログインしたときの分類項目の表示（多言語タブ設定済み）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/multilingual/assets/633b3614dcb5408fb04672c5875955e2.png)

## パラメータ

多言語タブの設定はJSON形式で記述します。

``` json title="パラメータの記述例（JSON形式）" linenums="1"
[
    {  
        "Language": "en", 
        "LabelText": "Branch name",
        "Description": "Enter as \"XX branch\"",
        "InputGuide": "Nakano branch"
    },
    {
        "Language": "de", 
        "LabelText": "Filialname"
    }
]
```

各パラメータの意味は以下の通りです。

| パラメータ  | 意味                                                                                                           |
| :---------- | :------------------------------------------------------------------------------------------------------------- |
| Language    | 表示に用いる言語を指定します。<br>上記「対応言語」における「プリザンター内部の言語コード」で指定してください。 |
| LabelText   | 翻訳した[表示名](../general/table-management-label-text.md)を指定してください。                                |
| Description | 翻訳した[説明](../general/table-management-column-description.md)を指定してください。                          |
| InputGuide  | 翻訳した[入力ガイド](../general/table-management-input-guide.md)を指定してください。                           |

## 操作手順

1.  対象のテーブルを開きます。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [テーブルの管理](../../../../index.md)をクリックしてください。
1.  [エディタ](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブをクリックしてください。
1.  「現在の設定」で対象の項目をクリックしてください。
1.  「詳細設定」ボタンをクリックしてください。
1.  「多言語」タブをクリックしてください。
1.  「多言語表示」に、上記のようなJSON形式で多言語データを入力してください。入力するのは必要な言語、パラメータだけで構いません。
1.  「変更」ボタンをクリックしてください。
1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.4.23.0 以降  | 機能追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../general/table-management-label-text.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../general/table-management-column-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力ガイド](../general/table-management-input-guide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値](../general/table-management-default-input.md)
-   [テーブルの管理：一覧画面](../../../../grid/index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理](../../../../index.md)
