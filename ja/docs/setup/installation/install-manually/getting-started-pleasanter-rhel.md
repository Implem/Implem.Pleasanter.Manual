---
title: プリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする
category: プリザンターのインストール
order: '4000'
status: ''
parts: ''
urlstring: getting-started-pleasanter-rhel
translationKey: getting-started-pleasanter-rhel
shortname: プリザンターのインストール,Linuxにインストール
created: 2021-08-27
updated: 2026-01-13
---

## 概要

本マニュアルは以下に示す環境にプリザンターの動作環境を構築するための手順を示したものです。

|対象|内容|
|---|---|
|OS|Red Hat Enterprise Linux 9.7/10.1|
|DB|PostgreSQL 18 / MySQL 8.4|
|Webサーバ|nginx 1.20.1|
|Platform|.NET 10.0.100|
|Pleasanter|PostgreSQL使用時：プリザンター 1.4.0.0以降<br />MySQL使用時：プリザンター 1.4.9.0以降|

## 注意事項

1. ver1.4.6以降でのインストール時に、CodeDefinerに引数を指定しないで実行した場合、言語：英語、タイムゾーン：UTCでセットアップされますので、必要に応じて言語とタイムゾーンをご指定ください。
1. ver1.4.5以前をインストールする場合は初回インストール時のCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
[ver1.4.6以降で初回インストール時のCodeDefinerの手順について](https://pleasanter.org/ja/manual/codedefiner-changed-steps)
1. MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。
1. MySQLにおいてWebサーバとDBサーバを分離した構成にする場合は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../additional/db-server/mysql-connecting-host-description.md)  」または「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)」を参照ください。

## 前提条件

1. OSのセットアップ方法については記載しません。あらかじめOSはセットアップされていることとします。
1. 動作環境やスペックについての詳細はこちらをご確認ください。   
[プリザンターの動作環境や推奨スペックが知りたい](../../../FAQ/system-requirements-and-setup/faq-recommended-specifications.md)  
1. プリザンターを起動するユーザをあらかじめ決めておいてください。手順の中で記載している **<プリザンターを起動するユーザ>** はこのユーザを指します。
1. 本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

## 手順

構築手順は以下の通りです。
1. .NETのセットアップ
1. データベースのセットアップ：  
PostgreSQL、MySQLのいずれかについて以下のセットアップを行う。  
※下記は、設定の実施順序と一致しない場合があります。
   1. DBのインストール
   1. DB管理者権限ユーザの設定
   1. DBのログ出力設定
   1. DBのサービス化および自動起動の有効化
   1. 外部からDBへのアクセスを許可する場合の設定
1. プリザンターのセットアップ
   1. アプリケーションの準備
   1. データベースの構成
   1. CodeDefinerの実行
   1. プリザンターの起動確認
   1. Pleasanterサービス用スクリプトの作成
   1. サービスとして登録・サービスの起動
1. リバースプロキシ(nginx)のセットアップ
   1. SELinuxの設定変更
   1. nginxのインストール
   1. リバースプロキシの設定
   1. Http(80) へのアクセス許可
1. プリザンターの動作確認

## 1. .NETのセットアップ

以下コマンドを実行して、.NET をインストールします。

```
sudo wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
sudo chmod +x ./dotnet-install.sh
sudo ./dotnet-install.sh -c 10.0 -i /usr/local/bin
dotnet --version
```

詳細につきましては下記公式ページの **スクリプトでのインストール** をご参照ください。  
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-scripted-manual#scripted-install  

また、dotnetコマンドを実行した際に特定のファイルに関するエラーが発生するケースがございます。その際は下記ページをご参照ください。
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-package-mixup?pivots=os-linux-redhat

## 2. データベースのセットアップ

以下の「PostgreSQLのセットアップ」または「MySQLのセットアップ」のいずれかを参照し、データベースをセットアップします。

<details markdown="1">
<summary style="font-weight:bold">1. PostgreSQLのセットアップ</summary>
PostgreSQLのセットアップ手順は以下の通りです。

#### 1. PostgreSQLのインストール

