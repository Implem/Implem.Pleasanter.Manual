---
title: Dockerイメージを使用しDBにMySQLを指定して起動する（バージョン1.4.17.1以前）
category: Dockerで起動する
order: '103'
status: ''
parts: ''
urlstring: setup-by-docker-image-and-mysql-before-1-4-17-1
translationKey: setup-by-docker-image-and-mysql-before-1-4-17-1
shortname: Dockerイメージを使用しDBにMySQLを指定して起動する（バージョン1.4.17.1以前）
created: 2026-05-29
updated: 2026-07-17
---

## はじめに

本手順は、以下2件のマニュアルの手順通りプリザンターの公式Dockerイメージを使用の上、パラメータファイルを変更して起動できることを前提としています。

1.  [Dockerで起動する](getting-started-pleasanter-docker.md)
1.  [Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)

未読の場合は先に上記マニュアルを参照し、プリザンターの公式Dockerイメージを使用の上、パラメータファイルを変更して起動できることを確認してください。

## 制限事項

1.  MySQLでDockerイメージを利用する際、プリザンターのバージョンは1.4.10.0以降としてください。プリザンターはVer1.4.9.0以降でMySQLに対応しましたが、本手順はVer1.4.10.0以降でなければ実施できません。
1.  Dockerでプリザンターを運用する場合、パラメータファイルの設定変更時は、プリザンターの停止・再起動だけでなく、`docker compose build`コマンドによるビルドを再実施してください。ビルドを行っていない状態では、プリザンターを再起動してもパラメータファイルの変更が反映されません。
1.  バージョン1.4.18.0以降を使用する場合は[Dockerイメージを使用しDBにMySQLを指定して起動する](setup-by-docker-image-and-mysql.md)を参照ください。

## 前提条件

1.  本手順ではデータベースとしてMySQLを使用します。PostgreSQLを使用する手順は「[Dockerで起動する](getting-started-pleasanter-docker.md)」および「[Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)」を参照してください。

## MySQL使用時に必要となるDockerの追加設定

本手順では、以下設定によりプリザンターのDBにMySQLを指定してコンテナを起動します。

1.  [Rds.json](../../parameters/rds-json.md)の内容をMySQL用の記述に変更する。
1.  プリザンター（およびCodeDefiner）のコンテナの環境変数に、MySQL用の接続文字列を登録する。

また、MySQLの利用に付随して必要となる以下の設定を行います。

1.  MySQLのユーザアカウント作成用SQLを記述する。（SQLはMySQLのコンテナを起動する際に自動実行）
1.  プリザンター（およびCodeDefiner）の起動時のエラーを防ぐため、MySQLの起動が完了しているかチェックする設定を、compose.yamlファイルに記述する。

---

## 1. ファイル配置

フォルダを以下のように構成し、ファイルを配置します。

```text
.
|-- compose.yaml
|-- .env
|
+-- app_data_parameters
|   +-- 拡張機能用フォルダ
|   |   +-- 拡張機能用ファイル
|   |  
|   +-- パラメータファイル
|
+-- docker-entrypoint-initdb.d
|   +-- pleasanter.sql
|
+-- CodeDefiner
|   +-- Dockerfile
|
+---Pleasanter
    +-- Dockerfile
```

### 1-1. app_data_parametersフォルダ

以下手順で[Rds.json](../../parameters/rds-json.md)および既定値から変更したいパラメータファイルを配備します。

1.  ダウンロードセンターから、プリザンターをダウンロードします。特段理由がない場合は最新バージョンをダウンロードしてください。過去にリリースした特定のバージョンが必要な場合は、該当のバージョンのプリザンターをダウンロードしてください。
1.  zipファイルを解凍します。
1.  解凍したフォルダ配下にある「\pleasanter\Implem.Pleasanter\App_Data\Parameters\Rds.json」を`app_data_parameters`フォルダ配下にコピーします。
1.  コピーした[Rds.json](../../parameters/rds-json.md)を編集し、使用するデータベースサーバをMySQLに変更して保存します。
1.  その他にパラメータを既定値から変更したい場合は、変更済みのパラメータファイルを`app_data_prameters`フォルダに格納してください。

以下、[Rds.json](../../parameters/rds-json.md)の修正例です。

``` json title="Rds.json" linenums="1"
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

### 1-2. CodeDefinerフォルダ

`/CodeDefiner/Dockerfile`を以下の内容で作成します。

``` Dockerfile title="/CodeDefiner/Dockerfile" linenums="1"
FROM implem/pleasanter:codedefiner

COPY app_data_parameters/ /app/Implem.Pleasanter/App_Data/Parameters/
ENTRYPOINT [ "dotnet", "Implem.CodeDefiner.dll" ]
```

### 1-3. Pleasanterフォルダ

`/Pleasanter/Dockerfile`を以下の内容で作成します。

``` Dockerfile title="/Pleasanter/Dockerfile" linenums="1"
ARG VERSION=latest
FROM implem/pleasanter:${VERSION}

