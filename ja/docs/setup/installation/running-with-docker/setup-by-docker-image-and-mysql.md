---
title: Dockerイメージを使用しDBにMySQLを指定して起動する
category: Dockerで起動する
order: '103'
status: ''
parts: ''
urlstring: setup-by-docker-image-and-mysql
translationKey: setup-by-docker-image-and-mysql
shortname: Dockerで起動する
created: 2024-11-05
updated: 2026-07-17
---

## 概要

データベースにMySQLを指定して、[公式Dockerイメージ](https://hub.docker.com/r/implem/pleasanter)からプリザンターを起動する手順です。

## 制限事項

1.  MySQLでDockerイメージを利用する際、プリザンターのバージョンは1.4.10.0以降としてください。プリザンターはバージョン1.4.9.0以降でMySQLに対応しましたが、本手順はバージョン1.4.10.0以降でなければ実施できません。
1.  バージョン1.4.17.1以前を使用する場合は[Dockerイメージを使用しDBにMySQLを指定して起動する（バージョン1.4.17.1以前）](setup-by-docker-image-and-mysql-before-1-4-17-1.md)を参照ください。
1.  ver1.4.5以前で実施する場合はCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
[ver1.4.6以降で初回インストール時のCodeDefinerの手順について](https://pleasanter.org/ja/manual/codedefiner-changed-steps)
1.  本ページの手順は、プリザンターをすぐに試したいユーザのために、MySQLコンテナをプリザンターと同一のDocker構成に含めた複数コンテナ構成を採用しています。この構成は**本番運用を想定したものではありません**。
1.  本番運用では、データベースコンテナが性能上のボトルネックになります。**別ホスト上のデータベース**とすることを強く推奨します。
1.  タイムゾーンを日本に、言語を日本語にしています。適宜変更してください。

## 前提条件

1.  他データベースを使用する手順は以下を参照してください。  

    -   「Dockerで起動する」（PostgreSQL）  
    -   「Dockerイメージを使用しパラメータを既定値から変更して起動する」（PostgreSQL）  
    -   「Dockerイメージを使用しDBにSQL Serverを指定して起動する」

## 操作手順

### 1. ファイル配置、フォルダ作成

プロジェクトディレクトリ（以下例ではpleasanter）にフォルダを以下のように構成し、ファイルを配置します。

```text
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

| フォルダ<br>またはファイル | 説明 |
| -------------------------- | ----------|
| app_data_parameters        | ご利用環境に合わせて設定したパラメータファイルを格納するためのフォルダ。拡張SQLや拡張スクリプトなどの拡張機能用フォルダおよび拡張機能用ファイルも必要に応じて本フォルダに格納する。 |
| .env                       | データベース接続情報などの設定情報や環境変数を記述したファイル                                                                                                                      |
| compose.yaml               | Docker Composeの設定ファイル                                                                                                                                                        |

### 1-1. app_data_parametersフォルダ

1.  プロジェクトディレクトリで以下コマンドを実行し、app_data_parametersフォルダを作成します。<br>&nbsp;

    ```bash
    mkdir ./app_data_parameters
    ```

### 1-2. パラメータファイルの準備

1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンターをダウンロードします。特段理由がない場合は最新バージョンをダウンロードしてください。過去にリリースした特定のバージョンが必要な場合は、該当のバージョンのプリザンターをダウンロードしてください。
1.  zipファイルを解凍します。
1.  解凍したフォルダ配下にある「\pleasanter\Implem.Pleasanter\App_Data\Parameters\Rds.json」をapp_data_parametersフォルダ配下にコピーします。
1.  コピーした[Rds.json](../../parameters/rds-json.md)を以下のように編集して保存します。

    ```json title="Rds.json" linenums="1"
    {
        "Dbms": "MySQL",
        "Provider": "Local",
        "SaConnectionString": null,
        "OwnerConnectionString": null,
        "UserConnectionString": null,
        "SqlCommandTimeOut": 0,
        "MinimumTime": 3,
        "DeadlockRetryCount": 4,
        "DeadlockRetryInterval": 1000,
        "DisableIndexChangeDetection": true,
        "SysLogsSchemaVersion": 2,
        "MySqlConnectingHost": "%"
    }
    ```

5.  拡張SQL（ExtendedSqls）や拡張スクリプト（ExtendedScripts）などの拡張機能を設定する場合は拡張機能用のフォルダをapp_data_parametersにコピーし、コピーした各フォルダ内に拡張機能用ファイルを作成します。

### 1-3 .envファイル

1.  以下コマンドを実行し、.envファイルを作成します。

=== "Windows（コマンドプロンプト）"

    ``` bat
    type nul > .env
    ```

=== "Windows（PowerShell）"

    ``` ps1
    New-Item .env -ItemType File -Force
    ```

=== "Linux、macOS"

    ``` bash
    touch .env
    ```

2.  テキストエディタで.envを開き、以下の内容を張り付け保存します。{{ ... }} はご利用環境に合わせて適宜修正してください。各設定内容については「 [Dockerで起動する](getting-started-pleasanter-docker.md) 」の.envファイルに関する説明を参照してください。

    ```bash title=".env" linenums="1"
    MYSQL_VERSION={{MySQL Version}}
    MYSQL_ROOT_PASSWORD={{Sa Password}}
    PLEASANTER_VERSION={{Pleasanter Version}}
    Implem_Pleasanter_Rds_MySQL_SaConnectionString="Server=db;Database=mysql;UID=root;PWD={{Sa password}}"
    Implem_Pleasanter_Rds_MySQL_OwnerConnectionString="Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}}"
    Implem_Pleasanter_Rds_MySQL_UserConnectionString="Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}}"
    ```

### 1-4 compose.yaml ファイル

1.  以下コマンドを実行し、.envファイルを作成します。  

=== "Windows（コマンドプロンプト）"

    ``` bat
    type nul > compose.yaml
    ```

=== "Windows（PowerShell）"

    ``` ps1
    New-Item compose.yaml -ItemType File -Force
    ```

=== "Linux、macOS"

   ``` bash
   touch compose.yaml
   ```

1.  テキストエディタでcompose.yamlを開き、以下の内容を張り付け保存します。

  ```yaml
  services:
    db:
      container_name: mysql
      image: mysql:${MYSQL_VERSION}
      environment:
        - MYSQL_ROOT_PASSWORD
      volumes:
        - type: volume
          source: my_data
          target: /var/lib/mysql
      healthcheck:
        test: mysqladmin ping -h 127.0.0.1 -u root -p${MYSQL_ROOT_PASSWORD}
        interval: 10s
        timeout: 10s
        retries: 6
      networks:
        - backend
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
        Implem.Pleasanter_Rds_MySQL_SaConnectionString: ${Implem_Pleasanter_Rds_MySQL_SaConnectionString}
        Implem.Pleasanter_Rds_MySQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_MySQL_OwnerConnectionString}
        Implem.Pleasanter_Rds_MySQL_UserConnectionString: ${Implem_Pleasanter_Rds_MySQL_UserConnectionString}
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
        Implem.Pleasanter_Rds_MySQL_SaConnectionString: ${Implem_Pleasanter_Rds_MySQL_SaConnectionString}
        Implem.Pleasanter_Rds_MySQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_MySQL_OwnerConnectionString}
        Implem.Pleasanter_Rds_MySQL_UserConnectionString: ${Implem_Pleasanter_Rds_MySQL_UserConnectionString}
      volumes:
        - codedefiner_params:/app/Implem.Pleasanter/App_Data/Parameters
      networks:
        - backend
  networks:
    backend:
  volumes:
    my_data:
      name: ${COMPOSE_PROJECT_NAME:-default}_my_data_volume
    pleasanter_params:
      name: ${COMPOSE_PROJECT_NAME:-default}_pleasanter_params_volume
    codedefiner_params:
      name: ${COMPOSE_PROJECT_NAME:-default}_codedefiner_params_volume
  ```

### 2. プリザンター再起動

1.  プリザンターが起動中の場合は以下コマンドを実行し、プリザンターを停止します。

   ```bash
   docker compose down
   ```

1.  以下コマンドを実行し、パラメータ用volumeをクリアします。{{プロジェクトディレクトリ名}}はご利用環境に応じて適宜修正してください。なお初めて本手順を実行するなどパラメータ用volumeが存在しない場合はボリュームが存在しない旨のエラーとなりますが、3.以降を続行してください。

   ```bash
   docker volume rm {{プロジェクトディレクトリ名}}_pleasanter_params_volume
   ```

   例：プロジェクトディレクトリが「pleasanter」の場合、以下コマンドとなります。

   ```bash
   docker volume rm pleasanter_pleasanter_params_volume
   ```

1.  以下コマンドを実行し、プリザンターを起動します。

   ```bash
   docker compose up -d pleasanter
   ```

### 3. プリザンターログイン

1.  ブラウザでプリザンターにアクセスし、ログイン画面でご利用のログインID、パスワードを入力してログインします。  

   <http://localhost:50001>

1.  設定したパラメータが適用されているか確認します。

## パラメータ変更後にCodeDefinerを実行する場合

「システムログの拡張機能」の利用時などパラメータを設定後にCodeDefinerを実行する場合は以下手順で実行してください。

1.  操作手順 1. を行い、app_data_parametersに変更したパラメータファイルを格納します。
1.  プリザンターが起動中の場合は以下コマンドを実行し、プリザンターを停止します。

   ```bash
   docker compose down
   ```

1.  以下コマンドを実行し、パラメータ用volumeをクリアします。{{プロジェクトディレクトリ名}}はご利用環境に応じて適宜修正してください。

   ```bash
   docker volume rm {{プロジェクトディレクトリ名}}_codedefiner_params_volume
   ```

   例：プロジェクトディレクトリが「pleasanter」の場合、以下コマンドとなります。

   ```bash
   docker volume rm pleasanter_codedefiner_params_volume
   ```

1.  CodeDefinerを実行します。

   ```bash
   docker compose run --rm codedefiner _rds
   ```

## 対応バージョン

| 対応バージョン | 内容                                                                                                                                                                                                             |
| :------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題の解消に伴いマニュアルを公開<br>* プリザンターはVer1.4.9.0以降でMySQLに対応しましたが、本手順はVer1.4.10.0以降でなければ実施できません。 |
| 1.4.18.0 以降  | MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能の追加に伴いマニュアルを修正                                                                                                           |

## 関連情報

[Dockerで起動する](getting-started-pleasanter-docker.md)  
[Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)  
[Dockerイメージのプリザンターをバージョンアップする](../../version-up-migration/version-up-manually/version-up-pleasanter-docker.md)  
