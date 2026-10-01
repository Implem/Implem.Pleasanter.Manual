---
title: Dockerで起動する
category: Dockerで起動する
order: '101'
status: ''
parts: ''
urlstring: getting-started-pleasanter-docker
translationKey: getting-started-pleasanter-docker
shortname: Dockerで起動する
created: 2023-10-12
updated: 2026-07-17
---

## 概要

データベースにPostgreSQLを指定して、[公式Dockerイメージ](https://hub.docker.com/r/implem/pleasanter)からプリザンターを起動する手順です。

以下2つのパターンの手順を説明します

1.  [既定の環境設定でプリザンターを起動する](#fast)
2.  [環境設定を行いプリザンターを起動する](#normal)

## 注意事項

1.  ver1.4.5以前で実施する場合はCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
    [ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../../installation/prerequisites/codedefiner-changed-steps.md)
1.  本ページの手順は、プリザンターをすぐに試したいユーザのために、PostgreSQLコンテナをプリザンターと同一のDocker構成に含めた複数コンテナ構成を採用しています。この構成は**本番運用を想定したものではありません**。
1.  本番運用では、データベースコンテナが性能上のボトルネックになります。**別ホスト上のデータベース**とすることを強く推奨します。

## 前提条件

1.  プリザンターのパラメータ値を変更してDockerで起動する手順は「[Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)」を参照してください。
1.  本手順ではデータベースとしてPostgreSQLを使用します。他データベースを使用する手順は以下を参照してください。
    1.  [Dockerイメージを使用しDBにMySQLを指定して起動する](setup-by-docker-image-and-mysql.md)
    1.  [Dockerイメージを使用しDBにSQL Serverを指定して起動する](setup-by-docker-image-and-sql-server.md)
1.  データベースにPostgreSQLを使用する場合[Rds.json](../../parameters/rds-json.md)の配置・編集は不要です。

<a id="fast"></a>

## 1. 既定の環境設定でプリザンターを起動する

すぐにプリザンターを試してみたい、まずは使ってみたい方はこちらの手順でプリザンターを起動してください。

!!! danger 本番運用における注意事項
    本番運用に移行する際は管理用ユーザのパスワード、各接続文字列のパスワードは必ず見直してください。

## 概要

下記既定値での環境設定ですぐにDocker版プリザンターを利用する手順について説明します。

| No  | 設定内容                             | パラメータ                                                        | 設定値       | 備考                   |
| --: | :----------------------------------- | :---------------------------------------------------------------- | :----------- | :--------------------- |
| 1   | PostgreSQLのバージョン               | POSTGRES_VERSION                                                  | 17           |                        |
| 2   | PostgreSQLの管理用ユーザのパスワード | POSTGRES_PASSWORD                                                 | SetSaPWD     |                        |
| 3   | Sa接続文字列のパスワード             | Implem_Pleasanter_Rds_PostgreSQL<br>_SaConnectionString内のPWD    | SetSaPWD     | 2と同じ値を設定        |
| 4   | Owner接続文字列のパスワード          | Implem_Pleasanter_Rds_PostgreSQL<br>_OwnerConnectionString内のPWD | SetAdminsPWD |                        |
| 5   | User接続文字列のパスワード           | Implem_Pleasanter_Rds_PostgreSQL<br>_UserConnectionString内のPWD  | SetUsersPWD  |                        |
| 6   | プリザンターのバージョン             | PLEASANTER_VERSION                                                | latest       | 利用時点の最新版を取得 |
| 7   | プリザンターの言語                   | CodeDefinerの/lオプション                                         | "ja"         |                        |
| 8   | プリザンターのタイムゾーン           | CodeDefinerの/zオプション                                         | "Asia/Tokyo" |                        |

## 手順

手順の流れは以下の通りです。

1.  [Docker実行環境の準備](#preq)
1.  [プロジェクトディレクトリの作成と移動](#projdir)
1.  [ファイルの作成](#makefiles)
1.  [CodeDefinerの実行](#runcodedefiner)
1.  [プリザンターの起動・終了](#runpleasanter)

<a id="preq"></a>

### 1. Docker実行環境の準備

ご利用のOSに応じたDocker実行環境（Docker EngineやDocker Desktop等）を準備します。詳細は以下の[Docker公式マニュアル](https://docs.docker.com/)をご参照ください。

-   [Docker Engine \| Docker Docs](https://docs.docker.com/engine/)
-   [Docker Desktop \| Docker Docs](https://docs.docker.com/desktop/)

<a id="projdir"></a>

### 2. プロジェクトディレクトリの作成と移動

以下のコマンドを実行し任意の場所にプロジェクトディレクトリを作成します。以下コマンドではプロジェクトディレクトリ名を「pleasanter」としましたが他の名称に変更しても問題ありません。

``` cmd
mkdir ./pleasanter
cd ./pleasanter
```

<a id="makefiles"></a>

### 3. ファイルの作成

プロジェクトディレクトリ内に「.env」、「compose.yaml」という2つのファイルを作成します。

=== "Windows（CMD）の場合"

    ``` cmd
    type nul > .env
    type nul > compose.yaml
    ```

=== "Windows（PowerShell）の場合"

    ``` ps1
    New-Item .env -ItemType File -Force
    New-Item compose.yaml -ItemType File -Force
    ```

=== "macOS、Linuxの場合"

    ``` bash
    touch .env
    touch compose.yaml
    ```

#### .env

テキストエディタで.envを開き、以下の内容を貼り付け保存します。

``` ini title=".env" linenums="1"
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

テキストエディタでcompose.yamlを開き、以下の内容を貼り付けて保存します。

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
  pleasanter:
    container_name: pleasanter
    image: implem/pleasanter:${PLEASANTER_VERSION}
    restart: unless-stopped
    depends_on:
      db:
        condition: service_healthy
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
      db:
        condition: service_healthy
    environment:
      Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
      Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
volumes:
  pg_data:
    name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
```

<a id="runcodedefiner"></a>

### 4. CodeDefinerの実行

プロジェクトディレクトリで、以下のコマンドでCodeDefinerを実行します。

``` bash
docker compose run --rm codedefiner _rds /y /l "ja" /z "Asia/Tokyo"
```

<a id="runpleasanter"></a>

### 5. プリザンターの起動・終了

#### プリザンターを起動する

1.  プロジェクトディレクトリで、以下のコマンドを実行しプリザンターを起動します。

    ```shell
    docker compose up -d pleasanter
    ```

1.  Webブラウザで[http://localhost:50001](http://localhost:50001)を開いてください。
1.  ログイン画面が表示されたら、次の各情報を入力してください。

    |  ログインID   | 初期パスワード |
    | :-----------: | :------------: |
    | Administrator |   pleasanter   |

    ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/running-with-docker/assets/a82685936a6c4b2aa5959830a9911daa.png)

1.  安全なパスワードに変更してください。

    ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/running-with-docker/assets/03ebe82fc4ed49b7a8325414557d9a6a.png)

#### プリザンターを終了する

1.  Webブラウザを終了してください。
1.  プロジェクトディレクトリで、コンテナを停止してください。

    ``` bash
    docker compose stop
    ```

#### プリザンターをもう一度起動する

1.  プロジェクトディレクトリで、コンテナを起動してください。

    ```shell
    docker compose start
    ```

1.  Webブラウザで[http://localhost:50001](http://localhost:50001)を開いてください。

---

<a id="normal"></a>

## 2. 環境設定を行いプリザンターを起動する

プリザンターやPostgreSQLのバージョン、PostgreSQLの設定やプリザンターの接続文字列などを設定してプリザンターをご利用したい場合はこちらの手順を参照してください。

??? note 詳しい説明を読む

    ## 1. プロジェクトディレクトリの作成

    次項で説明する「.env」、「compose.yaml」という2つのファイルを格納するプロジェクトディレクトリを任意の場所に作成します。ディレクトリ名は任意です。

    ## 2. .envの作成

    PostgreSQLを初期化するinitdbに使われるユーザやパスワードなどの環境変数とプリザンターのデータベース接続文字列の設定を記載した「.env」ファイルを作成します。設定する内容は以下の通りです。

    | No  | 設定内容                             | パラメータ                                                        | 設定例                   | 備考                                                      |
    | --: | :----------------------------------- | :---------------------------------------------------------------- | :----------------------- | :-------------------------------------------------------- |
    | 1   | PostgreSQLのバージョン               | POSTGRES_VERSION                                                  | 17                       |                                                           |
    | 2   | PostgreSQLのボリュームパス           | POSTGRES_VOLUMES_TARGET                                           | /var/lib/postgresql/data | バージョン18以降の場合は/var/lib/postgresqlと指定すること |
    | 3   | PostgreSQLの管理用ユーザのパスワード | POSTGRES_PASSWORD                                                 | SetSaPWD                 |                                                           |
    | 4   | Sa接続文字列のパスワード             | Implem_Pleasanter_Rds_PostgreSQL<br>_SaConnectionString内のPWD    | SetSaPWD                 | 3と同じ値を設定                                           |
    | 5   | Owner接続文字列のパスワード          | Implem_Pleasanter_Rds_PostgreSQL<br>_OwnerConnectionString内のPWD | SetAdminsPWD             |                                                           |
    | 6   | User接続文字列のパスワード           | Implem_Pleasanter_Rds_PostgreSQL<br>_UserConnectionString内のPWD  | SetUsersPWD              |                                                           |
    | 7   | プリザンターのバージョン             | PLEASANTER_VERSION                                                | 1.5.0.0                  | 利用時点の最新版を取得する場合はlatestと指定              |

    POSTGRESではじまる環境変数はPostgreSQLのDocker公式イメージが使用します。コンテナの初期化時にinitdbが実行され、環境変数の値を使ってPostgreSQLの初期設定が行われます。

    - [postgres - Official Image | Docker Hub](https://hub.docker.com/_/postgres)
    - [docker-library/postgres: Docker Official Image packaging for Postgres](https://github.com/docker-library/postgres)

    接続文字列の詳細については以下マニュアルを参照ください。

    - [Rds.json](../../../setup/parameters/rds-json.md)

    実際のファイルの例です。`{{ ... }}`は適宜修正し、**.env**としてプロジェクトディレクトリに保存します。

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

    ## 3. Docker Compose ファイル

    以下内容でcompose.yamlファイルを作成します。

    ``` yaml title="compose.yamml" linenums="1"
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
    pleasanter:
        container_name: pleasanter
        image: implem/pleasanter:${PLEASANTER_VERSION}
        restart: unless-stopped
        depends_on:
        db:
            condition: service_healthy
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
        db:
            condition: service_healthy
        environment:
        Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
        Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
        Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
    volumes:
    pg_data:
        name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
    ```

    ファイル配置は以下のようになります。

    ``` text
    ./projectDirectory
    |-- .env
    |-- compose.yaml
    ```

    ## 2. CodeDefinerの実行

    プロジェクトディレクトリで以下コマンドにてCodeDefinerを実行します。

    ```bash
    docker compose run --rm codedefiner _rds /l "<言語>" /z "<タイムゾーン>"
    ```

    | 引数 | 設定例     | 説明                                                |
    | :--- | :--------- | :-------------------------------------------------- |
    | /l   | ja         | Service.jsonのDefaultLanguageの値を書き換えます[^1] |
    | /z   | Asia/Tokyo | Service.jsonのTimeZoneDefaultの値を書き換えます[^1] |

    [^1]: 言語、タイムゾーンは以下マニュアルページを参照ください。  
    [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

    日本語環境でご利用する場合は以下コマンドとなります。

    ``` bash
    docker compose run --rm codedefiner _rds /l "ja" /z "Asia/Tokyo"
    ```

    途中で「Type "y" (yes) if the license is correct, otherwise type "n" (no).」と表示されたら ++y++ を入力してください。

    !!! note
        コンソールログに以下のようにバージョンが出力されます。ここで表示されるバージョンは常に「DockerHubで公開されている最新のプリザンターのバージョン」となります。このコンソールログ表示の仕様は、compose.yamlの{{Version}}に最新よりも前のバージョンを指定した場合も同様ですが、データベースは{{Version}}に準拠した内容で作成されますので、プリザンターの動作上の問題はありません。

        ``` bash
        <INFO> Starter.Main: Implem.CodeDefiner 1.5.0.0
        ```

    ## 3. プリザンター起動

    プロジェクトディレクトリで以下コマンドを実行し、コンテナを作成しプリザンターを起動します。

    ``` bash
    docker compose up -d pleasanter
    ```

    以下URLにブラウザでアクセスします。

    ``` text
    http://localhost:50001
    ```

    ログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力します。ログイン後、パスワードの変更を求められますので適宜パスワードを設定してください。

    ## 4. コンテナの停止と削除

    コンテナの停止はプロジェクトディレクトリで以下のコマンドを実行します。

    ``` bash
    docker compose stop
    ```

    停止したコンテナを再開する場合はプロジェクトディレクトリで以下のコマンドを実行します。

    ``` bash
    docker compose start
    ```

    コンテナを停止してもDBデータは削除されません。再開する際にはデータがそのまま利用できます。

---

コンテナの削除はプロジェクトディレクトリで以下のコマンドを実行します。コンテナを削除してもDBデータ（ボリューム）は削除されません。なおコンテナを削除した場合は再開はできません。

``` bash
docker compose down
```

コンテナ削除後に再度起動したい場合はプロジェクトディレクトリで以下コマンドを実行しコンテナを作成してください。これによりDBのコンテナも一緒に作成され残っているDBデータもそのまま利用できます。

``` bash
docker compose up -d pleasanter
```

コンテナを削除する時に同時にデータ（ボリューム）を削除する場合はボリュームを削除するオプションを付けて実行します。

``` bash
docker compose down -v
```

</details>

## 関連情報

-   [Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)
-   [Dockerイメージを使用しDBにMySQLを指定して起動する](setup-by-docker-image-and-mysql.md)
-   [Dockerイメージのプリザンターをバージョンアップする](../../version-up-migration/version-up-manually/version-up-pleasanter-docker.md)