COPY app_data_parameters/ App_Data/Parameters/
ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
```

### 1-4 .envファイル

`.env`ファイルを作成します。

MySQLのDocker公式イメージで必須とされる環境変数のうち、本手順ではデフォルトのスーパーユーザアカウント（root）のパスワード設定先である`MySQL_ROOT_PASSWORD`を記述します。

MySQL - Official Image | Docker Hub
docker-library/MySQL: Docker Official Image packaging for MySQL Community Server

| 名称                | 内容                             |
| ------------------- | -------------------------------- |
| MySQL_ROOT_PASSWORD | 任意のパスワード文字列を指定する |

環境変数`PLEASANTER_VER`を用意し、プリザンターのバージョンを指定します。

| 名称           | 内容                                                                                                                                                                                                                                                           |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PLEASANTER_VER | {{Version}}は、DockerHubで公開されているプリザンターのバージョン（例：latest、1.4.10.1など）を指定してください。<br>バージョンの値は、前述の「1-1. app_data_parametersフォルダ」内に配備するパラメータファイルの取得元のバージョンと一致させる必要があります。 |

`SaConnectionString`は最初にMySQLにスーパーユーザで接続するための設定が一行で表現されています。MySQLの環境変数の内容と`SaConnectionString`に記述されている内容を合わせる必要があります。

| 名称     | 内容                                                         |
| -------- | ------------------------------------------------------------ |
| Server   | composeファイルのサービス名（db）を指定する                 |
| Database | MySQLのデフォルトのシステムデータベース名（MySQL）を指定する |
| UID      | MySQLのデフォルトのスーパーユーザ名（root）を指定する        |
| PWD      | 環境変数のMySQL_ROOT_PASSWORDと揃える                      |

OwnerConnectionStringとUserConnectionStringはそれぞれのユーザで接続するための設定が一行で表現されています。

| 名称 | 内容                                                            |
| ---- | --------------------------------------------------------------- |
| PWD  | 任意のパスワード文字列。OwnerとUserのパスワードは別々が望ましい |

実際のファイルの例です。`{{ ... }}`は適宜修正してください。

``` ini title=".env" linenums="1"
MYSQL_ROOT_PASSWORD={{Sa Password}}
PLEASANTER_VER={{Version}}
Implem_Pleasanter_Rds_MySQL_SaConnectionString='Server=db;Database=mysql;UID=root;PWD={{Sa password}}'
Implem_Pleasanter_Rds_MySQL_OwnerConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}}'
Implem_Pleasanter_Rds_MySQL_UserConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}}'
```

### 1-5. docker-entrypoint-initdb.dフォルダ

#### 説明

後述する`compose.yaml`ファイル内`db`サービス配下の`volumes`の設定により、MySQLのコンテナの`docker-entrypoint-initdb.d`ディレクトリに自動的にマウントされるフォルダです。

コンテナにマウントされた`docker-entrypoint-initdb.d`ディレクトリ内のファイルに記載されているSQLコマンドは、MySQLのコンテナの起動時に自動実行されます。

#### 記述するSQLの内容

以下、`docker-entrypoint-initdb.d`フォルダ内に配置する`pleasanter.sql`ファイルの例です。

``` sql title="pleasanter.sql" linenums="1"
create user 'Implem.Pleasanter_Owner'@'%' identified by '{{Owner password}}';
grant create, alter, index, drop on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'%';
grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'%' with grant option;
create user 'Implem.Pleasanter_User'@'%' identified by '{{User password}}';
grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_User'@'%';
```

上記の例では、プリザンターのデータベース名に[Service.json](../../parameters/service-json.md)の`"Name"`の既定値である「Implem.Pleasanter」を指定しています。[Service.json](../../parameters/service-json.md)の`"Name"`を既定値から変更する場合、SQL文でデータベース名を指定している箇所（上記`Implem.Pleasanter`の箇所）を、[Service.json](../../parameters/service-json.md)の`"Name"`の変更後と揃えてください。

また、`identified by`の後で指定する各MySQLユーザアカウントのパスワード文字列は、上記`.env`ファイルと一致させてください。

### 1-6 compose.yamlファイル

`compose.yaml`ファイルを作成します。

``` yaml title="compose.yaml" linenums="1"
services:
  db:
    container_name: mysql
    image: mysql:8.4
    environment:
      - MYSQL_ROOT_PASSWORD
    volumes:
      - type: volume
        source: my_data
        target: /var/lib/mysql
      - ./docker-entrypoint-initdb.d:/docker-entrypoint-initdb.d
    healthcheck:
        test: mysqladmin ping -h 127.0.0.1 -u root -p${MYSQL_ROOT_PASSWORD}
        interval: 10s
        timeout: 10s
        retries: 6
  pleasanter:
    build:
      context: .
      dockerfile: ./Pleasanter/Dockerfile
      args:
        - VERSION=${PLEASANTER_VER}
    container_name: pleasanter_${PLEASANTER_VER}
    depends_on:
      db:
        condition: service_healthy
    ports:
      - '50001:8080'
    environment:
      Implem.Pleasanter_Rds_MySQL_SaConnectionString: ${Implem_Pleasanter_Rds_MySQL_SaConnectionString}
      Implem.Pleasanter_Rds_MySQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_MySQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_MySQL_UserConnectionString: ${Implem_Pleasanter_Rds_MySQL_UserConnectionString}
  codedefiner:
    build:
      context: .
      dockerfile: ./CodeDefiner/Dockerfile
    container_name: codedefiner
    depends_on:
      db:
        condition: service_healthy
    environment:
      Implem.Pleasanter_Rds_MySQL_SaConnectionString: ${Implem_Pleasanter_Rds_MySQL_SaConnectionString}
      Implem.Pleasanter_Rds_MySQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_MySQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_MySQL_UserConnectionString: ${Implem_Pleasanter_Rds_MySQL_UserConnectionString}
