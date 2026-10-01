---
title: プリザンターをAmazon EC2のRed Hat Enterprise Linux 10にインストールする
category: プリザンターのインストール
order: '1000'
status: ''
parts: ''
urlstring: getting-started-pleasanter-rhel10-aws
translationKey: getting-started-pleasanter-rhel10-aws
shortname: プリザンターのインストール,Linuxにインストール
created: 2025-05-27
updated: 2026-01-13
---

## 概要

本マニュアルは以下に示す環境にプリザンターの動作環境を構築するための手順を示したものです。

|対象|内容|
|---|---|
|サービス|Amazon EC2 および Amazon RDS|
|OS|Red Hat Enterprise Linux 10 (HVM), SSD Volume Type|
|DB|MySQL 8.4.5|
|Webサーバ|nginx 1.26.3|
|Platform|.NET 8.0.410|
|Pleasanter|プリザンター 1.4.18.0以降|

## 注意事項

1.  CodeDefinerに引数を指定しないで実行した場合、言語：英語、タイムゾーン：UTCでセットアップされますので、必要に応じて言語とタイムゾーンをご指定ください。

## 前提条件

1.  EC2インスタンスは以下の条件でセットアップされているものとします。
    1.  セキュリティグループのルールでSSHトラフィック、HTTPトラフィック、HTTPSトラフィックを許可していること。
    1.  EC2インスタンスのキーペアの秘密鍵をダウンロードしていること。
    1.  EC2インスタンスの既定ユーザec2-userが存在すること。
1.  RDSインスタンスは以下の条件でセットアップされているものとします。
    1.  EC2インスタンスと接続設定を行っていること。
    1.  マスターユーザー名とマスターパスワードを設定し、パスワード認証を行えること。
1.  本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

## 手順

構築手順は以下の通りです。

1.  EC2インスタンスへのSSH接続
1.  .NETのセットアップ
1.  プリザンターのセットアップ
    1.  アプリケーションの準備
    1.  データベースの構成
    1.  CodeDefinerの実行
    1.  プリザンターの起動確認
    1.  Pleasanterサービス用スクリプトの作成
    1.  サービスとして登録・サービスの起動
1.  リバースプロキシ(nginx)のセットアップ
    1.  SELinuxの設定変更
    1.  nginxのインストール
    1.  リバースプロキシの設定
1.  プリザンターの動作確認

## 1. EC2インスタンスへのSSH接続

本手順ではTeraTerm等のクライアントおよびWinSCP等のファイル転送ツールを用いて、クライアントのPCからEC2インスタンスにSSH接続を行います。

1.  EC2のインスタンスの管理画面を開きパブリックIPアドレスを確認します。

1.  TeraTerm等のクライアントおよびWinSCP等のファイル転送ツールを起動し、以下の接続設定でEC2インスタンスに接続します。
    1.  接続先：EC2インスタンスのパブリックIPアドレス
    1.  ユーザ名：ec2-user
    1.  パスワード：空欄
    1.  その他：秘密鍵を使う

## 2. .NETのセットアップ

以下コマンドを実行して、.NET をインストールします。

```
sudo wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
sudo chmod +x ./dotnet-install.sh
sudo ./dotnet-install.sh -c 8.0 -i /usr/local/bin
dotnet --version
```

詳細につきましては以下公式ページの **スクリプトでのインストール** をご参照ください。  
<https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-scripted-manual#scripted-install>  

!!! tip

    dotnet --version コマンドを実行した際にICU（Unicodeの取り扱いに関する様々な機能を提供するオープンソースのライブラリ）のインストールを要求するエラーが表示される場合があります。

    ``` text title="エラーメッセージ例"
    Process terminated. Couldn't find a valid ICU package installed on the system.
    Please install libicu (or icu-libs) using your package manager and try again.
    Alternatively you can set the configuration flag
    System.Globalization.Invariant to true if you want to run with no
    globalization support.
    Please see https://aka.ms/dotnet-missing-libicu for more information.
    ```

    その場合は、以下コマンドを実行してICUをインストールします。

    ``` bash title="実行コマンド"
    sudo yum install libicu-devel wget -y
    ```

## 3. プリザンターのセットアップ

### 1. アプリケーションの準備

1.  以下コマンドを実行して、ルートディレクトリ（"/"）に "web" ディレクトリを作成します。

    ```
    sudo mkdir /web
    ```

