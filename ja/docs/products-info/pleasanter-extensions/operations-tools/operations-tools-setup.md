---
title: Windows/Linux/Azure
category: 運用支援ツール
order: '2000'
status: ''
parts: ''
urlstring: operations-tools-setup
translationKey: operations-tools-setup
shortname: Pleasanter Extensions,Operations Tools,セットアップ
created: 2025-01-27
updated: 2026-08-18
---

## 概要

[Operations Tools](operations-tools-common-export.md)のセットアップおよび起動手順を説明します。

## 制限事項

-   [x] SQL Serverの互換性レベルは130以上が必要です。

    ??? note "互換性レベルとは"
        互換性レベルについては、下記公式ページを参照すてください。

        [https://learn.microsoft.com/ja-jp/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-ver16](https://learn.microsoft.com/ja-jp/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-ver16)

## 操作手順

### 1. ver.1.0.0からバージョンアップする場合

!!! note
    バージョンアップではなく新規セットアップを行う場合は、「2. 実行ファイルの配置」に進んでください。

ver.1.0.0では本ソフトウェアのパフォーマンス向上のため、Syslogsテーブルにインデックスを付与する手順となっていましたが、ver.1.1.0では表示データを中間テーブルに保持する仕様になったことでパフォーマンスが向上し、インデックスが不要となりました。そのため、ここではver.1.0.0で付与したインデックスの削除方法を説明します。

!!! warning
    作業前にデータベースのバックアップを取得することを推奨します。下記の作業後、プリザンターのバージョンアップ時にCodeDefinerを実行する場合は、[パラメータ設定：Rds.json](../../../setup/parameters/rds-json.md)のDisableIndexChangeDetectionを必ずtrue（既定値）に設定してください。falseとなっている場合はSyslogsテーブルが再作成（Migrate）され、レコード件数が多い場合はCodeDefinerの処理に時間がかかることがあります。

dbowner権限（[パラメータ設定：Rds.json](../../../setup/parameters/rds-json.md)を参照）のユーザでデータベースに接続後、インデックスを削除します。

=== "SQL Serverの場合"

    1. Syslogsテーブルからインデックスを削除します。

        ``` sql
        drop index idx_eot_Method on SysLogs;
        drop index idx_eot_CreatedTime on SysLogs;
        ```

    2. コミットします。

        ``` sql
        commit;
        ```

=== "PostgreSQLの場合"

    1. Syslogsテーブルからインデックスを削除します。

        ``` sql
        drop index idx_eot_Method;
        drop index idx_eot_CreatedTime;
        ```

    2. コミットします。

        ``` sql
        commit;
        ```

### 2. 実行ファイルの配置

<div class="steps" markdown>

1.  [Operations ToolsのReleasesページ](https://github.com/Implem/Implem.OperationsTools/releases)よりダウンロードした「OperationsTools_x.x.x.zip」に「ExtendedLibraries」「wwwroot」が存在することを確認します。
1.  プリザンターのサービスを停止します。
1.  プリザンターが稼働している環境で下記ディレクトリに移動します。

    === "Windows環境"

        ``` text
        C:\web\pleasanter\Implem.Pleasanter
        ```

    === "Linux環境"

        ``` text
        /web/pleasanter/Implem.Pleasanter
        ```

    === "Azure環境"

        ``` text
        C:\home\site\wwwroot
        ```

1.  「OperationsTools_x.x.x.zip」の「ExtendedLibraries」「wwwroot」をGUI操作またはコマンド実行で配置します。Windows環境の場合、配置結果は以下のようになります。

    ``` text
    C:\web\pleasanter\Implem.Pleasanter\
    　├ App_Data\
    　└ ExtendedLibraries\　★配置
    　　└ OperationsTools\
    　├ Libraries\
    　├ runtimes\
    　├ Views\
    　└ wwwroot\
    　　├ bundles\
    　　├ content\
    　　├ images\
    　　├ operations-tools\　★配置
    　　├ scripts\
    　　└ styles\
    ```

    !!! note
        Linux環境またはAzure環境の場合は後述の補足ページを参考に作業を実施してください。

1.  下記ディレクトリのGeneral.jsonを任意のエディタで開きます。**プリザンターのパラメータ設定ファイルにも同名のファイルがあります。間違えないように注意してください。**

    === "Windows環境"

        ``` text
        C:\web\pleasanter\Implem.Pleasanter\ExtendedLibraries\OperationsTools\App_Data\Parameters\General.json
        ```

    === "Linux環境"

        ``` text
        /web/pleasanter/Implem.Pleasanter/ExtendedLibraries/OperationsTools/App_Data/Parameters/General.json
        ```

    === "Azure環境"

        ``` text
        C:\home\site\wwwroot\ExtendedLibraries\OperationsTools\App_Data\Parameters\General.json
        ```

1.  Operations Toolsを利用できるユーザのログインIDをLogin.Usersに配列形式で指定します。

    ``` json title="General.json：修正前" linenums="1" hl_lines="4"
    {
       "SetupPassword": "operations-tools",
        "Login": {
            "Users": [ "Administrator" ]
        },
        "PageSize": 50,
        "SQLCommandTimeout": 240,
        "DefaultParametersDir": "DefaultParameters"
    }
    ```

    ``` json title="General.json：修正後" linenums="1" hl_lines="4"
    {
       "SetupPassword": "operations-tools",
        "Login": {
            "Users": [ "Administrator", "AdminUser1", "AdminUser2" ]
        },
        "PageSize": 50,
        "SQLCommandTimeout": 240,
        "DefaultParametersDir": "DefaultParameters"
    }
    ```

1.  ご利用中のプリザンターのバージョンにおける変更前のパラメータJSONファイルをDefaultParametersフォルダ配下に配置してください。

    ``` text title="配置場所の例"
    C:\web\pleasanter\Implem.Pleasanter\ExtendedLibraries\OperationsTools\App_Data\
    　└ DefaultParameters\
    　　├ Api.json　★配置
    　　├ Authentication.json　★配置
    　　├ ・・・
    ```

    !!! note
        DefaultParametersフォルダ配下に配置することで、後述のパラメータ一覧画面で差分を比較することができます。

        変更前のパラメータJSONファイルがお手元にない場合は、GitHubのリリース用ページからダウンロードして取得してください。  
        https://github.com/Implem/Implem.Pleasanter/releases

1.  プリザンターのサービスを開始します。

    !!! note
        Operations Toolsのバージョンアップをする際は、プリザンターをサービス停止後に「ExtendedLibraries」「wwwroot/operations-tools」を削除してから上記1～8の手順を実施してください。

</div>

#### パラメータ：General.jsonについて

共通設定に関するパラメータです。各パラメータの説明は以下のとおりです。

| パラメータ名         | 値                  | 説明                                                               |
| -------------------- | ------------------- | ------------------------------------------------------------------ |
| SetupPassword        | operations-tools    | セットアップ時に入力するパスワードを指定。                         |
| Login.Users          | [ "Administrator" ] | Operations Toolsを利用できるユーザのログインIDを配列形式で指定。   |
| PageSize             | 50                  | ページ送りの既定値を指定。                                         |
| SQLCommandTimeout    | 240                 | SQLコマンドのタイムアウト時間を秒単位で指定。                      |
| DefaultParametersDir | DefaultParameters   | 変更前のパラメータ配置ディレクトリを指定。（パラメータ一覧画面用） |

#### パラメータ：BackgroundService.jsonについて

データ表示用の中間テーブルをバックグラウンドで同期する処理に関するパラメータです。各パラメータの説明は以下のとおりです。

| パラメータ名                         | 値                   | 説明                                                          |
| ------------------------------------ | -------------------- | ------------------------------------------------------------- |
| IntermediateTableSynchronize.Enable  | true                 | バックグラウンド処理の有効化/無効化をtrue/falseで指定します。 |
| IntermediateTableSynchronize.RunTime | [ "00:00", "12:00" ] | バックグラウンド処理を実行する時間を配列形式で指定します。    |

#### 補足：Linux環境の場合

Linux環境の場合は下記の手順を参考にしてください。（Windowsのローカル環境から実施する場合を想定）

<div class="steps" markdown>

1. 下記コマンドでプリザンターのサービスを停止します。

    ``` bash
    sudo systemctl stop pleasanter
    ```

1. 実行ファイル「ExtendedLibraries」「wwwroot」をそれぞれzipで圧縮します。
1. WinSCPなどのツールで「/web/pleasanter/Implem.Pleasanter」にバイナリでアップロードします。
1. 下記コマンドでディレクトリを移動します。

    ``` bash
    cd /web/pleasanter/Implem.Pleasanter
    ```

1. 下記コマンドでzipファイル「ExtendedLibraries.zip」を展開します。

    ``` bash
    sudo unzip -q -d /web/pleasanter/Implem.Pleasanter ExtendedLibraries.zip
    ```

1. 下記コマンドでzipファイル「wwwroot.zip」を展開します。

    ``` bash
    sudo unzip -q -d /web/pleasanter/Implem.Pleasanter wwwroot.zip
    ```

1. ディレクトリ「ExtendedLibraries」配下の所有者を変更します。

    ``` bash
    sudo chown -R <プリザンターを起動するユーザ> /web/pleasanter/Implem.Pleasanter/ExtendedLibraries
    ```

1. ディレクトリ「wwwroot/operations-tools」配下の所有者を変更します。

    ``` bash
    sudo chown -R <プリザンターを起動するユーザ> /web/pleasanter/Implem.Pleasanter/wwwroot/operations-tools
    ```

1. 下記コマンドでプリザンターのサービスを開始します。

    ``` bash
    sudo systemctl start pleasanter
    ```

</div>

#### 補足：Azure環境の場合

Azure環境の場合は下記の手順を参考にしてください。

<div class="steps" markdown>

1.  App Serviceを停止します。
1.  実行ファイル「ExtendedLibraries」「wwwroot」をそれぞれzipで圧縮します。
1.  AzureのKuduを開き、「C:\home\site\wwwroot>」に移動します。
1.  zipファイル「ExtendedLibraries.zip」をドラッグ＆ドロップでアップロードします。

    ![Azure の Kudu で ExtendedLibraries.zip をアップロードするところ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/972c8a6c3c8443599748abf96351654e.png)

1.  zipファイル「wwwroot.zip」をドラッグ＆ドロップでアップロードします。

    ![Azure の Kudu で wwwroot.zip をアップロードするところ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/7ef51c068eaf4b4282e848c48fff65df.png)

1.  App Serviceを開始してプリザンターを起動します。

</div>

### 3. セットアップの実行

<div class="steps" markdown>

1.  下記URLにアクセスします。

    ``` text
    http://{プリザンターのパス}/operations-tools/admin
    ```

    ![Operations Tools の管理ページ。セットアップのパスワードを入力する](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/14180cf6830b48b9a42e7810650731db.png)

1.  パスワードを入力し、セットアップボタンをクリックします。

    !!! note
        パスワードはGeneral.jsonで設定したSetupPasswordの値（初期値は「operations-tools」）です。

1. メッセージ「セットアップの処理中です。しばらくお待ち下さい。」が表示されます。

    ![「セットアップの処理中です。しばらくお待ち下さい。」というメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/204c932c438c4883968f18cbdf8e1d11.png)

1. メッセージ「セットアップが完了しました。」が表示されたらセットアップは完了です。

    ![「セットアップが完了しました。」というメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/4ec5f162845f4bc982d6bde55777905c.png)

    !!! note
        上記操作によりOperations Tools用のテーブル一式（プレフィックスが「_eot」のテーブル）が作成されます。

    !!! note
        一部の画面の表示データはセットアップを実施したタイミングで中間テーブルに作成され、Operations ToolsのパラメータBackgroundService.jsonのIntermediateTableSynchronize.RunTimeで指定した時間にバックグラウンドで同期されます。直近のデータを見たい場合などは「表示データを最新化」ボタンを押下してデータを手動で同期してください。

</div>

## トラブルシューティング

**Q1.** 管理ページの画面にアクセスした際、以下のように「ライセンスファイルが正しく設定されていないか、またはライセンスファイルが無効です。」のメッセージが表示される。

![ライセンスファイルが正しく設定されていないことを示すエラーメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/fcab9662f9794eb1b2fe7d95a2c559b3.png)

**A1.** プリザンター本体に有効なライセンスファイルが配置されていることを確認してください。

---

**Q2.** 一部の画面について明細情報などの結果が表示されない。

**A2.** 対象環境のデータ量によってはセットアップ処理がタイムアウトで中断されることにより、一部画面の結果が表示されないことがあります。その場合は、以下の手順をお試しください。

1.  Operations Tools用のパラメータファイル：General.jsonの"SQLCommandTimeout"について値を調整してください。

    ``` json title="General.json" linenums="1" hl_lines="7"
    {
       "SetupPassword": "operations-tools",
        "Login": {
            "Users": [ "Administrator", "AdminUser1", "AdminUser2" ]
        },
        "PageSize": 50,
        "SQLCommandTimeout": 240,  <-- 値を調整する
        "DefaultParametersDir": "DefaultParameters"
    }
    ```

1.  プリザンターを再起動します。
1.  Operations Toolsの管理ページ画面から「表示データを最新化」ボタンをクリックします。
1.  [_eot_JobHistory]テーブルのログを確認し、Status, ErrMessage, ErrStackTraceの内容を確認します。  
    （Statusが'Success'となっており、ErrMessage, ErrStackTraceがブランクとなっていれば成功です。）

## 関連情報

-   [Operations Tools：共通機能：エクスポート](operations-tools-common-export.md)
-   [パラメータ設定：Rds.json](../../../setup/parameters/rds-json.md)
-   [Operations ToolsのReleasesページ](https://github.com/Implem/Implem.OperationsTools/releases)
