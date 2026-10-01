---
title: プリザンターのログを確認したい
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-view-syslogs
translationKey: faq-view-syslogs
shortname: SysLogsテーブル
created: 2019-03-20
updated: 2025-01-30
---

## 回答

1.  [システムログの管理](../../managers-guide/system-log-administration/index.md)を使用
1.  SQLを実行。

---

## 概要

プリザンターの[システムログ](../../managers-guide/system-log-administration/index.md)を確認・取得する手順です。

## 注意事項

1.  データベースを直接操作してログ取得を行う場合、事前に[バックアップ](../backup-restore/faq-backup-and-restore.md)を取得することを強く推奨いたします。

## 操作手順

### システムログ管理機能

#### パラメータ変更

システムログ管理機能は特権ユーザのみ使用可能なため、パラメータ設定を編集します。

1.  App_Data/Parameters/Security.jsonを開きます。
1.  「PrivilegedUsers」パラメータに特権ユーザ(ログインID)を指定して保存します。パラメータの指定方法につきましては下記マニュアルを確認してください。

    -   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)

1.  プリザンターを再起動します。

#### ログ取得

1.  特権ユーザでプリザンターにログインします。
1.  「管理」メニューを開き[システムログの管理](../../managers-guide/system-log-administration/index.md)をクリックします。
1.  フィルタで条件を設定し、[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)ボタンをクリックします。
1.  設定した条件でレコード(ログ)が表示されることを確認します。
1.  画面下部の[エクスポート](../../developers-guide/api/table-operations/api-export.md)ボタンをクリックします。

### SQL Server

1.  プリザンターをインストールしているサーバにログインします。
1.  SSMS（SQL Server Management Studio）を起動します。
1.  「オブジェクトエクスプローラ」から「データベース」を展開して「Implem.Pleasanter」を選択します。
1.  「Implem.Pleasanter」を右クリックし、「新しいクエリ」をクリックします。
1.  下記SQLを実行し[SysLogsテーブル](faq-contents-of-syslogs.md)のデータを取得します。

    === "直近の1000件を取得する"

        ``` sql
        select top 1000 * from "SysLogs" order by "CreatedTime" desc;
        ```

    === "特定の期間のログを取得する"

        ``` sql
        select * from "SysLogs" where "CreatedTime" between '2021/07/01 00:00:00' and '2021/07/02 00:00:00'
        ```

1.  結果ウィンドウの左上をクリックし、結果を全選択します。
1.  上記の選択部分を右クリックして、「結果に名前を付けて保存」をクリックします。
1.  出力結果(CSV)を保存します。

### PostgreSQL

### ①PSQLによるログ取得

1.  プリザンターをインストールしているサーバにログインします。
1.  postgresユーザに切り替えます。

    ```
    su - postgres
    ```

1.  下記のpsqlコマンドを実行し[SysLogsテーブル](faq-contents-of-syslogs.md)のデータを取得します。

    #### 直近の1000件を取得する場合

    ``` sql
    psql -d "Implem.Pleasanter" \
         -U postgres \
         -c "select * from \"SysLogs\" order by \"CreatedTime\" desc limit 1000;" -A -F, \
    > /web/syslogs.csv
    ```

    #### 特定の期間のログを取得する場合

    ``` sql
    psql -d "Implem.Pleasanter" \
         -U postgres \
         -c "select * from \"SysLogs\" \
                      where \"CreatedTime\" \
                      between '2022/02/08 00:00:00' and '2022/02/09 00:00:00' \
                      order by \"CreatedTime\" \
                      desc;" -A -F, \
    > /web/syslogs.csv
    ```

1.  /web/syslogs.csv に出力されるCSVを保存します。

### ②pgAdminを用いたログ取得

1.  pgAdminを起動します。
1.  プリザンターのデータベースに接続します。
1.  Object Explorerで「サーバ名 > データベース > Implem.Pleasanter」を右クリックし、「クエリツール」をクリックします。

    ![pgAdmin の Object Explorer から「クエリツール」を開くところ](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/b322999df47040f58b3221fea041b37f.png)

1.  以下のSQLを実行します。

    === "直近の1000件を取得する"

        ``` sql
        select * from "Implem.Pleasanter"."SysLogs" \
                 order by "CreatedTime" \
                 desc \
                 limit 1000;
        ```

    === "特定の期間のログを取得する"

        ``` sql
        select * from "Implem.Pleasanter"."SysLogs" \
                 where "CreatedTime" \
                 between '2022/02/08 00:00:00' and '2022/02/09 00:00:00' \
                 order by "CreatedTime" \
                 desc \
                 limit 1000;
        ```

1.  下図のデータ出力の赤枠部分をクリックし、出力結果(CSV)を保存します。

    ![pgAdmin のデータ出力。CSVを保存する箇所を赤枠で示している](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/d78ac30db78b48ba80461a920dd2d866.png)

## ログの内容

[SysLogsテーブル](faq-contents-of-syslogs.md)の内容につきましては、[FAQ：システムログ(SysLogsテーブル)の内容について](faq-contents-of-syslogs.md)を参照してください。

## 関連情報

-   [システムログ管理機能](../../managers-guide/system-log-administration/index.md)
-   [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](../backup-restore/faq-backup-and-restore.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../developers-guide/api/table-operations/api-export.md)
-   [FAQ：システムログ(SysLogsテーブル)の内容について](faq-contents-of-syslogs.md)
