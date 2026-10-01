---
title: ライセンス更新手順
category: ライセンス更新手順
order: '200'
status: ''
parts: ''
urlstring: enterprise-edition-renew-license
translationKey: enterprise-edition-renew-license
shortname: Enterprise Edition,ライセンス更新
created: 2025-01-24
updated: 2025-02-14
---

## 概要

年間サポートサービスの契約更新を行いEnterprise Editionの利用期限を延長された場合は、本手順にそってライセンスファイルを更新してください。

## 制限事項

1.  ライセンスファイルの期限が過ぎると以下の動作となります。
    1. ライセンスがAGPL（GNU AFFERO GENERAL PUBLIC LICENSE）に戻ります。
    1. 項目拡張していた場合、拡張した項目が非表示となります。ただしデータベース上のデータは保存済みのままです。
    1. ユーザ登録数の上限が解除されます。
    1. Pleasanter Extensions（Development Tools、Operations Tools）が利用不可となります。

## 前提条件

1.  本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

### 1. ライセンスファイルの格納

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

        C:\web\pleasanter\Implem.Pleasanter
        C:\web\pleasanter\Implem.CodeDefiner

    === ":fontawesome-brands-linux: Linux環境"

        /web/pleasanter/Implem.Pleasanter
        /web/pleasanter/Implem.CodeDefiner

    === ":material-microsoft-azure: Azure App Service環境"

        C:\home\site\wwwroot\
        C:\home\site\CodeDefiner

</div>

上記パスは弊社オンラインマニュアルの手順に従ってインストールした場合のものになります。ご利用中の環境に応じて適宜読み替えてください。

### 2. アップグレードの確認

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
    - ライセンスが「商用ライセンス」となっていること
    - ライセンス期限が正しいこと（2月末までのライセンスの場合、3/1と表示されます）
    - 使用者が正しいこと

</div>

### 3. 項目拡張作業

Community Editionでは[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を拡張することができます。

| DB         | Enterprise Editionで利用できる項目の上限 |
| ---------- | ---------------------------------------- |
| SQL Server | 6つの項目種別の合計で最大900個まで       |
| PostgreSQL | 6つの項目種別の合計で最大900個まで       |
| MySQL[^1]  | 6つの項目種別の合計で最大256個まで       |

[^1]: MySQLはver1.4.9.0以降のプリザンターで使用できます。

ライセンス更新と合わせて項目拡張の増減を行う場合は[項目拡張](../columns-expansion/enterprise-edition-columns-expansion-1.4.8.md)の手順に沿って作業を行ってください。

## 関連情報

-   [サイト機能](../../../users-guide/site/index.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [項目拡張手順（ver.1.4.8以降）](../columns-expansion/enterprise-edition-columns-expansion-1.4.8.md)