以下コマンドを実行してPostgreSQLをインストールします。

```
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo dnf install -y postgresql18-server postgresql18-contrib
```

#### 2.  PostgreSQLデータベースの初期化

以下コマンドを実行して、データベースの初期化を行います。※ -A: 認証方式の指定、-W: パスワード入力プロンプトを表示するオプション  
実行後、パスワード入力プロンプトが表示しますので、パスワードを入力します。  ここで設定したパスワードは手順3.2.で使用しますので忘れないように控えてください。

```
sudo su - postgres -c '/usr/pgsql-18/bin/initdb -E UTF8 -A scram-sha-256 -W'
```

#### 3. PostgreSQLのログ出力設定

/var/lib/pgsql/18/data/postgresql.conf を開き、以下の設定を編集します。

```
log_destination = 'stderr'
logging_collector = on
log_line_prefix = '[%t]%u %d %p[%l]'
```

#### 4. PostgreSQLのサービス再起動、サービス化 

以下コマンドを実行してPostgreSQLのサービス再起動およびサービス自動起動を有効化します。

```
sudo systemctl restart postgresql-18
sudo systemctl enable postgresql-18
```

#### 5. 外部からDBへのアクセスを許可する場合の設定

1. /var/lib/pgsql/18/data/postgresql.conf の以下の2行のコメントを解除して下記のように設定します。  

    ```
    # - Connection Settings -
    listen_addresses = '*'  # what IP address(es) to listen on;
    port = 5432             # (change requires restart)
    ```

2. /var/lib/pgsql/18/data/pg_hba.conf に以下の行を追加します。Address欄にはアクセスを許可するIPアドレスの範囲を指定します。  

    ```
    # TYPE  DATABASE        USER            ADDRESS                 METHOD
    host    all             all             192.168.1.0/24          scram-sha-256
    ```

3. 設定後、以下コマンドを実行して、PostgreSQLのサービスを再起動します。

    ```
    sudo systemctl restart postgresql-18
    ```

</details>

<details markdown="1">
<summary style="font-weight:bold">2. MySQLのセットアップ</summary>
MySQLのセットアップ手順は以下の通りです。

#### 1. MySQLのインストール

1. 以下コマンドを実行して、MySQLのパッケージとサーバをインストールします。

    ```
    sudo dnf install -y https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm
    sudo dnf install mysql-community-server
    ```

    コマンドで指定したURLにつきましては下記公式リポジトリの指定と同一のURLです。  
    https://dev.mysql.com/downloads/repo/yum/ 

2. コマンドを実行し、サービスの状態を表示します。

    ```
    systemctl status mysqld.service
    ```

3. 以下のように「Active: inactive (dead)」の文字が表示され、サービスが停止されていることを確認します。

    ```
    ○ mysqld.service - MySQL Server
         Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; preset: disabled)
         Active: inactive (dead)
           Docs: man:mysqld(8)
                 http://dev.mysql.com/doc/refman/en/using-systemd.html
    ```

#### 2. MySQLのサービス自動起動を有効化

1. 以下コマンドを実行して、MySQLのサービスを起動します。

    ```
    sudo systemctl start mysqld
    ```

2. 以下コマンドを実行してMySQLのサービス自動起動を有効化します。

    ```
    sudo systemctl enable mysqld
    ```

#### 3. MySQLユーザの設定

1. /etc/my.cnf の [mysqld] 配下に以下の設定を追記します。

    ```
    [mysqld]
    skip-grant-tables
    ```

    設定ファイルのパスは、OSまたはMySQLのバージョンにより異なる場合があります。

2. 以下コマンドを実行して、MySQLのサービスを再起動します。

    ```
    sudo systemctl restart mysqld
    ```

3. 以下コマンドを実行して、MySQLにrootアカウント（パスワード指定なし）でログインします。

    ```
    mysql -u root
    ```

