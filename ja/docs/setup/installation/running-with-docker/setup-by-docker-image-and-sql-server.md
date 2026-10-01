---
title: Dockerイメージを使用しDBにSQL Serverを指定して起動する
category: Dockerで起動する
order: '103'
status: ''
parts: ''
urlstring: setup-by-docker-image-and-sql-server
translationKey: setup-by-docker-image-and-sql-server
shortname: ''
created: 2025-07-18
updated: 2026-07-17
---

## 概要

データベースにSQL Serverを指定して、[公式Dockerイメージ](https://hub.docker.com/r/implem/pleasanter)からプリザンターを起動する手順です。

## 注意事項

1.  本ページの手順は、プリザンターをすぐに試したいユーザのために、SQL Serverコンテナをプリザンターと同一のDocker構成に含めた複数コンテナ構成を採用しています。この構成は本番運用を想定したものではありません。
1.  本番運用では、データベースコンテナが性能上のボトルネックになります。 別ホスト上のデータベース とすることを強く推奨します。
1.  タイムゾーンを日本に、言語を日本語にしています。適宜変更してください。
1.  SQL Serverの公式Dockerイメージ（mcr.microsoft.com/mssql/server:2025-latest）のエディションは既定でEnterprise Developer Editionですが、本手順ではExpression Editionを利用します。エディションを変更する必要がある場合は、.envのMSSQL_PIDの値を[マイクロソフト社のドキュメント](https://learn.microsoft.com/ja-jp/sql/linux/configure/environment-variables?view=sql-server-ver17#sql-server-editions)を参考に書き替えてください。  

    ``` ini title=".env" linenums="1"
    MSSQL_PID=Express
    ```

1.  SQL Serverへの接続には信頼された証明書によるTLS暗号化が必要です。本手順では証明書の検証を省略していますので注意してください。本番環境では適切な証明書を設定してください。詳細は「[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../prerequisites/sqlserver-connection-string-v15.md)」を参照してください。

## 前提条件

1.  本手順ではデータベースとしてSQL Serverを使用します。他データベースを使用する手順は以下を参照してください。

    -   [Dockerで起動する](getting-started-pleasanter-docker.md)（PostgreSQL）
    -   [Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)（PostgreSQL）
    -   [Dockerイメージを使用しDBにMySQLを指定して起動する](setup-by-docker-image-and-mysql.md)（MySQL）

1.  本手順は、以下2件のマニュアルの手順通りプリザンターの公式Dockerイメージを使用の上、パラメータファイルを変更して起動できることを前提としています。データベースの作成は不要です。

    1.  [Dockerで起動する](getting-started-pleasanter-docker.md)
    1.  [Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)

    未読の場合は上記マニュアルを参照して、プリザンターの公式Dockerイメージを使用の上、パラメータファイルを変更して起動できることを確認してください。

## 操作手順

### 1. フォルダ、ファイルを配置する

プロジェクトディレクトリ（以下例ではpleasanter）にフォルダを以下のように構成し、ファイルを配置します。

```text
📁 pleasanter
    +--📁 app_data_parameters
    |   +--📄 Rds.json
    |   +--📄 Service.json
    |
    +--📁 CodeDefiner
    |   +--📄 Dockerfile
    |
    +--📁 Pleasanter
    |   +--📄 Dockerfile
    |
    +--📁 SQLServer
    |   +--📄 Dockerfile
    |
    |--📄 .env
    +--📄 compose.yml
```

#### 1-1 パラメータファイル

1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンターをダウンロードします。特段理由がない場合は最新バージョンをダウンロードしてください。過去にリリースした特定のバージョンが必要な場合は、該当のバージョンのプリザンターをダウンロードしてください。
1.  zipファイルを解凍してください。
1.  解凍したフォルダ配下にある「\pleasanter\Implem.Pleasanter\App_Data\Parameters」内の[Rds.json](../../parameters/rds-json.md)と[Service.json](../../parameters/service-json.md)をapp_data_parametersフォルダ配下にコピーしてください。
1.  「Rds.json」と「Service.json」を以下のように編集してください。

##### 1-1-1 `app_data_parameters/Rds.json`

1.  "Dbms"の値を"SQLServer"に設定してください。
1.  "SaConnectionString"、"OwnerConnectionString"、"UserConnectionString"の値をnullに設定してください。

    ``` json title="app_data_parameters/Rds.json" linenums="1"
    {
        "Dbms": "SQLServer",
        "Provider": "Local",
        "SaConnectionString": null,
        "OwnerConnectionString": null,
        "UserConnectionString": null,
        "SqlCommandTimeOut": 0,
            : 中略
    }
    ```

##### 1-1-2 `app_data_parameters/Service.json`

1.  "TimeZoneDefault"の値を"Asia/Tokyo"に設定してください。SQL ServerのベースイメージはLinuxであり、Linuxのタイムゾーンを設定する必要があるためです。
1.  "DefaultLanguage"の値を"ja"（日本語）に設定してください。

    ``` json title="app_data_parameters/Service.json" linenums="1"
    {
        "Name": "Implem.Pleasanter",
        "EnvironmentName": null,
        "TimeZoneDefault": "Asia/Tokyo",
        "DefaultPassword": "pleasanter",
        "DeploymentEnvironment": null,
        "WithoutChangeDefaultPassword": false,
        "DefaultLanguage": "ja",
        "AbsoluteUri": null,
            : 中略
    }
    ```

#### 1-2 CodeDefiner/Dockerfile

CodeDefiner/Dockerfileを以下の内容で作成します。

```Dockerfile title="CodeDefiner/Dockerfile" linenums="1"
FROM implem/pleasanter:codedefiner

COPY app_data_parameters/ /app/Implem.Pleasanter/App_Data/Parameters/
ENTRYPOINT [ "dotnet", "Implem.CodeDefiner.dll" ]
```

#### 1-3 Pleasanter/Dockerfile

Pleasanter/Dockerfileを以下の内容で作成します。

```Dockerfile title="Pleasanter/Dockerfile" linenums="1"
ARG VERSION=latest
FROM implem/pleasanter:${VERSION}

COPY app_data_parameters/ App_Data/Parameters/
ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
```

#### 1-4 SQLServer/Dockerfile

フルテキスト検索を有効にするため、SQL Serverのイメージをベースにして、フルテキスト検索をインストールします。

```Dockerfile title="SQLServer/Dockerfile" linenums="1"
FROM mcr.microsoft.com/mssql/server:2025-latest

USER root

RUN apt-get update && apt-get install -y curl apt-transport-https gnupg2 && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/24.04/mssql-server-2025.list -o /etc/apt/sources.list.d/mssql-server-2025.list && \
    apt-get update && \
    apt-get install -y mssql-server-fts && \
    apt-get clean && rm -rf /var/lib/apt/lists

EXPOSE 1433
USER mssql
ENTRYPOINT [ "/opt/mssql/bin/sqlservr" ]
```

#### 1-5 .env

{{ ... }}はご利用環境に合わせて適宜修正してください。接続文字列中のTrustServerCertificate=true;については。[こちら](../prerequisites/sqlserver-connection-string-v15.md)を確認してください。

``` ini title=".env" linenums="1"
PLEASANTER_VER=latest
SA_PASSWORD={{Sa Password}}
MSSQL_PID=Express

Implem_Pleasanter_Rds_SQLServer_SaConnectionString=Server=db;Database=master;UID=sa;PWD={{Sa Password}};TrustServerCertificate=true
Implem_Pleasanter_Rds_SQLServer_OwnerConnectionString=Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}};TrustServerCertificate=true
Implem_Pleasanter_Rds_SQLServer_UserConnectionString=Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}};TrustServerCertificate=true
TZ=Asia/Tokyo
```

#### 1-6 compose.yaml

compose.yamlを以下の内容で作成します。

``` yaml title="compose.yaml" linenums="1"
services:
  pleasanter:
    build:
      context: .
      dockerfile: ./Pleasanter/Dockerfile
      args:
        - VERSION=${PLEASANTER_VER}
    container_name: pleasanter_${PLEASANTER_VER}
    restart: unless-stopped
    depends_on:
      db:
        condition: service_healthy
    environment:
      Implem.Pleasanter_Rds_SaConnectionString: ${Implem_Pleasanter_Rds_SQLServer_SaConnectionString}
      Implem.Pleasanter_Rds_OwnerConnectionString: ${Implem_Pleasanter_Rds_SQLServer_OwnerConnectionString}
      Implem.Pleasanter_Rds_UserConnectionString: ${Implem_Pleasanter_Rds_SQLServer_UserConnectionString}
      TZ: ${TZ}
    ports:
      - '8881:8080'
    networks:
      - default
  codedefiner:
    build:
      context: .
      dockerfile: ./CodeDefiner/Dockerfile
    container_name: codedefiner
    depends_on:
      db:
        condition: service_healthy
    environment:
      Implem.Pleasanter_Rds_SaConnectionString: ${Implem_Pleasanter_Rds_SQLServer_SaConnectionString}
      Implem.Pleasanter_Rds_OwnerConnectionString: ${Implem_Pleasanter_Rds_SQLServer_OwnerConnectionString}
      Implem.Pleasanter_Rds_UserConnectionString: ${Implem_Pleasanter_Rds_SQLServer_UserConnectionString}
      TZ: ${TZ}
    networks:
      - default
    stdin_open: true
  db:
    build:
      context: .
      dockerfile: ./SQLServer/Dockerfile
    container_name: sqldb
    restart: unless-stopped
    environment:
      ACCEPT_EULA: 'Y'
      MSSQL_SA_PASSWORD: ${SA_PASSWORD}
      MSSQL_PID: ${MSSQL_PID}
      TZ: ${TZ}
    ports:
      - '11433:1433'
    networks:
      - default
    volumes:
      - sqlvolume:/var/opt/mssql
    healthcheck:
      test: /opt/mssql-tools18/bin/sqlcmd -S localhost -U sa -P $$MSSQL_SA_PASSWORD -Q "SELECT 1" -No || exit 1
      interval: 10s
      timeout: 5s
      retries: 10
      start_period: 30s

volumes:
  sqlvolume:

networks:
  default:
    name: pleasanter_prod_network
```

### 2. コンテナイメージをビルドする

以下のコマンドを実行してください。各サービス（pleasanter、codedefiner、db）をビルドします。オプション--pullを指定することで、イメージの更新を確認し、最新のイメージを取得します。

``` bash
docker compose build --pull pleasanter codedefiner db
```

### 3. コンテナを起動する

以下のコマンドを実行してください。dbコンテナ（SQL Server）を起動します。

``` bash
docker compose up -d db
```

以下のコマンドを実行してください。codedefinerコンテナが起動し、データベースを初期化します。本手順ではあらかじめService.jsonでタイムゾーンと言語を設定しているため、/l、/zオプションの指定は不要です。初期化前の確認手順を省きたい場合は/yオプションを付与してください。

``` bash
docker compose run --rm codedefiner _rds
```

### 4. プリザンターを起動する

#### 4-1 プリザンターのコンテナを起動する

以下のコマンドを実行してください。プリザンターのコンテナが起動します。

``` bash
docker compose up -d pleasanter
```

#### 4-2 動作確認

1.  ブラウザで以下のURLにアクセスしてください。

    ``` text
    http://localhost:8881
    ```

1.  ログイン画面にて以下のように入力します。

    |  ログインID   | パスワード |
    | :-----------: | :--------: |
    | Administrator | pleasanter |

1.  ログイン後、パスワードの変更を求められますので、適宜パスワードを設定してください。

#### 4-3 SQL Serverコンテナに接続する

SSMSや各種対応ツールから、ホストの11433番ポート経由で接続できます。compose.ymlにより、コンテナ内のSQL Server（1433番ポート）にマッピングされています。

### 5. コンテナの停止と削除

#### 5-1 コンテナを停止する

コンテナの停止は、以下のコマンドを実行します。

```bash
docker compose stop
```

コンテナを停止してもDBデータ（ボリューム）は削除されません。

#### 5-2 停止したコンテナを再開する

停止したコンテナを再開する場合は、以下のコマンドを実行します。

```bash
docker compose start
```

コンテナを停止してもDBデータ（ボリューム）は削除されません。再開する際にはデータがそのまま利用できます。

#### 5-3 コンテナを削除する

コンテナの削除は、以下のコマンドを実行します。コンテナを削除してもDBデータ（ボリューム）は削除されません。

```bash
docker compose down
```

なお、コンテナを削除した場合、docker compose startでの再開はできません。

#### 5-4 コンテナを再作成する

コンテナを作成して、起動したい場合は、以下のコマンドを実行します。DBのコンテナが作成され、DBデータ（ボリューム）を利用できます。

```bash
docker compose up -d pleasanter
```

#### 5-5 コンテナ削除と同時にDBデータを削除する

コンテナを削除する時に同時にDBデータ（ボリューム）を削除する場合は、ボリュームを削除するオプション（-v）を付けて実行します。

```bash
docker compose down -v
```

### 6. パラメータ変更後にCodeDefinerを実行する場合

「システムログの拡張機能」の利用時などパラメータを設定後にCodeDefinerを実行する場合は以下手順で実行してください。

1.  操作手順1. を行い、app_data_parametersに変更したパラメータファイルを格納し、.env、compose.yamlを作成します。
1.  プリザンターが起動中の場合は以下コマンドを実行し、コンテナを停止して削除します。

       ```bash
       docker compose down
       ```

1.  以下コマンドを実行し、pleasanterコンテナとcodedefinerコンテナをビルドします。

       ```bash
       docker compose build pleasanter codedefiner
       ```

1.  CodeDefinerを実行します。

       ```bash
       docker compose run --rm codedefiner _rds
       ```

1.  pleasanterコンテナを起動します。

       ```bash
       docker compose up -d pleasanter
       ```

## 関連情報

[Dockerで起動する](getting-started-pleasanter-docker.md)  
[Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)  
[Dockerイメージのプリザンターをバージョンアップする](../../version-up-migration/version-up-manually/version-up-pleasanter-docker.md)  
