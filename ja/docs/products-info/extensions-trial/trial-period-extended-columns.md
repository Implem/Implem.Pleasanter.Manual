---
title: トライアル期間中の項目拡張・項目縮小
category: トライアル
order: '1400'
status: ''
parts: ''
urlstring: pleasanter-extensions-trial-extended-columns
translationKey: pleasanter-extensions-trial-extended-columns
shortname: 追加する項目数の設定
created: 2025-12-01
updated: 2025-12-03
---

## 概要

トライアル期間中に項目の数を変更する手順です。

!!! danger "トライアル期間中に拡張した項目の縮小"

    項目数を減らす場合にはテーブルから項目そのものを削除するため、増やした項目に登録したデータは消滅します。  
    項目数を増やす前に必ず[データベースのバックアップを取得](../../developers-guide/index.md)してください。

## 操作手順

### Issues.jsonとResults.jsonの編集・保存

プリザンターのインストールフォルダ配下の`\App_Data\Parameters\ExtendedColumns`にある、以下の2つのファイルを編集・保存してください。

-   `Issues.json`
-   `Results.json`

!!! tip プリザンターのインストールフォルダ

    ユーザマニュアルの手順に従ってインストールした場合、プリザンターのインストールフォルダは以下の通りです。

    | OS                | インストールフォルダ                |
    | :---------------- | :---------------------------------- |
    | Windows           | C:\web\pleasanter\Implem.Pleasanter |
    | Linux             | /web/pleasanter/Implem.Pleasanter   |
    | Azure App Service | C:\home\site\wwwroot\               |

    利用中の環境に応じて適宜読み替えてください。

=== "Issues.json：期限付きテーブル"

    ``` json linenums="1" hl_lines="4-9"
    {
        "TableName": "Issues",
        "ReferenceType": "Issues",
        "Class": 0,
        "Num": 0,
        "Date": 0,
        "Description": 0,
        "Check": 0,
        "Attachments": 0
    }
    ```

=== "Results.json：記録テーブル"

    ``` json linenums="1" hl_lines="4-9"
    {
        "TableName": "Results",
        "ReferenceType": "Results",
        "Class": 0,
        "Num": 0,
        "Date": 0,
        "Description": 0,
        "Check": 0,
        "Attachments": 0
    }
    ```

#### 設定内容

| 項目        | 内容                             |
| :---------- | :------------------------------- |
| Class       | 分類項目に追加する項目数         |
| Num         | 数値項目に追加する項目数         |
| Date        | 日付項目に追加する項目数         |
| Description | 説明項目に追加する項目数         |
| Check       | チェック項目に追加する項目数     |
| Attachments | 添付ファイル項目に追加する項目数 |

### CodeDefinerの実行

プリザンターのインストールフォルダへ移動し、`CodeDefiner`コマンドに`trial /e`をつけて実行してください。

``` text title="Windowsでの実行例"
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll trial /e
```

## 関連情報
