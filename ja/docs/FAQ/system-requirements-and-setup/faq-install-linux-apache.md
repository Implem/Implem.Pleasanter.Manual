---
title: WebサーバをApacheにしてPleasanterをインストールしたい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-install-linux-apache
translationKey: faq-install-linux-apache
shortname: プリザンターのインストール
created: 2019-01-06
updated: 2024-07-17
---

## 前提条件

1.  OSのセットアップ方法については記載しません。あらかじめOSはセットアップされていることとします。
1.  動作環境やスペックについての詳細はこちらを確認してください。

[FAQ：プリザンターの動作環境や推奨スペックが知りたい](faq-recommended-specifications.md)

## 概要

本説明は、以下に示す環境にプリザンターの動作環境を構築するための手順を示したものです。

| 対象       | 内容                         |
| ---------- | ---------------------------- |
| OS         | Red Hat Enterprise Linux 9.1 |
| DB         | PostgreSQL 14                |
| Webサーバ  | Apache                       |
| Platform   | .NET 6.0                     |
| Pleasanter | プリザンター 1.3.37.0        |

## 操作手順

### 1. .NET 6.0のインストール

#### ASP.NET Coreランタイムのインストール

``` bash
sudo dnf install aspnetcore-runtime-6.0
```

#### GDI+のインストール

``` bash
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo dnf install -y libgdiplus
```

### 2. PostgreSQLのセットアップ

#### パッケージリポジトリの登録

``` bash
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

#### PostgreSQLのインストール

```bash
sudo dnf module -y disable postgresql
sudo dnf install -y postgresql14-server postgresql14-contrib
```

#### データベースの初期化

```bash
sudo su - postgres -c '/usr/pgsql-14/bin/initdb -E UTF8 -A scram-sha-256 -W'
```

補足：

-   -A: 認証方式の指定
-   -W: パスワード入力プロンプトを表示するオプション
-   このタイミングでDBのpostgresユーザのパスワードを指定する

#### ログの出力設定

`/var/lib/pgsql/14/data/postgresql.conf`を開き、以下を設定します。

``` conf
log_destination = 'stderr'
logging_collector = on
log_line_prefix = '[%t]%u %d %p[%l]'
```

ログファイルは`/var/lib/pgsql/14/data/log`に保存されます。

#### サービス有効化

``` bash
sudo systemctl enable postgresql-14
```

#### OSのPostgreSQLユーザ設定

PostgreSQL管理用のユーザpostgres（OSのユーザ）にパスワードを設定します。

``` bash
sudo passwd postgres
```

#### 全⽂検索⽤モジュール（pg_trgm）のインストール

テキストの全⽂検索に必要なモジュール（pg_trgm）をインストールします。

1.  ユーザpostgresに切り替え、PostgreSQLへ接続します。

    ``` bash
    su - postgres
    psql -U postgres
    ```

1.  データベースImplem.Pleasanterを作成します。

    ``` sql
    create database "Implem.Pleasanter";
    ```

1.  データベースImplem.Pleasanterに切り替えます。

    ``` sql
    \c "Implem.Pleasanter";
    ```

1.  pg_trgmをインストールします。

    ``` sql
    create extension pg_trgm;
    ```

#### 外部からDBへのアクセスを許可する場合の設定。

1.  `/var/lib/pgsql/14/data/postgresql.conf`の以下の2行のコメントを解除して下記のように設定します。

    ``` conf title="/var/lib/pgsql/14/data/postgresql.conf" hl_lines="2 3"
    # - Connection Settings -
    listen_addresses = '*'  # what IP address(es) to listen on;
    port = 5432             # (change requires restart)
    ```

1.  /var/lib/pgsql/14/data/pg_hba.confに以下の行を追加します。Address欄にはアクセスを許可するIPアドレスの範囲を指定します。

   ``` conf title="/var/lib/pgsql/14/data/pg_hba.conf"
   # TYPE  DATABASE        USER            ADDRESS                 METHOD
   host    all             all             192.168.1.0/24          scram-sha-256
   ```

1.  設定後、PostgreSQLのサービスを再起動します。

    ``` bash
    sudo systemctl restart postgresql-14
    ```

### 3. プリザンター 1.3の導入

#### アプリケーションの準備

[プリザンター 1.3](https://pleasanter.org/dlcenter)をダウンロードします。

ルートディレクトリ（"/"）に "/web"フォルダーを作成し、そこに"pleasanter"フォルダーを配置するものとして記述します。

-   /web/pleasanter/Implem.Pleasanter
-   /web/pleasanter/Implem.CodeDefiner
-   /web/pleasanter/Tools

#### データベースの構成

1.  /web/pleasanter/Implem.Pleasanter/App_Data/Parameters/Rds.jsonを以下のように設定します。

    ``` json title="Rds.json" linenums="1"
    {
        "Dbms": "PostgreSQL",
        "Provider": "Local",
        "TimeZoneInfo": "Asia/Tokyo",
        "SaConnectionString":"Server=localhost;Port=5432;Database=postgres;UID=postgres;PWD={設定したパスワード}",
        "OwnerConnectionString":"Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD",
        "UserConnectionString":"Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD",
        "SqlCommandTimeOut": 600,
        "MinimumTime": 3,
        "DeadlockRetryCount": 4,
        "DeadlockRetryInterval": 1000
    }
    ```

1.  CodeDefinerを実行

    ``` bash
    cd /web/pleasanter/Implem.CodeDefiner
    dotnet Implem.CodeDefiner.dll _rds
    ```

1.  Pleasanterの起動

    ```bash
    cd /web/pleasanter/Implem.Pleasanter
    dotnet Implem.Pleasanter.dll
    ```

1.  別のターミナルで`http://localhost:5000/`にアクセスし、正常なレスポンスが返ってくることを確認します。

    ```bash
    curl -v http://localhost:5000/
    ```

    ``` text title="レスポンスの例"
    * About to connect() to localhost port 5000 (#0)
    *   Trying ::1...
    * Connected to localhost (::1) port 5000 (#0)
    > GET / HTTP/1.1
    > User-Agent: curl/7.29.0
    > Host: localhost:5000
    > Accept: */*
    >
    < HTTP/1.1 302 Found
    < Date: Mon, 25 May 2020 15:13:08 GMT
    < Server: Kestrel
    < Content-Length: 0
    < Location: http://localhost:5000/users/login?ReturnUrl=%2F
    ```

    確認できたら ++ctrl+c++ で終了します。