volumes:
  my_data:
    name: ${COMPOSE_PROJECT_NAME:-default}_my_data_volume
```

## 2. コンテナイメージのビルド

以下コマンドを実行します。

```bash
docker compose build
```

## 3. CodeDefinerの実行

以下コマンドを実行します。

```bash
docker compose run --rm codedefiner _rds /l "<言語>" /z "<タイムゾーン>"
```

| 引数 | 設定例     | 説明                                                 |
| :--- | :--------- | :--------------------------------------------------- |
| /l   | ja         | Service.jsonのDefaultLanguageの値を書き換えます [^1] |
| /z   | Asia/Tokyo | Service.jsonのTimeZoneDefaultの値を書き換えます [^1] |

[^1]: 言語、タイムゾーンは以下マニュアルページを参照ください。  
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

日本語環境で利用する場合は、以下コマンドとなります。

``` bash
docker compose run --rm codedefiner _rds /l "ja" /z "Asia/Tokyo"
```

途中で`Type "y" (yes) if the license is correct, otherwise type "n" (no).`と表示されたら ++y++ を入力してください。

!!! note
    コンソールログに以下のようにバージョンが出力されます。ここで表示されるバージョンは常に「DockerHubで公開されている最新のプリザンターのバージョン」となります。このコンソールログ表示の仕様は、`.env`ファイルの`{{Version}}`に最新よりも前のバージョンを指定した場合も同様ですが、データベースは`{{Version}}`に準拠した内容で作成されますので、プリザンターの動作上の問題はありません。

    ``` bash
    <INFO> Starter.Main: Implem.CodeDefiner 1.4.10.1
    ```

## 4. プリザンター起動

コンテナを作成、プリザンターを起動します。

```bash
docker compose up -d pleasanter
```

ブラウザでアクセスします。

```text
http://localhost:50001
```

ログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力します。ログイン後、パスワードの変更を求められますので適宜パスワードを設定してください。

## 5. コンテナの停止と削除

コンテナの停止は以下のコマンドで行います。

```bash
docker compose stop
```

停止したコンテナを再開する場合は以下のコマンドを実行します。

```bash
docker compose start
```

コンテナを停止してもDBデータは削除されません。再開する際にはデータがそのまま利用できます。

---

コンテナの削除は以下のコマンドで行います。  
コンテナを削除してもDBデータ（ボリューム）は削除されません。

```bash
docker compose down
```

なおコンテナを削除した場合は、再開はできません。起動したい場合はコンテナを作成してください。  
以下のコマンドを実行します。これによりDBのコンテナも一緒に作成され残っているDBデータもそのまま利用できます。

```bash
docker compose up -d pleasanter
```

コンテナを削除する時に同時にデータ（ボリューム）を削除する場合はボリュームを削除するオプションを付けて実行します。

```bash
docker compose down -v
```

## 対応バージョン

| 対応バージョン | 内容                                                                                                                                                                                                            |
| :------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題の解消に伴いマニュアルを公開 [^2] |
| 1.4.18.0 以降  | MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能の追加に伴いマニュアルを修正                                                                                                          |

[^2]: プリザンターはVer1.4.9.0以降でMySQLに対応しましたが、本手順はVer1.4.10.0以降でなければ実施できません。

## 関連情報

-   [Dockerで起動する](getting-started-pleasanter-docker.md)
-   [Dockerイメージを使用しパラメータを既定値から変更して起動する](change-parameters-at-docker-image.md)
-   [Dockerイメージのプリザンターをバージョンアップする](../../version-up-migration/version-up-manually/version-up-pleasanter-docker.md)