4. 以下SQLを実行して、MySQLのrootアカウントのパスワードを設定します。

    ```
    flush privileges;
    alter user 'root'@'localhost' identified by '<MySQLのrootアカウントの新しいパスワード※>';
    ```

    ※本手順でインストールするMySQLのデフォルトの設定では、8文字以上、大文字、小文字、数値、特殊文字を使用したパスワードを求められます。

5. 以下コマンドを実行して、MySQLからrootアカウントをログアウトします。

    ```
    quit;
    ```

6. /etc/my.cnf の [mysqld] 配下に追記した記述を削除します。その際 [mysqld] は削除しないでください。  

    ```
    skip-grant-tables
    ```

7. 以下コマンドを実行して、MySQLのサービスを再起動します。

    ```
    sudo systemctl restart mysqld
    ```

8. 以下コマンドを実行して、MySQLにrootアカウントでログインできることを確認してください。

    ```
    mysql -u root -p
    ```

9. 以下コマンドを実行して、MySQLからrootアカウントをログアウトします。

    ```
    quit;
    ```

#### 4. MySQLのログ出力設定

**MySQLではデフォルトでエラーログの出力が有効です。デフォルトの出力先を変更しない場合、以下の手順は実施不要です。**

1. /etc/my.cnf の [mysqld] 配下にあるlog-errorに記載されているログファイルのパスを確認します。  
    設定ファイルのパスは、OSまたはMySQLのバージョンにより異なる場合があります。

    ```
    [mysqld]
    log-error=/var/log/mysqld.log
    ```

2. エラーログの出力先を変更する場合は、my.cnfファイルの編集後、以下コマンドを実行してMySQLのサービスを再起動します。

    ```
    sudo systemctl restart mysqld
    ```

#### 5. 外部からDBへのアクセスを許可する場合の設定

以下マニュアルの手順を実施し、MySQLのユーザを追加します。  

-   [WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../additional/db-server/mysql-connecting-host-description.md)  
-   [WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)

WebサーバとDBサーバを分離しない場合は、実施不要です。

</details>

## 3. プリザンターのセットアップ

### 1. アプリケーションの準備

1. 以下コマンドを実行して、ルートディレクトリ（"/"）に "web" ディレクトリを作成します。

    ```
    sudo mkdir /web
    ```

2. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。  
   プリザンター1.4.23.3以前をインストールする場合は、[GitHub](https://github.com/Implem/Implem.Pleasanter/releases)から任意のバージョンのzipファイル（例：Pleasanter_1.4.23.3.zip）をダウンロードします。

3. ダウンロードしたzipファイルを解凍し、解凍された"pleasanter"フォルダごと[WinSCP](https://winscp.net/jp/)などのファイル転送アプリケーションでサーバの"/web"に配置します。

4. 以下コマンドを実行して、pleasanterディレクトリ配下の所有者をあらかじめ決めたプリザンターを起動するユーザに変更します。

    ```
    sudo chown -R <プリザンターを起動するユーザ> /web/pleasanter
    ```

### 2. データベースの構成 

/web/pleasanter/Implem.Pleasanter/App_Data/Parameters/Rds.jsonにデータベースへの接続情報を設定します。設定例を以下に示します。必要に応じてRds.jsonのマニュアルも参照してください。
[Rds.json](../../parameters/rds-json.md)

<details markdown="1">
<summary style="font-weight:bold">PostgreSQL使用時のRds.jsonの設定例</summary>

|No|プロパティ名|値|
|:----|:----|:----|
|1|Dbms|"PostgreSQL"|
|2|SaConnectionString|"Server=localhost;Port=5432;Database=postgres;UID=postgres;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は「PostgreSQLデータベースの初期化」で設定したパスワードを入力してください。|
|3|OwnerConnectionString|"Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|
|4|UserConnectionString|"Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_User;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|

```json
{
    "Dbms": "PostgreSQL",
    "Provider": "Local",
    "SaConnectionString": "Server=localhost;Port=5432;Database=postgres;UID=postgres;PWD=<「PostgreSQLデータベースの初期化」で設定したパスワード>",
    "OwnerConnectionString": "Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD",
    "UserConnectionString": "Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD",
    "SqlCommandTimeOut": 0,
    "MinimumTime": 3,
    "DeadlockRetryCount": 4,
    "DeadlockRetryInterval": 1000,
    "DisableIndexChangeDetection": true,
    "SysLogsSchemaVersion": 1,
    "MySqlConnectingHost": "%"
}
```

</details>

<details markdown="1">
<summary style="font-weight:bold">MySQL使用時のRds.jsonの設定例</summary>

|No|プロパティ名|値|
|:----|:----|:----|
|1|Dbms|"MySQL"|
|2|SaConnectionString|"Server=localhost;Port=3306;Database=mysql;UID=root;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は「MySQLユーザの設定」で設定したパスワードを入力してください。|
|3|OwnerConnectionString|"Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|
|4|UserConnectionString|"Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|
|5|MySqlConnectingHost|特段の要件がない場合は"%"、MySQLに対するアクセス制限を行う場合は[Rds.json](../../parameters/rds-json.md)を参照し適宜設定。|

※本手順でインストールするMySQLのデフォルトの設定では、8文字以上、大文字、小文字、数値、特殊文字を使用したパスワードを求められます。

```json
{
    "Dbms": "MySQL",
    "Provider": "Local",
    "SaConnectionString": "Server=localhost;Port=3306;Database=mysql;UID=root;PWD=<「MySQLユーザの設定」で設定したパスワード>",
    "OwnerConnectionString": "Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=Set_0_Admins_0_PWD",
    "UserConnectionString": "Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=Set_0_Users_0_PWD",
    "SqlCommandTimeOut": 0,
    "MinimumTime": 3,
    "DeadlockRetryCount": 4,
    "DeadlockRetryInterval": 1000,
    "DisableIndexChangeDetection": true,
    "SysLogsSchemaVersion": 1,
    "MySqlConnectingHost": "%"
}
```

</details>

### 3. CodeDefinerの実行

以下コマンドを実行して、あらかじめ決めたプリザンターを起動するユーザでCodeDefinerを実行します。  
本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時に指定するディレクトリをインストール先に合わせて変更してください。  
※下記コマンドは初回インストール時にのみ実行します。

```
cd /web/pleasanter/Implem.CodeDefiner
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds /l "<言語>" /z "<タイムゾーン>"
```

|引数|設定例|説明|
|:--|:--|:--|
|/l|ja|Service.jsonのDefaultLanguageの値を書き換えます(※1)|
|/z|Asia/Tokyo|Service.jsonのTimeZoneDefaultの値を書き換えます(※1)|  

(※1) 言語、タイムゾーンは以下マニュアルページを参照ください。
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](https://pleasanter.org/manual/faq-supported-language)

日本語環境でご利用する場合は以下コマンドとなります。

```
cd /web/pleasanter/Implem.CodeDefiner
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds /l "ja" /z "Asia/Tokyo"
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力してください。

### 4. プリザンターの起動確認

1. 以下コマンドを実行して、あらかじめ決めたユーザでプリザンターを起動します。

    ```
    cd /web/pleasanter/Implem.Pleasanter
    sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.Pleasanter.dll
    ```

2. 起動中に別のターミナルで以下コマンドを実行し、プリザンターが起動していることを確認します。「Ctrl+C」で終了します。
* 実行コマンド

```
curl -v http://localhost:5000/
```

* 実行結果

```
*   Trying ::1:5000...
* Connected to localhost (::1) port 5000 (#0)
> GET / HTTP/1.1
> Host: localhost:5000
> User-Agent: curl/7.76.1
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 302 Found
< Content-Length: 0
< Date: Tue, 25 Jul 2023 02:42:19 GMT
< Server: Kestrel
< Location: http://localhost:5000/users/login?ReturnUrl=%2F
< X-Frame-Options: SAMEORIGIN
< X-XSS-Protection: 1; mode=block
< X-Content-Type-Options: nosniff
<
* Connection #0 to host localhost left intact
```

### 5. Pleasanterサービス用スクリプトの作成

/etc/systemd/system/pleasanter.service を以下の内容で作成します。下記の **User** にはあらかじめ決めたプリザンターを起動するユーザを指定してください。
本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、ExecStartに指定するディレクトリをインストール先に合わせて変更してください。

```
[Unit]
Description = Pleasanter
Documentation =
Wants=network.target
After=network.target

[Service]
ExecStart = /usr/local/bin/dotnet Implem.Pleasanter.dll
WorkingDirectory = /web/pleasanter/Implem.Pleasanter
Restart = always
RestartSec = 10
KillSignal=SIGINT
SyslogIdentifier=dotnet-pleasanter
User = <プリザンターを起動するユーザ>
Group = root
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy = multi-user.target
```

### 6. サービスとして登録・サービスの起動

以下コマンドを実行してプリザンターのサービス起動およびサービス自動起動を有効化します。

```
sudo systemctl daemon-reload
sudo systemctl enable pleasanter
sudo systemctl start pleasanter
```

## 4. リバースプロキシ(nginx)のセットアップ

通常のwebサーバと同じ Port80 でアクセスできるようにリバースプロキシの設定を行います。  

### 1. SELinuxの設定変更

以下コマンドを実行します。

```
getenforce
```

#### a. 「コマンド 'getenforce' が見つかりません。」、「Permissive」、「Disabled」のいずれかが表示された場合

「2. nginxのインストール」に進みます。

#### b. 「Enforcing」が表示された場合

以下コマンドを実行します。

```
sudo setsebool -P httpd_can_network_connect on
```

※SELinuxの上記ブール値を変更することで、該当のサーバにおいてスクリプトやモジュールによるネットワーク接続がすべて許可されます。

### 2. nginxのインストール

以下コマンドを実行して、nginxをインストールします。

```
sudo dnf install -y nginx
sudo systemctl enable nginx
```

### 3. リバースプロキシの設定

1. /etc/nginx/conf.d/pleasanter.conf を以下の内容で作成します。server_name 行には実際にアクセスするサーバのホスト名またはIPアドレスを指定します。   

    ```
    server {
        listen  80;
        server_name   192.168.1.100;
        client_max_body_size 100M;
        location / {
           proxy_pass         http://localhost:5000;
           proxy_http_version 1.1;
           proxy_set_header   Upgrade $http_upgrade;
           proxy_set_header   Connection keep-alive;
           proxy_set_header   Host $host;
           proxy_cache_bypass $http_upgrade;
           proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header   X-Forwarded-Proto $scheme;
        }
    }
    ```
2. ファイルを作成後、以下コマンドを実行して、サービスを再起動します。  

    ```
    sudo systemctl restart nginx
    ```

### 4. Http(80) へのアクセス許可

以下コマンドを実行して、クライアントからWebサービスへアクセスさせるために Http（port:80）へのアクセス許可設定を行います。  

```
sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --reload
```

## 5. プリザンターの動作確認

1. プリザンターを起動後、プリザンターのログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
       ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/5477647dc121413190827affdc7fa1ff.png)

2. ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
       ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/0ff466031f9f41719bb5eb9f8190c218.png)

### 正しくリダイレクトされない場合

nginxの設定が正しいか確認してください。記述内容の / の有無など細かな違いで動作が変わる場合があります。  

### プリザンターの画面が開かない場合

上記までの手順において特にエラーも出ずに完了したにも関わらず、ブラウザでアクセスすると「Welcome to nginx!」といったページ(エラー表示ではない)が表示される場合、ブラウザのセキュリティ設定により、プリザンターのログイン画面に遷移できていない可能性があります。  
お使いのブラウザのセキュリティ設定を確認してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.9.0 以降|MySQLに対応|
|1.4.10.0 以降|MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題を解消<br>※併せて注意事項に「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)」へのリンクを追加|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能を追加|
|1.5.0.0 以降|.NET 10、PostgreSQL 18に対応|

## 関連情報

[PostgreSQLが14以前のバージョンで、1.3.43.0以前のプリザンターをLinuxの環境へ導入したい](../../../FAQ/system-requirements-and-setup/faq-postgresql-14-install-pleasanter-for-linux.md)