---
title: 項目拡張手順
category: 項目数を増やす手順
order: '700'
status: ''
parts: ''
urlstring: enterprise-edition-columns-expansion
translationKey: enterprise-edition-columns-expansion
shortname: Enterprise Edition,項目拡張
created: 2025-01-24
updated: 2025-02-14
---

## 概要

Community Editionでは[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB          | Enterprise Editionで利用できる項目の上限 |
| :---------- | :--------------------------------------- |
| SQL Server  | 6つの項目種別の合計で最大900個まで       |
| PostgreSQL  | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]   | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

拡張した項目は"001"からの連番で作成されます（分類001、分類002・・・等）。  
項目を拡張する、拡張した項目数を変更する場合は本手順を実行してください。

## 注意事項

項目拡張を行うと期限付きテーブル（Issuesテーブル）、記録テーブル（Resultsテーブル）のテーブル構造を変更します。特に項目数を削減する場合にはテーブルから項目そのものを削除するため、項目拡張で増やした項目に登録したデータが消滅します。項目拡張を行う前には必ずバックアップを取得してください。

## 前提条件

本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

### 1. データベースのバックアップ

ご利用中の環境に応じてデータベースのバックアップを行ってください。弊社オンラインマニュアルもご参考ください。  
[Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)

### 2. Issues.jsonおよびResults.jsonの編集、格納

プリザンターインストールフォルダ[^2]配下の\App_Data\Parameters\ExtendedColumns にある、Issues.jsonおよびResults.jsonを変更してください。

- Issues.json：期限付きテーブル

    ``` json
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

- Results.json：記録テーブル

    ``` json
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

- 設定内容

    |項目|内容|
    |:----|:----|
    |Class|分類項目に追加する項目数|
    |Num|数値項目に追加する項目数|
    |Date|日付項目に追加する項目数|
    |Description|説明項目に追加する項目数|
    |Check|チェック項目に追加する項目数|
    |Attachments|添付ファイル項目に追加する項目数|

[^2]:
    プリザンターインストールフォルダは弊社オンラインマニュアルの手順に従ってインストールした場合以下の通りです。ご利用中の環境に応じて適宜読み替えてください。

    | OS                | インストールフォルダ                |
    | :---------------- | :---------------------------------- |
    | Windows           | C:\web\pleasanter\Implem.Pleasanter |
    | Linux             | /web/pleasanter/Implem.Pleasanter   |
    | Azure App Service | C:\home\site\wwwroot\               |

### 3. CodeDefinerの実行

弊社オンラインマニュアルを参考にCodeDefinerを実行してください。

=== ":fontawesome-brands-windows: Windows環境"

    1.  コマンドプロンプト（またはPowerShell、ターミナル）を開き、以下コマンドを実行します。

        ``` bat
        cd C:\web\pleasanter\Implem.CodeDefiner
        dotnet Implem.CodeDefiner.dll _rds
        ```

=== ":fontawesome-brands-linux: Linux環境"

    1.  以下コマンドを実行します。<プリザンター起動ユーザ>は「Pleasanterサービス用スクリプト」で指定するユーザを指します。詳しくは弊社オンラインマニュアルを参照ください。

        ``` bash
        cd /web/pleasanter/Implem.CodeDefiner
        sudo -u <プリザンター起動ユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds
        ```

=== ":material-microsoft-azure: Azure App Service環境"

    1.  Kudu のディレクトリ一覧から CodeDefiner を選択し、 プロンプトが C:\home\site\CodeDefiner となることを確認します。
    1.  次のコマンドを実行します。

        ``` bat
        dotnet Implem.CodeDefiner.dll _rds /p C:\home\site\wwwroot
        ```

上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。

### 4. 項目拡張の確認

<div class="steps" markdown>

1.  弊社オンラインマニュアルを参考にプリザンターを再起動してください。

    === ":fontawesome-brands-windows: Windows環境"

        1.  インターネットインフォメーションサービス（IIS）マネージャを開きます。
        1.  左ペインより、「サイト」-「Default Web Site」を選択して、右ペインの「再起動」をクリックします。

    === ":fontawesome-brands-linux: Linux環境"

        1.  以下コマンドを実行します。

            ``` bash
            sudo systemctl restart pleasanter
            ```

    === ":material-microsoft-azure: Azure App Service環境"

        1.  App Serviceを開き「再起動」をクリックします。

1.  プリザンターにログインし、任意のテーブルを開き、ナビゲーションメニューの「管理」－[テーブルの管理](../../../managers-guide/manage-table/index.md)より[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブにて、選択肢一覧のリストに拡張した項目（分類001、数値001等）が表示されることを確認してください。

</div>

## 関連情報

-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [Pleasanter ユーザーマニュアル － FAQ：バックアップ、リストア](../../../FAQ/backup-restore/index.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
