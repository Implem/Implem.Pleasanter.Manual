---
title: Dockerではじめる
hide:
  - navigation
translationKey: getting-started-with-docker
created: 2023-10-12
updated: 2026-07-17
---

!!! danger "Docker版プリザンターを業務に用いたいユーザ向けの注意事項"

    本マニュアルの手順は、すぐにプリザンターを試したいユーザのために簡略化されています。Docker版プリザンターを業務に用いる場合は、[正規の手順](../developers-guide/index.md)でのセットアップを強く推奨します。

## 概要

下記の設定値で環境設定を行うことで、すぐにDockerでプリザンターをはじめられる手順を説明します。

| No  | 設定内容                             | パラメータ                                                           | 設定値       | 備考                   |
| --- | ------------------------------------ | -------------------------------------------------------------------- | ------------ | ---------------------- |
| 1   | PostgreSQLのバージョン               | POSTGRES_VERSION                                                     | 17           |                        |
| 2   | PostgreSQLの管理用ユーザのパスワード | POSTGRES_PASSWORD                                                    | SetSaPWD     |                        |
| 3   | Sa接続文字列のパスワード             | Implem_Pleasanter_Rds_PostgreSQL<br>**SaConnectionString内のPWD**    | SetSaPWD     | 2と同じ値を設定        |
| 4   | Owner接続文字列のパスワード          | Implem_Pleasanter_Rds_PostgreSQL<br>**OwnerConnectionString内のPWD** | SetAdminsPWD |                        |
| 5   | User接続文字列のパスワード           | Implem_Pleasanter_Rds_PostgreSQL<br>**UserConnectionString内のPWD**  | SetUsersPWD  |                        |
| 6   | プリザンターのバージョン             | PLEASANTER_VERSION                                                   | latest       | 利用時点の最新版を取得 |
| 7   | プリザンターの言語                   | CodeDefinerの/lオプション                                            | "ja"         |                        |
| 8   | プリザンターのタイムゾーン           | CodeDefinerの/zオプション                                            | "Asia/Tokyo" |                        |

## 手順

手順の流れは以下の通りです。

1.  [Docker実行環境の準備](#1-docker)
1.  [プロジェクトディレクトリの作成と移動](#2)
1.  [ファイルの作成](#3)
1.  [CodeDefinerの実行](#4-codedefiner)
1.  [プリザンターの起動・終了](#5)

### 1. Docker実行環境の準備

利用中のOSに応じたDocker実行環境（Docker EngineやDocker Desktopなど）を準備してください。

!!! tip "Docker実行環境の準備はDocker公式マニュアルで"
    詳細は以下の[Docker公式マニュアル](https://docs.docker.com/)を参照してください。

    -   :fontawesome-brands-docker: [Docker Engine \| Docker Docs](https://docs.docker.com/engine/)
    -   :fontawesome-brands-docker: [Docker Desktop \| Docker Docs](https://docs.docker.com/desktop/)

### 2. プロジェクトディレクトリの作成と移動

以下のコマンドを実行して、任意の場所にプロジェクトディレクトリを作成し、プロジェクトディレクトリへ移動します。

``` bat
mkdir ./pleasanter
cd ./pleasanter
```

!!! tip "プロジェクトディレクトリの名前は変更可能"
    上記のコマンドではプロジェクトディレクトリ名を`pleasanter`としましたが、他の名称に変更しても問題ありません。

### 3. ファイルの作成

プロジェクトディレクトリ内に`.env`、`compose.yaml`という2つのファイルを作成します。

=== ":octicons-command-palette-16: Windows（CMD）の場合"

    ``` bat
    type nul > .env
    type nul > compose.yaml
    ```

=== ":material-powershell: Windows（PowerShell）の場合"

    ``` ps1
    New-Item .env -ItemType File -Force
    New-Item compose.yaml -ItemType File -Force
    ```

=== ":fontawesome-brands-apple: :fontawesome-brands-linux: macOSまたはLinuxの場合"

    ``` bash
    touch .env
    touch compose.yaml
    ```

#### .env

テキストエディタで`.env`を開き、以下の内容を貼り付けて保存します。

``` ini linenums="1" title="pleasanter/.env"
POSTGRES_VERSION=17
POSTGRES_VOLUMES_TARGET=/var/lib/postgresql/data
POSTGRES_USER=postgres
POSTGRES_PASSWORD=SetSaPWD
POSTGRES_DB=postgres
POSTGRES_HOST_AUTH_METHOD=scram-sha-256
POSTGRES_INITDB_ARGS="--auth-host=scram-sha-256"
PLEASANTER_VERSION=latest
Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString="Server=db;Database=postgres;UID=postgres;PWD=SetSaPWD"
Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString="Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD"
Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString="Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD"
```

#### compose.yaml

テキストエディタで`compose.yaml`を開き、以下の内容を貼り付けて保存します。

``` yaml linenums="1" title="pleasanter/compose.yml"
services:
    db:
    container_name: postgres
    image: postgres:${POSTGRES_VERSION}
    environment:
        - POSTGRES_USER
        - POSTGRES_PASSWORD
        - POSTGRES_DB
        - POSTGRES_HOST_AUTH_METHOD
        - POSTGRES_INITDB_ARGS
    volumes:
        - type: volume
        source: pg_data
        target: ${POSTGRES_VOLUMES_TARGET}
    pleasanter:
    container_name: pleasanter
    image: implem/pleasanter:${PLEASANTER_VERSION}
    depends_on:
        - db
    ports:
        - '50001:8080'
    environment:
        Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
        Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
        Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
    codedefiner:
    container_name: codedefiner
    image: implem/pleasanter:codedefiner
    depends_on:
        - db
    environment:
        Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
        Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
        Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
volumes:
    pg_data:
    name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
```

### 4. CodeDefinerの実行

プロジェクトディレクトリで、以下のコマンドでCodeDefinerを実行します。

``` bat
docker compose run --rm codedefiner _rds /y /l "ja" /z "Asia/Tokyo"
```

### 5. プリザンターの起動と終了

#### プリザンターを起動する

1.  プロジェクトディレクトリで、以下のコマンドを実行しプリザンターを起動します。

    ``` bat
    docker compose up -d pleasanter
    ```

1.  Webブラウザで[http://localhost:50001](http://localhost:50001)を開いてください。
1.  ログイン画面が表示されたら、次の各情報を入力してください。

    |  ログインID   | 初期パスワード |
    | :-----------: | :------------: |
    | Administrator |   pleasanter   |

    ![ログインIDと初期パスワードを入力するログイン画面](https://pleasanter.org/files/images/ja/getting-started/assets/a82685936a6c4b2aa5959830a9911daa.png)

1.  安全なパスワードに変更してください。

    ![パスワードを変更する画面](https://pleasanter.org/files/images/ja/getting-started/assets/03ebe82fc4ed49b7a8325414557d9a6a.png)

#### プリザンターを終了する

1.  Webブラウザを終了してください。
1.  プロジェクトディレクトリで、コンテナを停止してください。

    ``` bat
    docker compose stop
    ```

#### プリザンターをもう一度起動する

1.  プロジェクトディレクトリで、コンテナを起動してください。

    ``` bat
    docker compose start
    ```

1.  Webブラウザで[http://localhost:50001](http://localhost:50001)を開いてください。
