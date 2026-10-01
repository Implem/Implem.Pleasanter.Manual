---
title: Docker
category: 運用支援ツール
order: '2001'
status: ''
parts: ''
urlstring: operations-tools-setup-docker
translationKey: operations-tools-setup-docker
shortname: ''
created: 2025-05-08
updated: 2026-07-17
---

## Docker版プリザンターについて

Docker Hubで公開されているプリザンターの公式Dockerイメージを利用する手順です。

implem/pleasanter - Docker Image | Docker Hub  
https://hub.docker.com/r/implem/pleasanter

## 概要

[Operations Tools](operations-tools-common-export.md)のセットアップおよび起動手順を説明します。

## 制限事項

1. Operations ToolsはMySQLではご利用いただけません。

## 前提条件

1. 本手順はプリザンターをEnterprise Editionにアップグレードしていることを前提とします。

## 操作手順

### 1. 資源の配置

<div class="steps" markdown>

1. [Operations ToolsのReleasesページ](https://github.com/Implem/Implem.OperationsTools/releases)よりダウンロードした「OperationsTools_x.x.x.zip」を解凍します。

2. フォルダ「OperationsTools_x.x.x」のフォルダ名を「OperationsTools」に変更し、以下のフォルダ構成とします。

    ```text
    .
    +-- OperationsTools
        +-- ExtendedLibraries
        +-- wwwroot
    ```

3. 以下コマンドを実行し、コンテナを停止します。

    ```text
    docker compose stop
    ```

4. 「OperationsTools」フォルダをコンテナの基準フォルダの配下（「Pleasanter」フォルダや[CodeDefiner](../../../setup/codedefiner/codedefiner-command.md)フォルダと同じ配置先）に配置します。

5. 「\OperationsTools\ExtendedLibraries\OperationsTools\App_Data\Parameters\General.json」を任意のエディタで開きます。

6. Operations Toolsを利用できるユーザのログインIDをLogin.Usersに配列形式で指定します。

    例）  
    General.json：修正前
    ```json
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

    General.json：修正後
    ```json
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

    ※OperationsToolsのパラメータファイルの詳細は後述の補記「パラメータ：General.jsonについて」および「パラメータ：BackgroundService.jsonについて」を参照してください。

7. ご利用中のプリザンターのバージョンにおける既定のパラメータJSONファイル（**全てのファイル**）を「\OperationsTools\ExtendedLibraries\OperationsTools\App_Data\DefaultParameters」フォルダ配下に配置してください。  

    ``` text
    配置場所の例：
    \OperationsTools\ExtendedLibraries\OperationsTools\App_Data\
    　└ DefaultParameters\
    　　├ Api.json　★配置
    　　├ Authentication.json　★配置
    　　├ ・・・　★全パラメータファイルを配置
    ```

    > **Note**  
    > DefaultParametersフォルダ配下に配置することで、後述のパラメータ一覧画面で差分を比較することができます。  
    > 
    > 変更前のパラメータJSONファイルがお手元にない場合は、GitHubのリリース用ページからダウンロードして取得してください。  
    > https://github.com/Implem/Implem.Pleasanter/releases  

8. 「\Pleasanter\Dockerfile」を任意のテキストエディタで開き、以下の内容に修正します。

    ```text
    ARG VERSION=latest
    FROM implem/pleasanter:${VERSION}

    COPY app_data_parameters/ App_Data/Parameters/
    COPY OperationsTools/ExtendedLibraries/ ExtendedLibraries/
    COPY OperationsTools/wwwroot/operations-tools wwwroot/operations-tools/
    COPY Implem.License.dll .
    ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
    ```

    > **Note**  
    > Operations Toolsのバージョンアップをする際は、コンテナ停止後に「\OperationsTools」フォルダを削除してから上記1～8の手順を実施してください。

</div>

#### パラメータ：General.jsonについて

共通設定に関するパラメータです。各パラメータの説明は以下のとおりです。  

| パラメータ名               | 値                   | 説明                                        |
|----------------------|---------------------|-------------------------------------------|
| SetupPassword        | operations-tools    | セットアップ時に入力するパスワードを指定。                     |
| Login.Users          | [ "Administrator" ] | Operations Toolsを利用できるユーザのログインIDを配列形式で指定。 |
| PageSize             | 50                  | ページ送りの既定値を指定。                             |
| SQLCommandTimeout    | 240                 | SQLコマンドのタイムアウト時間を秒単位で指定。                  |
| DefaultParametersDir | DefaultParameters   | 変更前のパラメータ配置ディレクトリを指定。（パラメータ一覧画面用）                  |

#### パラメータ：BackgroundService.jsonについて

データ表示用の中間テーブルをバックグラウンドで同期する処理に関するパラメータです。各パラメータの説明は以下のとおりです。  

| パラメータ名                               | 値                    | 説明                             |
|--------------------------------------|----------------------|--------------------------------|
| IntermediateTableSynchronize.Enable  | true                 | バックグラウンド処理の有効化/無効化をtrue/falseで指定します。 |
| IntermediateTableSynchronize.RunTime | [ "00:00", "12:00" ] | バックグラウンド処理を実行する時間を配列形式で指定します。 |

### 2. コンテナイメージのビルドおよび起動

<div class="steps" markdown>

1. 以下コマンドを実行し、コンテナイメージをビルドします。

    ```text
    docker compose build
    ```

2. 以下コマンドを実行し、OperationsToolsの資源を含むプリザンターのコンテナを再作成・再起動します。

    ```text
    docker compose up -d pleasanter
    ```

3. 下記URLにアクセスします。

    ```text
    http://localhost:50001/operations-tools/admin
    ```

    ![Operations Tools の管理ページ。セットアップのパスワードを入力する](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/14180cf6830b48b9a42e7810650731db.png)

2. パスワードを入力し、セットアップボタンをクリックします。

    > **Note**  
    > パスワードはGeneral.jsonで設定したSetupPasswordの値（初期値は「operations-tools」）です。

3. メッセージ「セットアップの処理中です。しばらくお待ち下さい。」が表示されます。
    ![「セットアップの処理中です。しばらくお待ち下さい。」というメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/204c932c438c4883968f18cbdf8e1d11.png)

4. メッセージ「セットアップが完了しました。」が表示されたらセットアップは完了です。

</div>
![「セットアップが完了しました。」というメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/4ec5f162845f4bc982d6bde55777905c.png)

    > **Note**  
    > 上記操作によりOperations Tools用のテーブル一式（プレフィックスが「_eot」のテーブル）が作成されます。

    > **Note**  
    > 一部の画面の表示データはセットアップを実施したタイミングで中間テーブルに作成され、Operations ToolsのパラメータBackgroundService.jsonのIntermediateTableSynchronize.RunTimeで指定した時間にバックグラウンドで同期されます。直近のデータを見たい場合などは「表示データを最新化」ボタンを押下してデータを手動で同期してください。

### トラブルシューティング

Q. 管理ページの画面にアクセスした際、以下のように「ライセンスファイルが正しく設定されていないか、またはライセンスファイルが無効です。」のメッセージが表示される。

![ライセンスファイルが正しく設定されていないことを示すエラーメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/fcab9662f9794eb1b2fe7d95a2c559b3.png)

A. プリザンター本体に有効なライセンスファイルが配置されていることを確認してください。

---

Q. 一部の画面について明細情報などの結果が表示されない。

A. 対象環境のデータ量によってはセットアップ処理がタイムアウトで中断されることにより、一部画面の結果が表示されないことがあります。その場合は、以下の手順をお試しください。

＜手順＞

<div class="steps" markdown>

1. コンテナを停止します。

    ```text
    docker compose stop
    ```

2. Operations Tools用のパラメータファイル：General.jsonの"SQLCommandTimeout"について値を調整してください。  

    ```json
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

3. 以下コマンドを実行します。

    ```text
    docker compose build
    ```

4. 以下コマンドを実行します。

    ```text
    docker compose up -d pleasanter
    ```

5. Operations Toolsの管理ページ画面から「表示データを最新化」ボタンをクリックします。

6. [_eot_JobHistory]テーブルのログを確認し、Status, ErrMessage, ErrStackTrace の内容を確認します。  

</div>
（Statusが'Success'となっており、ErrMessage, ErrStackTraceがブランクとなっていれば成功です。）

## 関連情報

-   [Operations Tools：共通機能：エクスポート](operations-tools-common-export.md)
-   [Operations ToolsのReleasesページ](https://github.com/Implem/Implem.OperationsTools/releases)
-   [CodeDefinerのコマンド一覧](../../../setup/codedefiner/codedefiner-command.md)
