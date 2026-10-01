---
title: Community EditionからEnterprise Editionへのアップグレード手順
category: 初回導入手順
order: '100'
status: ''
parts: ''
urlstring: enterprise-edition-upgrade
translationKey: enterprise-edition-upgrade
shortname: Enterprise Edition,アップグレード
created: 2025-01-24
updated: 2026-06-10
---

## 概要

プリザンターをCommunity EditionからEnterprise Editionへアップグレードする手順について説明します。

本手順はインストーラまたは手動でセットアップした環境を対象としています。Dockerを利用している場合は、以下の各ページを参照してください。

-   [Community EditionからEnterprise Editionへのアップグレード手順(Docker利用)](enterprise-edition-upgrade-docker.md)
-   [Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにMySQLを利用）](enterprise-edition-upgrade-docker-mysql.md)
-   [Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにPostgreSQLを利用）](enterprise-edition-upgrade-docker-postgresql.md)
-   [Community EditionからEnterprise Editionへのアップグレード手順（Docker利用／DBにSQL Serverを利用）](enterprise-edition-upgrade-docker-sqlserver.md)

## 注意事項

Enterprise Editionにアップグレードすると以下の動作となります。

1.  ライセンスが商用ライセンスになります。ナビゲーションメニューの「ヘルプ」－「バージョン」にて確認できます。
1.  分類項目、数値項目などの各項目の利用数を拡張することができます。
1.  契約した年間サポートサービスプランに応じてユーザ登録数の上限が設定され、上限を超えてユーザを登録することができません。
1.  Pleasanter Extensions（Site Visualizer、Code Assist、Operations Tools、Development Tools）が利用可能になります。

データベースにMySQLを使用する場合はPleasanter Extensionsの利用に制限がございます。詳細は「[データベースによる制限事項](../../limitations-database.md)」を参照してください。

## 操作手順

### プリザンターの準備

既にCommunity Editionとしてご利用中のプリザンターをEnterprise Editionにアップグレードする場合は「プリザンターのバージョンアップ」を実施してください。  
プリザンターの新規インストールと合わせてEnterprise Editionにアップグレードする場合は「[プリザンターのインストール](../../../setup/installation/index.md)」を実施してください。

#### プリザンターのバージョンアップ

アップグレードの前に弊社オンラインマニュアルの手順にそってバージョンアップを実施してください。

-   [Pleasanter ユーザーマニュアル - バージョンアップ(インストーラ)](../../../setup/version-up-migration/version-up-installer/index.md)
-   [Pleasanter ユーザーマニュアル - バージョンアップ](../../../setup/version-up-migration/version-up-manually/index.md)

#### プリザンターのインストール

弊社オンラインマニュアルの手順にそってプリザンターをインストールし、ログイン画面が表示することを確認してください。

-   [Pleasanter ユーザーマニュアル - セットアップ](../../../setup/installation/index.md)

### ライセンスファイルの格納

<div class="steps" markdown>

1.  プリザンターを停止します。

    === ":fontawesome-brands-windows: Windows環境"

        1.  インターネットインフォメーションサービス（IIS）マネージャを開きます。
        1.  左ペインより、「サイト」-「Default Web Site」を選択して、右ペインの「停止」をクリックします。

    === ":fontawesome-brands-linux: Linux環境"

        1.  以下コマンドを実行します。

            ``` bash
            sudo systemctl stop pleasanter
            ```

    === ":material-microsoft-azure: Azure App Service環境"

        1.  App Serviceを開き「停止」をクリックします。

1.  ライセンスパックに含まれる「Implem.License.dll」をご利用中の環境に応じて以下フォルダにそれぞれ上書きコピーしてください。

    === ":fontawesome-brands-windows: Windows環境"

        -   C:\web\pleasanter\Implem.Pleasanter
        -   C:\web\pleasanter\Implem.CodeDefiner

    === ":fontawesome-brands-linux: Linux環境"

        -   /web/pleasanter/Implem.Pleasanter
        -   /web/pleasanter/Implem.CodeDefiner

    === ":material-microsoft-azure: Azure App Service環境"

        -   C:\home\site\wwwroot\
        -   C:\home\site\CodeDefiner

    上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。

</div>

### アップグレードの確認

<div class="steps" markdown>

1.  プリザンターを起動します。

    === ":fontawesome-brands-windows: Windows環境"

        1.  インターネットインフォメーションサービス（IIS）マネージャを開きます。
        1.  左ペインより、「サイト」-「Default Web Site」を選択して、右ペインの「開始」をクリックします。

    === ":fontawesome-brands-linux: Linux環境"

        1.  以下コマンドを実行します。

        ``` bash
        sudo systemctl start pleasanter
        ```

    === ":material-microsoft-azure: Azure App Service環境"

        1.  App Serviceを開き「開始」をクリックします。

1.  プリザンターにログインし、ナビゲーションメニューの「ヘルプ」－「バージョン」より以下を確認してください。

    -   ライセンスが「商用ライセンス」となっていること
    -   ライセンス期限が正しいこと
    -   使用者が正しいこと

</div>

### 項目拡張作業

Community Editionでは[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB         | Enterprise Editionで利用できる項目の上限 |
| ---------- | ---------------------------------------- |
| SQL Server | 6つの項目種別の合計で最大900個まで       |
| PostgreSQL | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]  | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

項目拡張を行う場合は[項目拡張](../columns-expansion/enterprise-edition-columns-expansion-1.4.8.md)の手順に沿って作業を行ってください。

## 関連情報

-   [Pleasanter ユーザーマニュアル - バージョンアップ(インストーラ)](../../../setup/version-up-migration/version-up-installer/index.md)
-   [Pleasanter ユーザーマニュアル - バージョンアップ](../../../setup/version-up-migration/version-up-manually/index.md)
-   [Pleasanter ユーザーマニュアル - セットアップ](../../../setup/installation/index.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [項目拡張手順（ver.1.4.8以降）](../columns-expansion/enterprise-edition-columns-expansion-1.4.8.md)