1.  [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1.  ダウンロードしたzipファイルを解凍し、解凍された"pleasanter"フォルダごと[WinSCP](https://winscp.net/jp/)などのファイル転送アプリケーションでサーバの"/web"に配置します。

1.  以下コマンドを実行して、pleasanterディレクトリ配下の所有者をec2-user（プリザンターを起動するユーザ）に変更します。

    ```
    sudo chown -R ec2-user /web/pleasanter
    ```

### 2. データベースの構成

1.  データベースへの接続情報を設定します。  
    /web/pleasanter/Implem.Pleasanter/App_Data/Parameters/Rds.jsonを開き、パラメータを下記の通りに設定し、保存します。

    |パラメータ名|値|説明|
    |:--|:--|:--|
    |Dbms|MySQL|リレーショナル・データベースに Amazon RDS（MySQL）を使用。|
    |Provider|Local|リレーショナル・データベースに Amazon RDS（MySQL）を使用。|
    |SaConnectionString|**\*\*\*\***|手順3.2.2の通り設定。|
    |OwnerConnectionString|**\*\*\*\***|手順3.2.3の通り設定。|
    |UserConnectionString|**\*\*\*\***|手順3.2.4の通り設定。|
    |SqlCommandTimeOut|0|SQL コマンドタイムアウト時間を無期限にする。|
    |MinimumTime|3|データベースが識別可能な最小時間単位をミリ秒で指定。本パラメータは変更不可。|
    |DeadlockRetryCount|4|デッドロック発生時の最大再試行回数。|
    |DeadlockRetryInterval|1000|デッドロック発生時に再試行を行うまでの間隔。|
    |DisableIndexChangeDetection|true|バージョンアップ時にデータベースのインデックスの差異を検出しない。|
    |SysLogsSchemaVersion|2|「システムログの拡張機能」を利用する。|
    |MySqlConnectingHost|%|EC2インスタンスから接続を許可するためワイルドカードを指定。|

#### "MySqlConnectingHost"について

Ver.1.4.18.0以降で追加された[Rds.json](../../parameters/rds-json.md)の"MySqlConnectingHost"について詳細は下記を参照ください。

??? note "（こちらをクリックすると詳細が開閉します）"

    -   以下の要件が特段ない場合（既定値）："%"
    -   指定の外部のホスト以外からMySQLへのアクセスを禁じる場合："接続を許可するホスト名／IPアドレス（AWSの場合はプライベートIPアドレスを設定します）"。半角カンマ区切りで複数指定可（例："hostname01,hostname02"）

1.  接続文字列SaConnectionStringは下記の通りに設定します。

    |内容|設定例|詳細|
    |:--|:--|:--|
    |Server|{DB識別子等の文字列}.rds.amazonaws.com|RDSインスタンスのエンドポイント。|
    |Port|3306|RDSインスタンスのポート番号。|
    |Database|mysql|mysql固定。|
    |UID|{UserName}|Microsoft Azure Database for MySQLのマスターユーザー名。|
    |PWD|{Password}|Microsoft Azure Database for MySQLのマスターパスワード。|

    ```text title="接続文字列SaConnectionStringの設定例"
    Server={DB識別子等の文字列}.rds.amazonaws.com;Port=3306;Database=mysql;UID={UserName};PWD={Password}
    ```

1.  接続文字列OwnerConnectionStringは下記の通りに設定します。

    |内容|設定例|詳細|
    |:--|:--|:--|
    |Server|{DB識別子等の文字列}.rds.amazonaws.com|RDSインスタンスのエンドポイント。|
    |Port|3306|RDSインスタンスのポート番号。|
    |Database|#ServiceName#|Service.jsonのName。#ServiceName#はService.jsonのNameを参照するプレースホルダー。|
    |UID|#ServiceName#_Owner|CodeDefinerで作成する任意のユーザ名。#ServiceName#はService.jsonのNameを参照するプレースホルダー。|
    |PWD|SetAdminsPWD|CodeDefinerで設定する任意のユーザのパスワード。|

    ```text title="接続文字列OwnerConnectionStringの設定例"
    Server={DB識別子等の文字列}.rds.amazonaws.com;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD
    ```

1.  接続文字列UserConnectionStringは下記の通りに設定します。

    |内容|設定例|詳細|
    |:--|:--|:--|
    |Server|{DB識別子等の文字列}.rds.amazonaws.com|RDSインスタンスのエンドポイント。|
    |Port|3306|RDSインスタンスのポート番号。|
    |Database|#ServiceName#|Service.jsonのName。#ServiceName#はService.jsonのNameを参照するプレースホルダー。|
    |UID|#ServiceName#_User|CodeDefinerで作成する任意のユーザ名。#ServiceName#はService.jsonのNameを参照するプレースホルダー。|
    |PWD|SetUsersPWD|CodeDefinerで設定する任意のユーザのパスワード。|

    ```text title="接続文字列UserConnectionStringの設定例"
    Server={DB識別子等の文字列}.rds.amazonaws.com;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD
    ```

### 3. CodeDefinerの実行

以下コマンドを実行して、ec2-userでCodeDefinerを実行します。
本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時に指定するディレクトリをインストール先に合わせて変更してください。

以下のコマンドは初回インストール時にのみ実行します。

``` bash
cd /web/pleasanter/Implem.CodeDefiner
sudo -u ec2-user /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds /l "<言語>" /z "<タイムゾーン>"
```

|引数|設定例|説明|
|:--|:--|:--|
|/l|ja|Service.jsonのDefaultLanguageの値を書き換えます [^1]|
|/z|Asia/Tokyo|Service.jsonのTimeZoneDefaultの値を書き換えます [^1]|

[^1]:
    言語、タイムゾーンは以下マニュアルページを参照ください。
    [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

日本語環境でご利用する場合は以下コマンドとなります。

``` bash
cd /web/pleasanter/Implem.CodeDefiner
sudo -u ec2-user /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds /l "ja" /z "Asia/Tokyo"
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら ++y++ を入力してください。

### 4. プリザンターの起動確認

1.  以下コマンドを実行して、ec2-userでプリザンターを起動します。

    ``` bash
    cd /web/pleasanter/Implem.Pleasanter
    sudo -u ec2-user /usr/local/bin/dotnet Implem.Pleasanter.dll
    ```

1.  起動中に別のターミナルで以下コマンドを実行し、プリザンターが起動していることを確認します。「Ctrl+C」で終了します。

    ``` bash title="実行コマンド"
    curl -v http://localhost:5000/
    ```

    ``` text title="実行結果"
    * Host localhost:5000 was resolved.
    * IPv6: ::1
    * IPv4: 127.0.0.1
    *   Trying [::1]:5000...
    * Connected to localhost (::1) port 5000
    > GET / HTTP/1.1
    > Host: localhost:5000
    > User-Agent: curl/8.9.1
    > Accept: */*
    >
    * Request completely sent off
    < HTTP/1.1 302 Found
    < Content-Length: 0
    < Date: Tue, 24 Jun 2025 02:59:24 GMT
    < Server: Kestrel
    < Location: http://localhost:5000/users/login?ReturnUrl=%2F
    < X-Frame-Options: SAMEORIGIN
    < X-XSS-Protection: 1; mode=block
    < X-Content-Type-Options: nosniff
    <
    * Connection #0 to host localhost left intact
    ```

### 5. Pleasanterサービス用スクリプトの作成

/etc/systemd/system/pleasanter.service を以下の内容で作成します。

``` ini title="pleasanter.service" linenums="1"
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
User = ec2-user
Group = root
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy = multi-user.target
```

### 6. サービスとして登録・サービスの起動

以下コマンドを実行してプリザンターのサービス起動およびサービス自動起動を有効化します。

``` bash
sudo systemctl daemon-reload
sudo systemctl enable pleasanter
sudo systemctl start pleasanter
```

## 4. リバースプロキシ(nginx)のセットアップ

通常のwebサーバと同じ Port80 でアクセスできるようにリバースプロキシの設定を行います。  

### 1. SELinuxの設定変更

以下コマンドを実行します。

``` bash
getenforce
```

#### a. 「コマンド 'getenforce' が見つかりません。」、「Permissive」、「Disabled」のいずれかが表示された場合

「2. nginxのインストール」に進みます。

#### b. 「Enforcing」が表示された場合

以下コマンドを実行します。

``` bash
sudo setsebool -P httpd_can_network_connect on
```

SELinuxの上記ブール値を変更することで、該当のサーバにおいてスクリプトやモジュールによるネットワーク接続がすべて許可されます。

### 2. nginxのインストール

以下コマンドを実行して、nginxをインストールします。

``` bash
sudo dnf install -y nginx
sudo systemctl enable nginx
```

### 3. リバースプロキシの設定

1.  /etc/nginx/conf.d/pleasanter.conf を以下の内容で作成します。 server_name 行にはEC2インスタンスのパブリックIPアドレスを指定します。

    !!! warning
        パブリックIPアドレスはEC2インスタンスの再起動時に変更されてしまいます。固定IPアドレス取得はElastic IP アドレスの利用をご検討ください。  

    ``` text title="pleasanter.conf" linenums="1"
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

1.  ファイルを作成後、以下コマンドを実行して、サービスを再起動します。  

    ``` bash
    sudo systemctl restart nginx
    ```

## 5. プリザンターの動作確認

1.  プリザンターの起動を確認可能なアドレスは2種類あります。  
    パブリックIPアドレスおよびパブリックDNSは、EC2のインスタンスの管理画面から確認します。
    1.  http://{EC2のパブリックIPアドレス}
    1.  http://{EC2のパブリックDNS}  
        例：http://{文字列}.compute.amazonaws.com

1.  プリザンターを起動後、プリザンターのログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。

    ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/db5708b71ddc4da5b6ddf4394cf8232b.png)

1.  ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  

    ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/fd605a3863f84187aa2110b98a8aab54.png)

### 正しくリダイレクトされない場合

nginxの設定が正しいか確認してください。記述内容の / の有無など細かな違いで動作が変わる場合があります。  

### プリザンターの画面が開かない場合

上記までの手順において特にエラーも出ずに完了したにも関わらず、ブラウザでアクセスすると「Welcome to nginx!」といったページ(エラー表示ではない)が表示される場合、ブラウザのセキュリティ設定により、プリザンターのログイン画面に遷移できていない可能性があります。  
お使いのブラウザのセキュリティ設定を確認してください。

## プリザンターのバージョンアップ

本手順でインストールしたプリザンターのバージョンアップ手順は以下マニュアル参照してください。  
[1.4.8.0以降のバージョンアップ手順(Linux)](../../version-up-migration/version-up-manually/version-up-linux-1.4.8.0.md)

## 関連情報

[1.4.8.0以降のバージョンアップ手順(Linux)](../../version-up-migration/version-up-manually/version-up-linux-1.4.8.0.md)
