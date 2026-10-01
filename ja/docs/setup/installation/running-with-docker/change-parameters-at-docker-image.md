---
title: Dockerイメージを使用しパラメータを既定値から変更して起動する
category: Dockerで起動する
order: '102'
status: ''
parts: ''
urlstring: change-parameters-at-docker-image
translationKey: change-parameters-at-docker-image
shortname: Dockerで起動する
created: 2024-10-29
updated: 2026-07-17
---

## 概要

データベースにPostgreSQLを指定し、パラメータを既定値から変更して、[公式Dockerイメージ](https://hub.docker.com/r/implem/pleasanter)からプリザンターを起動する手順です。

## 制限事項

1.  ver1.4.5以前で実施する場合はCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
   [ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../prerequisites/codedefiner-changed-steps.md)
1.  本ページの手順は、プリザンターをすぐに試したいユーザのために、PostgreSQLコンテナをプリザンターと同一のDocker構成に含めた複数コンテナ構成を採用しています。この構成は**本番運用を想定したものではありません**。
1.  本番運用では、データベースコンテナが性能上のボトルネックになります。**別ホスト上のデータベース**とすることを強く推奨します。

## 前提条件

1.  本手順ではデータベースとしてPostgreSQLを使用します。他データベースを使用する手順は以下を参照してください。
    -   [Dockerイメージを使用しDBにMySQLを指定して起動する](setup-by-docker-image-and-mysql.md)
    -   [Dockerイメージを使用しDBにSQL Serverを指定して起動する](setup-by-docker-image-and-sql-server.md)
1.  本手順は、以下マニュアルの手順通りにDockerが利用できることを前提としています。
    下記マニュアルを参照し、プリザンターの公式Dockerイメージを使ってプリザンターを起動できることを確認してください。
    -   [Dockerで起動する](getting-started-pleasanter-docker.md)
1.  データベースにPostgreSQLを使用する場合[パラメータ設定：Rds.json](../../../setup/parameters/rds-json.md)の配置・編集は不要です。

## 操作手順

### 1. ファイル配置、フォルダ作成

プロジェクトディレクトリ（以下例ではpleasanter）にフォルダを以下のように構成し、ファイルを配置します。

``` text
📁pleasanter
    +-- 📁app_data_parameters
    |   +-- 📁拡張機能用フォルダ
    |   |   +-- 📄拡張機能用ファイル
    |   |  
    |   +-- 📄パラメータファイル
    |
    |-- 📄.env
    |-- 📄compose.yaml
```

| フォルダ<br>またはファイル | 説明                                                                                                                                                                                |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| app_data_parameters        | ご利用環境に合わせて設定したパラメータファイルを格納するためのフォルダ。拡張SQLや拡張スクリプトなどの拡張機能用フォルダおよび拡張機能用ファイルも必要に応じて本フォルダに格納する。 |
| .env                       | データベース接続情報などの設定情報や環境変数を記述したファイル                                                                                                                      |
| compose.yaml               | Docker Composeの設定ファイル                                                                                                                                                        |

#### 1-1. app_data_parametersフォルダの作成

1.  プロジェクトディレクトリで以下コマンドを実行し、`app_data_parameters`フォルダを作成します。

    ```bash
    mkdir ./app_data_parameters
    ```

#### 1-2. パラメータファイルの準備

1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンターをダウンロードします。特段理由がない場合は最新バージョンをダウンロードしてください。過去にリリースした特定のバージョンが必要な場合は、該当のバージョンのプリザンターをダウンロードしてください。
1.  zipファイルを任意の場所に解凍します。
1.  解凍したフォルダ内にある「`\pleasanter\Implem.Pleasanter\App_Data\Parameters`」から変更したいパラメータを1-1で作成した`app_data_parameters`フォルダ配下にコピーします。
1.  パラメータの内容を適宜変更し、更新します。
1.  拡張SQL（ExtendedSqls）や拡張スクリプト（ExtendedScripts）などの拡張機能を設定する場合は拡張機能用のフォルダを`app_data_parameters`にコピーし、コピーした各フォルダ内に拡張機能用ファイルを作成します。

#### 1-3 .envファイル

1.  以下コマンドを実行し、`.env`ファイルを作成します。

    === "Windows（コマンドプロンプト）"

        ``` bash
        type nul > .env
        ```

    === "Windows（PowerShell）"

        ``` bash
        New-Item .env -ItemType File -Force
        ```

    === "Linux、macOS"

        ``` bash
        touch .env
        ```

1.  テキストエディタで`.env`を開き、以下の内容を張り付け保存します。`{{ ... }}`はご利用環境に合わせて適宜修正してください。各設定内容については「[Dockerで起動する](getting-started-pleasanter-docker.md)」の`.env`ファイルに関する説明を参照してください。

    ``` ini title=".env" linenums="1"
    POSTGRES_VERSION={{PostgreSQL Version}}
    POSTGRES_VOLUMES_TARGET={{Volumes TargetPath}}
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD={{Sa Password}}
    POSTGRES_DB=postgres
    POSTGRES_HOST_AUTH_METHOD=scram-sha-256
    POSTGRES_INITDB_ARGS="--auth-host=scram-sha-256"
    PLEASANTER_VERSION={{Pleasanter Version}}
    Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString="Server=db;Database=postgres;UID=postgres;PWD={{Sa Password}}"
    Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString="Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}}"
    Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString="Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}}"
    ```

#### 1-4 compose.yamlファイル

1.  以下コマンドを実行し、compose.yamlファイルを作成します。

    === "Windows（コマンドプロンプト）"

        ``` bash
        type nul > compose.yaml
        ```

    === "Windows（PowerShell）"

        ``` bash
        New-Item compose.yaml -ItemType File -Force
        ```

    === "Linux、macOS"

        ``` bash
        touch compose.yaml
        ```

1.  テキストエディタで`compose.yaml`を開き、以下の内容を貼り付け保存します。

    ``` yaml title="compose.yaml" linenums="1"
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
        networks:
          - backend
        healthcheck:
          test:
            [
              "CMD-SHELL",
              "pg_isready -U $${POSTGRES_USER:-postgres} -d $${POSTGRES_DB:-postgres} || exit 1",
            ]
          interval: 10s
          timeout: 5s
          retries: 5
          start_period: 30s
        restart: unless-stopped
      param-init:
        container_name: param-init
        image: implem/pleasanter:${PLEASANTER_VERSION}
        volumes:
          - ./app_data_parameters:/tmp/app_data_parameters:ro
          - pleasanter_params:/app/App_Data/Parameters
        entrypoint:
          - sh
          - -c
          - cp -rf /tmp/app_data_parameters/. /app/App_Data/Parameters/ && echo "Parameters copied"
        restart: "no"
        network_mode: none
      param-init-codedefiner:
        container_name: param-init-codedefiner
        image: implem/pleasanter:codedefiner
        volumes:
          - ./app_data_parameters:/tmp/app_data_parameters:ro
          - codedefiner_params:/app/Implem.Pleasanter/App_Data/Parameters
        entrypoint:
          - sh
          - -c
          - cp -rf /tmp/app_data_parameters/. /app/Implem.Pleasanter/App_Data/Parameters/ && echo "Parameters copied"
        restart: "no"
        network_mode: none
      pleasanter:
        container_name: pleasanter
        image: implem/pleasanter:${PLEASANTER_VERSION}
        restart: unless-stopped
        depends_on:
          db:
            condition: service_healthy
          param-init:
            condition: service_completed_successfully
        ports:
          - '50001:8080'
        environment:
          Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
        volumes:
          - pleasanter_params:/app/App_Data/Parameters
        networks:
          - backend
      codedefiner:
        container_name: codedefiner
        image: implem/pleasanter:codedefiner
        depends_on:
          db:
            condition: service_healthy
          param-init-codedefiner:
            condition: service_completed_successfully
        environment:
          Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
          Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
        volumes:
          - codedefiner_params:/app/Implem.Pleasanter/App_Data/Parameters
        networks:
          - backend
    networks:
      backend:
    volumes:
      pg_data:
        name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
      pleasanter_params:
        name: ${COMPOSE_PROJECT_NAME:-default}_pleasanter_params_volume
      codedefiner_params:
        name: ${COMPOSE_PROJECT_NAME:-default}_codedefiner_params_volume
    ```

### 2. プリザンター再起動

1.  プリザンターが起動中の場合は以下コマンドを実行し、プリザンターを停止します。

    ``` bash
    docker compose down
    ```

1.  以下コマンドを実行し、パラメータ用volumeをクリアします。{{プロジェクトディレクトリ名}}はご利用環境に応じて適宜修正してください。なお初めて本手順を実行するなどパラメータ用volumeが存在しない場合はボリュームが存在しない旨のエラーとなりますが、3.以降を続行してください。

    ``` bash
    docker volume rm {{プロジェクトディレクトリ名}}_pleasanter_params_volume
    ```

    例：プロジェクトディレクトリが「pleasanter」の場合、以下コマンドとなります。

    ``` bash
    docker volume rm pleasanter_pleasanter_params_volume
    ```

1.  以下コマンドを実行し、プリザンターを起動します。

    ``` bash
    docker compose up -d pleasanter
    ```

### 3. プリザンターログイン

1.  ブラウザでプリザンターにアクセスし、ログイン画面でご利用のログインID、パスワードを入力してログインします。

    ``` text
    http://localhost:50001
    ```

1.  設定したパラメータが適用されているか確認します。

### 4. パラメータ変更後にCodeDefinerを実行する場合

「システムログの拡張機能」の利用時などパラメータを設定後にCodeDefinerを実行する場合は以下手順で実行してください。

1.  操作手順1. を行い、app_data_parametersに変更したパラメータファイルを格納します。
1.  プリザンターが起動中の場合は以下コマンドを実行し、プリザンターを停止します。

    ``` bash
    docker compose down
    ```

1.  以下コマンドを実行し、パラメータ用volumeをクリアします。{{プロジェクトディレクトリ名}}はご利用環境に応じて適宜修正してください。

    ``` bash
    docker volume rm {{プロジェクトディレクトリ名}}_codedefiner_params_volume
    ```

    例：プロジェクトディレクトリが「pleasanter」の場合、以下コマンドとなります。

    ``` bash
    docker volume rm pleasanter_codedefiner_params_volume
    ```

1.  CodeDefinerを実行します。

    ``` bash
    docker compose run --rm codedefiner _rds
    ```

## 関連情報

-   [Dockerで起動する](getting-started-pleasanter-docker.md)
-   [Dockerイメージを使用しDBにMySQLを指定して起動する](setup-by-docker-image-and-mysql.md)
-   [Dockerイメージを使用しDBにSQL Serverを指定して起動する](setup-by-docker-image-and-sql-server.md)
-   [Dockerイメージのプリザンターをバージョンアップする](../../version-up-migration/version-up-manually/version-up-pleasanter-docker.md)
-   [パラメータ設定：Rds.json](../../../setup/parameters/rds-json.md)
