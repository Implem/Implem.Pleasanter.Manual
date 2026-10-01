---
title: GitHubリポジトリのソースコードおよびDockerで起動する
category: GitHubリポジトリのソースファイルで起動する
order: '0'
status: ''
parts: ''
urlstring: setup-by-github-sources-on-docker
translationKey: setup-by-github-sources-on-docker
shortname: ''
created: 2024-12-05
updated: 2026-07-17
---

## 概要

[プリザンターの公式GitHubリポジトリ](https://github.com/Implem/Implem.Pleasanter)からソースコードをダウンロードし、Dockerコンテナを作成してプリザンターを起動する手順を説明します。

本手順を使用すると、ソースコード改変を行った際の動作検証ができます。

-   第1部　セットアップ手順  
-   第2部　バージョンアップ手順  
-   第3部　コンテナの停止と削除

## 制限事項

1. Dockerでプリザンターを運用する場合、パラメータファイルの設定変更時は、プリザンターの停止・再起動だけでなく、「docker compose build」コマンドによるビルドを再実施してください。ビルドを行っていない状態では、プリザンターを再起動してもパラメータファイルの変更が反映されません。
2. MySQLでDockerを利用する際、プリザンターのバージョンは1.4.10.0 以降としてください。プリザンターはVer1.4.9.0以降でMySQLに対応しましたが、本手順はVer1.4.10.0以降でなければ実施できません。

## 前提条件

1. 本手順で記述する「docker-compose.yml」では、データベースサーバとしてPostgreSQLまたはMySQLの公式Dockerイメージを指定しており、データベースサーバの動作は各Dockerイメージの仕様に依存します。  

    -   [postgres - Official Image | Docker Hub](https://hub.docker.com/_/postgres/)  
    -   [mysql - Official Image | Docker Hub](https://hub.docker.com/_/mysql/)

2. GitおよびDocker Composeのコマンドを使用します。  

    -   [Git](https://git-scm.com/)  
    -   [Docker Compose | Docker Docs](https://docs.docker.com/compose/)  

    ※本手順は、GitおよびDocker ComposeのCLIコマンドについて、ある程度の実務経験がある利用者を想定しています。各コマンドの概念および仕様については公式ドキュメント等で確認してください。

3. Docker Composeを使用して、プリザンターのソースコード一式からDockerイメージを作成します。プリザンターの起動はDockerのコンテナ上で行います。

---

## 第1部　セットアップ手順

プリザンターを初期セットアップする手順は以下の通りです。
1. GitHubリポジトリのクローン
2. コンテナ運用に関わるファイルの編集
   1. .env
   2. docker-compose.yml
   3. Implem.Pleasanter\Dockerfile
   4. Implem.CodeDefiner\Dockerfile
   5. docker-entrypoint-initdb.d\pleasanter.sql
3. パラメータファイルの編集
   1. Rds.json
   2. Service.json
4. コンテナイメージのビルド
5. CodeDefinerの実行
6. プリザンターの起動

### 1.GitHubリポジトリのクローン

以下コマンドを実行し、GitHubのリモートリポジトリ上にある、プリザンターのソースコードをダウンロードします。

```
git clone https://github.com/Implem/Implem.Pleasanter
```

以下フォルダが作成されたことを確認します。

```text
.
+-- Implem.Pleasanter
    +-- .git
    +-- .github
    +-- Implem.CodeDefiner
    +-- Implem.DefinitionAccessor
    +-- Implem.DisplayAccessor
    +-- Implem.Factory
    +-- Implem.Libraries
    +-- Implem.ParameterAccessor
    +-- Implem.Pleasanter
    +-- ……
    |
    |
（以下省略）
```

### 2.コンテナ運用に関わるファイルの編集

以下ファイルを編集します。

1. 環境変数を記述する .env   
2. Dockerイメージの構成を記述する docker-compose.yml  
3. CodeDefinerのビルド内容を記述する Implem.CodeDefiner\Dockerfile  
4. プリザンターのビルド内容を記述する Implem.Pleasanter\Dockerfile  
5. MySQLのユーザアカウント作成用SQLを記述する docker-entrypoint-initdb.d\pleasanter.sql

#### 1.「.env」の編集

「\Implem.Pleasanter\\.env」を新規作成し、以下の通り編集します。

<details markdown="1">
<summary style="font-weight:bold">PostgreSQLの場合</summary>

.envファイルの例です。 {{ ... }} は、後述の説明を参考に適宜修正してください。

```txt
POSTGRES_USER={{Sa User}}
POSTGRES_PASSWORD={{Sa Password}}
POSTGRES_DB={{System DB}}
POSTGRES_HOST_AUTH_METHOD=scram-sha-256
POSTGRES_INITDB_ARGS="--auth-host=scram-sha-256 --encoding=UTF-8"
Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString='Server=db;Database={{System DB}};UID={{Sa User}};PWD={{Sa password}}'
Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}}'
Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}}'
```

**※説明**
POSTGRES ではじまる環境変数はPostgreSQLのDocker公式イメージが使用します。コンテナの初期化時に initdb が実行され、環境変数の値を使ってPostgreSQLの初期設定が行われます。

[postgres - Official Image | Docker Hub](https://hub.docker.com/_/postgres)  
[docker-library/postgres: Docker Official Image packaging for Postgres](https://github.com/docker-library/postgres)

SaConnectionString は最初にPostgreSQLにスーパーユーザで接続するための設定が一行で表現されています。PostgreSQLの環境変数の内容と SaConnectionString に記述されている内容を合わせる必要があります。

|名称|内容|
|---|---|
|Server|Compose ファイルのサービス名 (db) に設定する|
|Database|環境変数の POSTGRES_DB と揃える|
|UID|環境変数の POSTGRES_USER と揃える|
|PWD|環境変数の POSTGRES_PASSWORD と揃える|

OwnerConnectionString と UserConnectionString はそれぞれのユーザで接続するための設定が一行で表現されています。

|名称|内容|
|---|---|
|PWD|任意のパスワード文字列。Owner と User のパスワードは別々が望ましい|

</details>

<details markdown="1">
<summary style="font-weight:bold">MySQLの場合</summary>

.envファイルの例です。 {{ ... }} は、後述の説明を参考に適宜修正してください。

```txt
MYSQL_ROOT_PASSWORD={{Sa Password}}
Implem_Pleasanter_Rds_MySQL_SaConnectionString='Server=db;Database=mysql;UID=root;PWD={{Sa password}}'
Implem_Pleasanter_Rds_MySQL_OwnerConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD={{Owner password}}'
Implem_Pleasanter_Rds_MySQL_UserConnectionString='Server=db;Database=#ServiceName#;UID=#ServiceName#_User;PWD={{User password}}'
```

**※説明**
MySQLのDocker公式イメージで必須とされる環境変数のうち、本手順ではデフォルトのスーパーユーザアカウント（root）のパスワード設定先である MYSQL_ROOT_PASSWORD を記述します。

[mysql - Official Image | Docker Hub](https://hub.docker.com/_/mysql)  
[docker-library/mysql: Docker Official Image packaging for MySQL Community Server](https://github.com/docker-library/mysql)

|名称|内容|
|---|---|
|MYSQL_ROOT_PASSWORD|任意のパスワード文字列を指定する|

SaConnectionString は最初にMySQLにスーパーユーザで接続するための設定が一行で表現されています。MySQLの環境変数の内容と SaConnectionString に記述されている内容を合わせる必要があります。  

|名称|内容|
|---|---|
|Server|Compose ファイルのサービス名 (db) を指定する|
|Database|MySQLのデフォルトのシステムデータベース名（mysql）を指定する|
|UID|MySQLのデフォルトのスーパーユーザ名（root）を指定する|
|PWD|環境変数の MYSQL_ROOT_PASSWORD と揃える|

OwnerConnectionString と UserConnectionString はそれぞれのユーザで接続するための設定が一行で表現されています。

|名称|内容|
|---|---|
|PWD|任意のパスワード文字列。Owner と User のパスワードは別々が望ましい|

</details>

#### 2.「docker-compose.yml」の編集

「\Implem.Pleasanter\docker-compose.yml」を開いて以下の通り編集します。

<details markdown="1">
<summary style="font-weight:bold">PostgreSQLの場合</summary>

```txt
services:
  pleasanter:
    build:
      context: .
      dockerfile: ./Implem.Pleasanter/Dockerfile
    environment:
      Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
      Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
    container_name: Implem.Pleasanter
    depends_on:
      - db
    ports:
      - '50001:8080'
  codedefiner:
    build:
      context: .
      dockerfile: ./Implem.CodeDefiner/Dockerfile
    environment:
      Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_SaConnectionString}
      Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString: ${Implem_Pleasanter_Rds_PostgreSQL_UserConnectionString}
    container_name: Implem.CodeDefiner
    depends_on:
      - db
  db:
    container_name: postgres
    image: postgres:17
    environment:
      - POSTGRES_USER
      - POSTGRES_PASSWORD
      - POSTGRES_DB
      - POSTGRES_HOST_AUTH_METHOD
      - POSTGRES_INITDB_ARGS
    volumes:
      - type: volume
        source: pg_data
        target: /var/lib/postgresql/data
volumes:
  pg_data:
    name: ${COMPOSE_PROJECT_NAME:-default}_pg_data_volume
```

</details>

<details markdown="1">
<summary style="font-weight:bold">MySQLの場合</summary>

```txt
services:
  pleasanter:
    build:
      context: .
      dockerfile: ./Implem.Pleasanter/Dockerfile
    environment:
      Implem.Pleasanter_Rds_MySQL_SaConnectionString: ${Implem_Pleasanter_Rds_MySQL_SaConnectionString}
      Implem.Pleasanter_Rds_MySQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_MySQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_MySQL_UserConnectionString: ${Implem_Pleasanter_Rds_MySQL_UserConnectionString}
    container_name: Implem.Pleasanter
    depends_on:
      db:
        condition: service_healthy
    ports:
      - '50001:8080'
  codedefiner:
    build:
      context: .
      dockerfile: ./Implem.CodeDefiner/Dockerfile
    environment:
      Implem.Pleasanter_Rds_MySQL_SaConnectionString: ${Implem_Pleasanter_Rds_MySQL_SaConnectionString}
      Implem.Pleasanter_Rds_MySQL_OwnerConnectionString: ${Implem_Pleasanter_Rds_MySQL_OwnerConnectionString}
      Implem.Pleasanter_Rds_MySQL_UserConnectionString: ${Implem_Pleasanter_Rds_MySQL_UserConnectionString}
    container_name: Implem.CodeDefiner
    depends_on:
      db:
        condition: service_healthy
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
volumes:
  my_data:
    name: ${COMPOSE_PROJECT_NAME:-default}_my_data_volume
```

</details>

#### 3.「Implem.CodeDefiner\Dockerfile」の編集

「\Implem.Pleasanter\Implem.CodeDefiner\Dockerfile」を開いて以下の通り編集します。

<details markdown="1">
<summary style="font-weight:bold">PostgreSQL／MySQL共通</summary>

```txt
FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Implem.CodeDefiner/Implem.CodeDefiner.csproj", "Implem.CodeDefiner/"]
COPY ["Implem.DefinitionAccessor/Implem.DefinitionAccessor.csproj", "Implem.DefinitionAccessor/"]
COPY ["Implem.ParameterAccessor/Implem.ParameterAccessor.csproj", "Implem.ParameterAccessor/"]
COPY ["Implem.DisplayAccessor/Implem.DisplayAccessor.csproj", "Implem.DisplayAccessor/"]
COPY ["Implem.Libraries/Implem.Libraries.csproj", "Implem.Libraries/"]
COPY ["Rds/Implem.IRds/Implem.IRds.csproj", "Rds/Implem.IRds/"]
COPY ["Implem.Factory/Implem.Factory.csproj", "Implem.Factory/"]
COPY ["Rds/Implem.PostgreSql/Implem.PostgreSql.csproj", "Rds/Implem.PostgreSql/"]
COPY ["Rds/Implem.SqlServer/Implem.SqlServer.csproj", "Rds/Implem.SqlServer/"]
COPY ["Rds/Implem.MySql/Implem.MySql.csproj", "Rds/Implem.MySql/"]
COPY ["Implem.Pleasanter/Implem.Pleasanter.csproj", "Implem.Pleasanter/"]
RUN dotnet restore "Implem.CodeDefiner/Implem.CodeDefiner.csproj"
COPY . .
RUN dotnet build "Implem.CodeDefiner/Implem.CodeDefiner.csproj" -c Release -o /app/build/Implem.CodeDefiner
RUN dotnet build "Implem.Pleasanter/Implem.Pleasanter.csproj" -c Release -o /app/build/Implem.Pleasanter

FROM build AS publish
RUN dotnet publish "Implem.CodeDefiner/Implem.CodeDefiner.csproj" -c Release -o /app/publish/Implem.CodeDefiner
RUN dotnet publish "Implem.Pleasanter/Implem.Pleasanter.csproj" -c Release -o /app/publish/Implem.Pleasanter

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
WORKDIR /app/Implem.CodeDefiner

ENTRYPOINT ["dotnet", "Implem.CodeDefiner.dll"]
```

</details>

#### 4.「Implem.Pleasanter\Dockerfile」の編集

「\Implem.Pleasanter\Implem.Pleasanter\Dockerfile」を開いて以下の通り編集します。

<details markdown="1">
<summary style="font-weight:bold">PostgreSQL／MySQL共通</summary>

```txt
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
RUN apt-get update && apt-get install -y \
    libgdiplus \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Implem.Pleasanter/Implem.Pleasanter.csproj", "Implem.Pleasanter/"]
COPY ["Implem.DefinitionAccessor/Implem.DefinitionAccessor.csproj", "Implem.DefinitionAccessor/"]
COPY ["Implem.ParameterAccessor/Implem.ParameterAccessor.csproj", "Implem.ParameterAccessor/"]
COPY ["Implem.DisplayAccessor/Implem.DisplayAccessor.csproj", "Implem.DisplayAccessor/"]
COPY ["Implem.Libraries/Implem.Libraries.csproj", "Implem.Libraries/"]
COPY ["Rds/Implem.IRds/Implem.IRds.csproj", "Rds/Implem.IRds/"]
COPY ["Implem.Plugins/Implem.Plugins.csproj", "Implem.Plugins/"]
COPY ["Implem.Factory/Implem.Factory.csproj", "Implem.Factory/"]
COPY ["Rds/Implem.PostgreSql/Implem.PostgreSql.csproj", "Rds/Implem.PostgreSql/"]
COPY ["Rds/Implem.SqlServer/Implem.SqlServer.csproj", "Rds/Implem.SqlServer/"]
COPY ["Rds/Implem.MySql/Implem.MySql.csproj", "Rds/Implem.MySql/"]
RUN dotnet restore "Implem.Pleasanter/Implem.Pleasanter.csproj"
COPY . .
WORKDIR "/src/Implem.Pleasanter"
RUN dotnet build "Implem.Pleasanter.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Implem.Pleasanter.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Implem.Pleasanter.dll"]
```

</details>

#### 5.「docker-entrypoint-initdb.d」フォルダの作成とSQL文の記述

PostgreSQLを利用する場合は、実施不要です。

MySQLを利用する場合は、以下手順を実施します。

??? note "MySQLを利用する場合"

    1.  「\Implem.Pleasanter\docker-entrypoint-initdb.d」フォルダを新規作成します。

    2.  「\Implem.Pleasanter\docker-entrypoint-initdb.d」フォルダの中に、MySQLのユーザアカウント作成用SQLを記述した「pleasanter.sql」ファイルを格納します。  

        説明

        「Implem.Pleasanter\docker-entrypoint-initdb.d」フォルダは、docker-compose.ymlファイル内「db」サービス配下の「volumes」の設定により、MySQLのコンテナの「docker-entrypoint-initdb.d」ディレクトリに自動的にマウントされるフォルダです。

        コンテナにマウントされた「docker-entrypoint-initdb.d」ディレクトリ内のファイルに記載されているSQLコマンドは、MySQLのコンテナの起動時に自動実行されます。

        ``` sql title="pleasanter.sqlファイルの作成例" linenums="1"
        create user 'Implem.Pleasanter_Owner'@'%' identified by '{{Owner password}}';
        grant create, alter, index, drop on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'%';
        grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'%' with grant option;
        create user 'Implem.Pleasanter_User'@'%' identified by '{{User password}}';
        grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_User'@'%';
        ```

        上記の例では、プリザンターのデータベース名に[Service.json](../../parameters/service-json.md)の"Name"の既定値である「Implem.Pleasanter」を指定しています。[Service.json](../../parameters/service-json.md)の"Name"を既定値から変更する場合、SQL文でデータベース名を指定している箇所（上記「Implem.Pleasanter」の箇所）を、[Service.json](../../parameters/service-json.md)の"Name"の変更後と揃えてください。

        また、identified byの後で指定する各MySQLユーザアカウントのパスワード文字列は、手順2.1の.envファイルと一致させてください。

### 3.パラメータファイルの記述

以下ファイルを編集します。

1. データベース構成情報を記述する [Rds.json](../../parameters/rds-json.md)  
2. 言語、タイムゾーン等を記述する [Service.json](../../parameters/service-json.md)  

#### 1. [Rds.json](../../parameters/rds-json.md)の編集

「\Implem.Pleasanter\Implem.Pleasanter\App_Data\Parameters\Rds.json」を開いて"Dbms"に"PostgreSQL"（既定値）または"MySQL"を設定します。

その他、既定値から変更したい[Rds.json](../../parameters/rds-json.md)の項目を修正します。

<details markdown="1">
<summary style="font-weight:bold">PostgreSQLの修正例</summary>

```txt
{
    "Dbms": "PostgreSQL",
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
    "MySqlConnectionHots": "%"
}
```

</details>

<details markdown="1">
<summary style="font-weight:bold">MySQLの修正例</summary>

```txt
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
    "MySqlConnectionHots": "%"
}
```

</details>

#### 2. [Service.json](../../parameters/service-json.md)の編集

「\Implem.Pleasanter\Implem.Pleasanter\App_Data\Parameters\Service.json」を開いて"TimeZoneDefault"および"DefaultLanguage"を修正します。

**修正例（日本語環境の場合）**

|内容|設定例|
|:--|:--|
|TimeZoneDefault|Asia/Tokyo|
|DefaultLanguage|ja|

言語、タイムゾーンは以下マニュアルページを参照ください。

-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

**※説明**  
本手順のように[Service.json](../../parameters/service-json.md)を編集してセットアップすると、CodeDefinerの実行時に /l /z オプションの指定を省略できます。

-   [CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)

### 4.コンテナイメージのビルド

以下すべての手順において、カレントディレクトリは上記手順1.で確認した「Implem.Pleasanter」としてください。  
以下コマンドを実行します。

```txt
cd Implem.Pleasanter
```

以下コマンドを実行します。  
環境によりますが、初回のビルドには10分～15分程度の時間がかかる場合があります。

```bash
docker compose build
```

### 5.CodeDefinerの実行

以下コマンドを実行します。

```bash
docker compose run --rm codedefiner _rds
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力してください。

### 6.プリザンターの起動

コンテナを作成、プリザンターを起動します。

```bash
docker compose up -d pleasanter
```

ブラウザでアクセスします。

<http://localhost:50001>

ログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力します。  ログイン後、パスワードの変更を求められますので適宜パスワードを設定してください。

---

## 第2部　バージョンアップ手順

プリザンターをバージョンアップする手順は以下の通りです。
1. プリザンターの停止
2. GitHubリポジトリのプル
   1. GitHubのリモートリポジトリの更新有無を確認
   2. 「.env」、「docker-compose.yml」等の修正を退避
   3. 退避データがGitに保存されていることを確認
   4. バージョンアップ内容のダウンロード
   5. 手順2.2.で退避した「.env」、「docker-compose.yml」等の修正の復元  
      ※必要に応じて『5-追加手順.「Unmerged paths:」が表示された際の解消方法』を実施
   6. リモートリポジトリ上に更新がないことの確認
   7. 退避した「.env」、「docker-compose.yml」等の情報の削除確認
3. コンテナイメージのビルド
4. CodeDefinerの実行
5. プリザンターのコンテナ作成・起動

### 1.プリザンターの停止

以下コマンドを実行し、プリザンターのコンテナを停止します。

```bash
docker compose stop
```

### 2.GitHubリポジトリのプル

「git pull」コマンドでソースコードファイルを最新化します。

**※備考**  
本マニュアルの「第1部　セットアップ手順」の通りに初期セットアップを行った場合は、「.env」、「docker-compose.yml」等、ローカルでDockerに関わるファイルの修正が行われています。またCommunity Editionでは、その他のソースコード変更もライセンスが許可する範囲内で自由に行えます。

ローカルで変更が行われている状態で「git pull」コマンドを実行すると、リモートリポジトリの変更箇所との衝突を表すエラーが表示される場合があります。  

以下、ローカルの修正箇所がリモートリポジトリの修正と衝突し、「git pull」を行えなかった場合に表示されるエラーメッセージの例です。  
以下エラーメッセージが表示された場合は、「git pull」実行後、ローカルのファイルにリモートリポジトリの修正が一切反映されていません。（衝突していない箇所もローカルに反映されません。）

```bash
>git pull
Updating {{旧ID}}..{{新ID}}
error: Your local changes to the following files would be overwritten by merge:
         Implem.Pleasanter/App_Data/Parameters/Rds.json
Please commit your changes or stash them before you merge.
Aborting
```

対策として、事前にそれらの修正情報を退避するGitのコマンドを使用します。

※なお、ローカルの修正箇所がリモートリポジトリの修正箇所と1箇所も衝突していない場合、「git pull」コマンドは問題なく実行完了します。「git pull」がエラーになるかどうかは実行するまでわかりません。

以下、ソースファイルに衝突が発生している・発生していないにかかわらず実施可能な、共通のバージョンアップ手順です。

事前準備なく「git pull」コマンドのみ実行する場合と比較して手順は増えますが、状況をチェックするポイントが追加されているため、確実にバージョンアップ時の作業ミスを予防できます。

#### 1.GitHubのリモートリポジトリの更新有無を確認

以下コマンドを実行します。

```bash
git fetch
git log origin/main
```

「git fetch」コマンドを実行した時点では、ローカルのファイルは更新されず、更新の情報のみリモートリポジトリから取得されます。  
「git log origin/main」コマンドの実行時に以下ログが表示された場合（「**HEAD -> main**」がGitログの先頭にない状態）、まだローカルに取り込んでいない更新情報が存在します。

```bash
>git log origin/main
commit {{ID}} (tag: Pleasanter_1.4.99.1, origin/main, origin/HEAD)
Author: Commiter Hayato <{{メールアドレス}}>
Date:   Mon Dec 02 10:00:00 2024 +0900

    ## Bug fixed

commit {{ID}} (HEAD -> main, tag: Pleasanter_1.4.99.0)
Author: Commiter Hayato <{{メールアドレス}}>
Date:   Sun Dec 01 10:00:00 2024 +0900

    ## Added new features / Bug fixed

～～以下略～～

:
```
「git log origin/main」コマンドの結果確認後、キーボードの「Q」キーを押し、Gitログの確認モードを終了します。  
その後、手順2.2以降を実施してください。

なお、「**HEAD -> main**」がGitログの先頭にある場合、プリザンターのバージョンアップは不要です。

#### 2.「.env」、「docker-compose.yml」等の修正を退避

以下コマンドを実行します。ダブルクォーテーションで囲まれたメッセージを追加し、任意のコメントを付与することができます。

```bash
git stash push -m "1.x.x.xにバージョンアップする前の退避情報"
```

「git stash push」コマンドの実行後、ローカルのファイルの修正内容がGitによって退避され、修正前の内容に変更されます。

#### 3.退避データがGitに保存されていることを確認

以下コマンドを実行します。

```bash
git stash list
```

「git stash list」コマンドの実行後ログに「stash@{0}:　…」等の情報が表示され、変更情報が保存されたことを確認します。

```bash
>git stash list
stash@{0}: On main: 1.x.x.xにバージョンアップする前の退避情報
```

#### 4.バージョンアップ内容のダウンロード

以下コマンドを実行します。

```bash
git pull
```

「git pull」コマンドの実行後、ローカルのファイルが次期バージョンの内容に更新されます。

#### 5.手順2.2.で退避した「.env」、「docker-compose.yml」等の修正の復元

以下コマンドを実行します。

```bash
git stash pop
```

**※注意**  
「git stash pop」コマンドの実行後、以下のような「**Unmerged paths:**」に続くログが表示された場合は、ファイル更新時に「衝突」が発生しています。   
**後述の「5-追加手順.「Unmerged paths:」が表示された際の解消方法」を参照し、「衝突」を解消してください。**

```bash
>git stash pop

～～中略～～

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both modified:   Implem.Pleasanter/App_Data/Parameters/Rds.json
```

なお、「git stash pop」コマンドの実行後は「Unmerged paths:」以外にも、様々なログが表示されます。  
以下のような、「Unmerged paths:」以外のログは表示されても問題はありません。

```bash
>git stash pop
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Implem.CodeDefiner/Dockerfile
        modified:   Implem.Pleasanter/App_Data/Parameters/Rds.json
        modified:   Implem.Pleasanter/Dockerfile
        modified:   docker-compose.yml

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .env

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} ({{ここにIDが表示されている}})
```

「Unmerged paths:」を見落としたかもしれず再度確認したい場合は、以下の通り「git status」コマンドを実行してください。

```bash
git status
```

#### 5-追加手順.「Unmerged paths:」が表示された際の解消方法

「git pop stash」コマンドまたは「git status」コマンドの実行後、「Unmerged paths:」が表示されていない場合は実施不要です。

ソースファイル修正の衝突を解消する手順は、以下の通りです。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

1. 衝突の解消が必要なファイルの確認
2. 衝突したファイルのバックアップ
3. 衝突したファイルをGitコマンドで修正  

    -   （解消方法a. ）ローカルの修正を反映する  
    -   （解消方法b. ）リモートリポジトリの修正を反映する

4. Git情報のリカバリ

**1.衝突の解消が必要なファイルの確認**

「Unmerged paths:」に続いて表示されたすべてのファイルのパスをコピーします。

後述の手順2.5-追加手順.3のコマンドに転記するため、テキストエディタ等に退避します。

```txt
Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both modified:   Implem.Pleasanter/App_Data/Parameters/Rds.json
```

上記のログが表示されている場合、文字列「Implem.Pleasanter/App_Data/Parameters/Rds.json」をテキストエディタ等に退避します。

**2.衝突したファイルのバックアップ**

手順2.5-追加手順.1で確認したパスについて、実際のファイルをすべて別の場所（Implem.Pleasanterディレクトリの外）にバックアップします。

退避先でファイルを開き、下図のような衝突の内容がGitによって書き込まれていることを確認します。（識別しやすいように色分けしています。）

![衝突した内容が書き込まれたファイルを開いたところ。Git が入れた衝突箇所が色分けされている](https://pleasanter.org/files/images/ja/setup/installation/running-from-source/assets/d983793686ad4bcaabc625e0ed89cd18.png)

**3.衝突したファイルをGitコマンドで修正**

すべてのファイルについて、以下に示すいずれかの解消方式を選択し、コマンドを実行します。  

-   （解消方法a. ）ローカルの修正を反映する  
-   （解消方法b. ）リモートリポジトリの修正を反映する

コマンドは引き続き、Implem.Pleasanterディレクトリで実行してください。

**（解消方法a. ）ローカルの修正を反映する**

以下コマンドを実行します。

```
git checkout --theirs Implem.Pleasanter/App_Data/Parameters/Rds.json
```

「git checkout --theirs」に続けて衝突の解消が必要なファイル名を記述します。

コマンド実行後、Gitによって「Implem.Pleasanter/App_Data/Parameters/Rds.json」は下図のように修正されます。

![git checkout --theirs の実行後の Rds.json。衝突箇所が解消された状態](https://pleasanter.org/files/images/ja/setup/installation/running-from-source/assets/09026657f3a646809e1dc01e2c1c6435.png)

バージョンアップ以前からローカルで修正していた"Dbms"の設定値"MySQL"が、バージョンアップ後も引き続き設定されます。  
プリザンターのバージョンアップによる新しい"Dbms"の既定値"NewDefaultDbms"は取り消されます。

**（解消方法b. ）リモートリポジトリの修正を反映する**

以下コマンドを実行します。

```
git checkout --ours Implem.Pleasanter/App_Data/Parameters/Rds.json
```

コマンド実行後、Gitによって「Implem.Pleasanter/App_Data/Parameters/Rds.json」は下図のように修正されます。

![git checkout --ours の実行後の Rds.json。衝突箇所が解消された状態](https://pleasanter.org/files/images/ja/setup/installation/running-from-source/assets/592de3af786349458522e6cd8c9fe842.png)

プリザンターのバージョンアップによる新しい"Dbms"の既定値"NewDefaultDbms"に書き換えられます。  
バージョンアップ以前からローカルで修正していた"Dbms"の設定値"MySQL"は取り消されます。

**4.Git情報のリカバリ**

以下手順を実施し、衝突によって発生したGitの不整合を修正します。

「git add .」コマンドを実行し、すべてのファイルの衝突が解消済みである旨をGitに登録します。

```bash
git add .
```

ソースの変更がステージされたため、ステージを取り消して手順2.1実施前の状態に戻す必要があります。  
「git reset HEAD」コマンドを実行し、ステージを取り消します。

```bash
git reset HEAD
```

手順2.3と同様、「git stash list」コマンドを実行します。  
衝突が発生したため、手順2.退避した修正情報が自動で削除されていません。

```bash
>git stash list
stash@{0}: On main: 1.x.x.xにバージョンアップする前の退避情報
```

「git stash drop」コマンドを実行し、手順2.2で退避した修正情報を手動で削除します。

```bash
git stash drop
```

ソースファイル修正で発生した衝突が解消されました。引き続き手順2.6.以降を実施してください。

</details>

#### 6.リモートリポジトリ上に更新がないことの確認

「git pull」コマンドの再実行後に「Already up to date.」が表示されることをもって、Git情報の整合性が保たれていることの最終確認を行います。  
以下コマンドを実行します。

```bash
git pull
```

「git pull」コマンドの実行後、以下ログが表示された場合は、問題なくローカルファイルにプリザンターのバージョンアップ内容が反映されています。

```bash
>git pull
Already up to date.
```

「git pull」コマンドの実行後、以下ログが表示された場合は、手順2.5.でファイルを更新した際に「衝突」が発生しています。（手順2.5.で衝突を検知したメッセージは他メッセージに紛れやすいため、見逃された可能性があります。）  
**前述の「5-追加手順.「Unmerged paths:」が表示された際の解消方法」を参照し、「衝突」を解消してください。**

```bash
>git pull
error: Pulling is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.
```

#### 7.退避した「.env」、「docker-compose.yml」等の情報の削除確認

以下コマンドを実行します。

```
git stash list
```

手順2.3.で確認した変更情報（「stash@{0}:　…」等）は、「git stash pop」で復元した際に自動で削除されたため、（または、「git stash drop」コマンドによって手動で削除されたため、）何も表示されません。

以上で、GitHubリポジトリのプルは完了です。

### 3.コンテナイメージのビルド

以下コマンドを実行します。

```
docker compose build
```

### 4.CodeDefinerの実行

以下コマンドを実行します。

```bash
docker compose run --rm codedefiner _rds
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力してください。

### 5.プリザンターのコンテナ作成・起動

1. 以下コマンドを実行します。  
    停止して残っていた現行バージョンのプリザンターのコンテナが、次期バージョンのコンテナとして再作成され、起動します。

    ```
    docker compose up -d pleasanter
    ```

2. ブラウザでアクセスし、ログインします。

    -   <http://localhost:50001>

3. ログイン後、ナビゲーションメニューの「ヘルプ」－「バージョン」をクリックし、バージョンが正しいことを確認します。

---

## 第3部　コンテナの停止と削除

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
コンテナを削除してもDBデータ(ボリューム)は削除されません。

```bash
docker compose down
```

なおコンテナを削除した場合は、再開はできません。起動したい場合はコンテナを作成してください。  
以下のコマンドを実行します。これによりDBのコンテナも一緒に作成され残っているDBデータもそのまま利用できます。

```bash
docker compose up -d pleasanter
```

コンテナを削除する時に同時にデータ(ボリューム)を削除する場合はボリュームを削除するオプションを付けて実行します。

```bash
docker compose down -v
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能の追加に伴いマニュアルを修正|

## 関連情報

-   [プリザンターの公式GitHubリポジトリ](https://github.com/Implem/Implem.Pleasanter)
-   [postgres - Official Image | Docker Hub](https://hub.docker.com/_/postgres/)
-   [mysql - Official Image | Docker Hub](https://hub.docker.com/_/mysql/)
-   [Git](https://git-scm.com/)
-   [Docker Compose | Docker Docs](https://docs.docker.com/compose/)
-   [postgres - Official Image | Docker Hub](https://hub.docker.com/_/postgres)
-   [docker-library/postgres: Docker Official Image packaging for Postgres](https://github.com/docker-library/postgres)
-   [mysql - Official Image | Docker Hub](https://hub.docker.com/_/mysql)
-   [docker-library/mysql: Docker Official Image packaging for MySQL Community Server](https://github.com/docker-library/mysql)
-   [パラメータ設定：Service.json](../../parameters/service-json.md)
-   [パラメータ設定：Rds.json](../../parameters/rds-json.md)
-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)
-   [CodeDefinerのコマンド一覧](../../codedefiner/codedefiner-command.md)