#### Pleasanterサービス用スクリプトの作成

`/etc/systemd/system/pleasanter.service`を以下の内容で作成します。

``` ini title="/etc/systemd/system/pleasanter.service" linenums="1" hl_lines="8"
[Unit]
Description = Pleasanter
Documentation =
Wants=network.target
After=network.target

[Service]
ExecStart = /usr/bin/dotnet Implem.Pleasanter.dll # (1)
WorkingDirectory = /web/pleasanter/Implem.Pleasanter
Restart = always
RestartSec = 10
KillSignal=SIGINT
SyslogIdentifier=dotnet-pleasanter
User = root
Group = root
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy = multi-user.target
```

1.  この例はRed Hat Enterprise Linux 8の場合の例です。その他のバージョンでご利用の場合、dotnetコマンドのPATHを確認してから環境に応じて変更してください。以下のコマンドを実行してdotnetの実行パスを確認できます。

    ``` bash
    whereis -b dotnet
    ```

    例えば上記のコマンドを実行した結果が/usr/local/bin/dotnetである場合は、脚注の行は以下のように設定する必要があります。

    ``` text
    ExecStart = /usr/local/bin/dotnet Implem.Pleasanter.dll
    ```

#### サービスとして登録・サービスの起動

``` bash
sudo systemctl daemon-reload
sudo systemctl enable pleasanter
sudo systemctl start pleasanter
```

#### リバースプロキシ（Apache）の設定

通常のwebサーバと同じPort80でアクセスできるようにリバースプロキシの設定を行います。

##### Apacheのインストール

次のコマンドでApacheをインストールします。

``` bash
dnf install -y httpd
systemctl enable httpd
```

##### リバースプロキシの設定

/etc/httpd/conf/httpd.confの最終行に以下の内容を追記します。

``` conf title="/etc/httpd/conf/httpd.conf"
ProxyRequests Off
ProxyPass / http://localhost:5000/
ProxyPassReverse / http://localhost:5000/
```

ファイルを追記後、Apacheを再起動します。

``` bash
systemctl restart httpd
```

##### 80番ポートへのアクセス許可

クライアントからWebサービスへアクセスさせるため、http（80番ポート）へのアクセス許可の設定を行ってください。
設定は各環境により異なりますので適宜調べてください。

### 4. その他設定

#### 初期アカウント

ログインID: Administratorが初期ユーザとして作成されます。
初期ユーザのパスワードは、既定ではpleasanterです。初回ログイン時にパスワード変更ダイアログが表示されますので、任意のパスワードを設定してください。

このパスワードは、/web/pleasanter/Implem.Pleasanter/App_Data/Parameters/Service.jsonのDefaultPasswordで指定可能です。

## プリザンター バージョン 1.3.7.0以降でリマインダー機能を有効化する手順

[BackgroundService.json](../../setup/parameters/background-service-json.md)および[Service.json](../../setup/parameters/service-json.md)のパラメータ設定値を変更してください。なお、パラメータ変更時はマニュアルパラメータ変更時の確認事項を確認してください。

### BackgroundService.json

マニュアル[パラメータ設定：BackgroundService.json](../../setup/parameters/background-service-json.md)を参照し、BackgroundService.jsonファイル内の設定を下記の設定値に変更してください。

| 項目     | 設定例 | 説明                     |
| :------- | :----- | :----------------------- |
| Reminder | true   | リマインダー機能の有効化 |

### Service.json

マニュアル[パラメータ設定：Service.json](../../setup/parameters/service-json.md)を参照し、Service.jsonファイル内の設定を下記の設定値に変更してください。

| 項目        | 設定例                            | 説明                                                                                  |
| :---------- | :-------------------------------- | :------------------------------------------------------------------------------------ |
| AbsoluteUri | "http://pleasanter.example.local" | 通知やリマインダーに記載されるURLの先頭部分を記入してください。（nullは使えません。） |

#### データベースの移行

SQL ServerからPostgreSQLに移行する場合の手順は以下のマニュアルを参照してください。

[プリザンターのDBをSQL ServerからPostgreSQLへ移行する手順](../../setup/version-up-migration/migration/migrate-sql-server-to-postgresql.md)
