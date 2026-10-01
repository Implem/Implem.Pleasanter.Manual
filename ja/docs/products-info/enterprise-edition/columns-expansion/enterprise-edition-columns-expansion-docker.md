---
title: 項目拡張手順（Docker利用）
category: 項目数を増やす手順
order: '701'
status: ''
parts: ''
urlstring: enterprise-edition-columns-expansion-docker
translationKey: enterprise-edition-columns-expansion-docker
shortname: Docker利用時の項目拡張
created: 2025-05-08
updated: 2026-07-17
---

## Docker版プリザンターについて

Docker Hubで公開されているプリザンターの公式Dockerイメージを利用する手順です。

implem/pleasanter - Docker Image | Docker Hub  
https://hub.docker.com/r/implem/pleasanter

## 概要

Community Editionでは[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB          | Enterprise Editionで利用できる項目の上限 |
| ----------- | ---------------------------------------- |
| PostgreSQL  | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]   | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

拡張した項目は"001"からの連番で作成されます（分類001、分類002・・・等）。  
項目を拡張する、拡張した項目数を変更する場合は本手順を実行してください。

## 注意事項

1. 項目拡張を行うと期限付きテーブル（Issuesテーブル）、記録テーブル（Resultsテーブル）のテーブル構造を変更します。特に項目数を削減する場合にはテーブルから項目そのものを削除するため、項目拡張で増やした項目に登録したデータが消滅します。項目拡張を行う前には必ずバックアップを取得してください。
1. ver1.4.5以前で実行する場合はCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
[ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../../../setup/installation/prerequisites/codedefiner-changed-steps.md)

## 前提条件

1. 本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

### 1. コンテナの停止

<div class="steps" markdown>

1. 以下コマンドを実行します。

    ```bash
    docker compose stop
    ```

</div>

### 2. データベースのバックアップ

<div class="steps" markdown>

1. ご利用中の環境に応じてデータベースのバックアップを行ってください。弊社オンラインマニュアルもご参考ください。

    -   [FAQ：PostgreSQL データベース バックアップ・リストア手順(Docker利用)](../../../FAQ/backup-restore/faq-postgresql-backup-restore-docker.md)
    -   [FAQ：MySQL データベース バックアップ・リストア手順(Docker利用)](../../../FAQ/backup-restore/faq-mysql-backup-restore-docker.md)

</div>

### 3. Issues.jsonおよびResults.jsonの編集、格納

<div class="steps" markdown>

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、起動するプリザンターと同一バージョンのモジュールをダウンロードします。
2. zipファイルを解凍します。
3. 解凍したフォルダからDocker用資源の配置先フォルダに以下のフォルダをコピーします。  

    -   コピーするフォルダ：\pleasanter\Implem.Pleasanter\App_Data\Parameters\ExtendedColumns フォルダをコピー  
    -   コピー先：\app_data_parameters フォルダ内に配置し、\app_data_parameters\ExtendedColumns フォルダを作成  
    ![ExtendedColumnsフォルダをDocker用資源の配置先にコピーした状態](https://pleasanter.org/files/images/ja/products-info/enterprise-edition/columns-expansion/assets/be32d79f30084993994f9737f50c04f6.png)

4. コピー先のExtendedColumnsフォルダ内にあるIssues.jsonおよびResults.jsonを編集します。  
    ![ExtendedColumnsフォルダ内のIssues.jsonとResults.json](https://pleasanter.org/files/images/ja/products-info/enterprise-edition/columns-expansion/assets/7ac82c83d10a43ceb32a862538de1f7d.png)

    - 期限付きテーブル

        ```json title="Issues.json" linenums="1" hl_lines="4-9"
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

    - 記録テーブル

        ```json title="Results.json" linenums="1" hl_lines="4-9"
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

</div>

### 4. コンテナイメージのビルド

<div class="steps" markdown>

1. 以下コマンドを実行します。

    ```bash
    docker compose build
    ```

</div>

### 5. CodeDefinerの実行

<div class="steps" markdown>

1. 以下コマンドを実行します。  
    ※Dockerイメージを使用する場合に限り、バージョンアップ時のコマンドに /l、/zの引数設定が必要です。

    ```bash
    docker compose run --rm codedefiner _rds /l "<言語>" /z "<タイムゾーン>"
    ```

    |引数|設定例|説明|
    |:--|:--|:--|
    |/l|ja|Service.jsonのDefaultLanguageの値を書き換えます[^2]|
    |/z|Asia/Tokyo|Service.jsonのTimeZoneDefaultの値を書き換えます[^2]|

</div>

[^2]:
    言語、タイムゾーンは以下マニュアルページを参照ください。
    [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

日本語環境でご利用する場合は以下コマンドとなります。

```bash
docker compose run --rm codedefiner _rds /l "ja" /z "Asia/Tokyo"
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力してください。

なお、バージョン1.4.8以降では、"Enterprise Edition" である旨のメッセージが表示されますので、確認してください。  
※ライセンス情報のLicenseeは利用するCLIによって文字化けする可能性があります。

![CodeDefinerのログ。Enterprise Editionと表示されている](https://pleasanter.org/files/images/ja/products-info/enterprise-edition/columns-expansion/assets/1a14f2b00aff494ba0db8bf59425eb76.png)

また、バージョン1.4.8以降では、CodeDefiner実行時に項目拡張の使用数削減が起こる場合、エラーメッセージ「 Configurator.CheckColumnsShrinkage: The columns will be shrinked.」が表示されて終了し、CodeDefinerは実行されません。エラーとなった場合は下図のように削減する項目が表示されますので、パラメータファイルおよびライセンスが正しく適用されているか再度確認ください。

![項目の削減が発生してCodeDefinerがエラー終了したログ](https://pleasanter.org/files/images/ja/products-info/enterprise-edition/columns-expansion/assets/6a38ec6af5124fa99233eb0b2dc2f87e.png)

バージョン1.4.8以降で項目の削減を許容する場合は、引数「/f」を指定して、実行してください。

```bash
docker compose run --rm codedefiner _rds /l "ja" /z "Asia/Tokyo" /f
```

### 6. 項目拡張の確認

<div class="steps" markdown>

1. 以下コマンドを実行し、項目が追加されたコンテナの再作成・再起動を行います。

    ```bash
    docker compose up -d pleasanter
    ```

2. ブラウザでアクセスし、ログインします。

    -   <http://localhost:50001>

3. プリザンターにログインし、任意のテーブルを開き、ナビゲーションメニューの「管理」－「[テーブルの管理](../../../managers-guide/manage-table/index.md)」より「[エディタ](../../../managers-guide/manage-table/editor/index.md)」タブにて、選択肢一覧のリストに拡張した項目（分類001、数値001等）が表示されることを確認してください。

</div>

## 関連情報

-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../../../setup/installation/prerequisites/codedefiner-changed-steps.md)
-   [ダウンロードセンター](https://pleasanter.org/dlcenter)
-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
