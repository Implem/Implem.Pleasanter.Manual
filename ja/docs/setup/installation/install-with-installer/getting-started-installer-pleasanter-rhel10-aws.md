---
title: インストーラでプリザンターをAmazon EC2のRed Hat Enterprise Linux 10にインストールする
category: プリザンターのインストール(インストーラ)
order: '310'
status: ''
parts: ''
urlstring: getting-started-installer-pleasanter-rhel10-aws
translationKey: getting-started-installer-pleasanter-rhel10-aws
shortname: プリザンターのインストール,プリザンターのインストール（インストーラ）,インストーラ,Linuxにインストール
created: 2025-05-27
updated: 2026-07-17
---

## 概要

本手順は[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターの動作環境を構築する手順です。モジュールの配置やパラメータ設定を手動で行う今までの手順でもインストール可能です。手動インストールの手順は以下を参照ください。
[プリザンターをAmazon EC2のRed Hat Enterprise Linux 10にインストールする](../install-manually/getting-started-pleasanter-rhel10-aws.md)

|対象|内容|
|---|---|
|サービス|Amazon EC2 および Amazon RDS|
|OS|Red Hat Enterprise Linux 10 (HVM), SSD Volume Type|
|DB|MySQL 8.4.5|
|Webサーバ|nginx 1.26.3|
|Platform|.NET 8.0.410|
|Pleasanter|プリザンター 1.4.18.0以降|

## 前提条件

1. EC2インスタンスは以下の条件でセットアップされているものとします。
    1. セキュリティグループのルールでSSHトラフィック、HTTPトラフィック、HTTPSトラフィックを許可していること。
    1. EC2インスタンスのキーペアの秘密鍵をダウンロードしていること。
    1. EC2インスタンスの既定ユーザec2-userが存在すること。
1. RDSインスタンスは以下の条件でセットアップされているものとします。
    1. EC2インスタンスと接続設定を行っていること。
    1. マスターユーザー名とマスターパスワードを設定し、パスワード認証を行えること。
1. 本手順では.NETを /usr/local/bin にインストールする場合として説明します。同一環境に複数バージョンの.NETが必要などの理由で.NETを異なるディレクトリにインストールする場合は、CodeDefinerの実行時やPleasanterサービス用スクリプトの作成でExecStartに指定するディレクトリをインストール先に合わせて変更してください。

## 手順

構築手順は以下の通りです。
1. EC2インスタンスへのSSH接続
1. .NETのセットアップ
1. インストーラのインストール
1. プリザンターのセットアップ
   1. インストーラの実行
   1. プリザンターの起動確認
   1. Pleasanterサービス用スクリプトの作成
   1. サービスとして登録・サービスの起動
1. リバースプロキシ(nginx)のセットアップ
   1. SELinuxの設定変更
   1. nginxのインストール
   1. リバースプロキシの設定
1. プリザンターの動作確認

## 1. EC2インスタンスへのSSH接続

本手順ではTeraTerm等のクライアントおよびWinSCP等のファイル転送ツールを用いて、クライアントのPCからEC2インスタンスにSSH接続を行います。

1. EC2のインスタンスの管理画面を開きパブリックIPアドレスを確認します。

2. TeraTerm等のクライアントおよびWinSCP等のファイル転送ツールを起動し、以下の接続設定でEC2インスタンスに接続します。
    1. 接続先：EC2インスタンスのパブリックIPアドレス
    2. ユーザ名：ec2-user
    3. パスワード：空欄
    4. その他：秘密鍵を使う

## 2. .NETのセットアップ

以下コマンドを実行して、.NET をインストールします。

```
sudo wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
sudo chmod +x ./dotnet-install.sh
sudo ./dotnet-install.sh -c 8.0 -i /usr/local/bin
dotnet --version
```

詳細につきましては以下公式ページの **スクリプトでのインストール** をご参照ください。  
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-scripted-manual#scripted-install  

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

## 3.インストーラのインストール

以下コマンドを実行して、インストーラ をインストールします。

```
dotnet tool install -g Implem.PleasanterSetup
echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
source ~/.bashrc
```

### ネットワーク環境に接続されていない場合は下記手順でインストールしてください。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

1. 以下コマンドを実行して.nupkgファイルを配置する任意のフォルダを作成します。
    ※本手順では/dotnet-toolsを作成する場合として説明します。
    ```
    sudo mkdir /dotnet-tools
    ```
1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードします。
    ![Implem.PleasanterSetup の NuGet ギャラリーのページ。「Download package」がある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)
1. 手順2.2でダウンロードした.nupkgファイルを**/dotnet-tools**に配置します。
1. 画像の②のコマンドをコピーします。
1. 以下コマンド実行します。

    ```
    <手順2.4でコピーしたコマンド> --add-source /dotnet-tools
    echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
    echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
    echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
    source ~/.bashrc
    ```

 **例：Implem.PleasanterSetupのVersionが1.0.1の場合**

 ```
 dotnet tool install --global Implem.PleasanterSetup --version 1.0.1 --add-source /dotnet-tools
 echo 'export PATH="$PATH:~/.dotnet/tools"' >> ~/.bashrc
 echo 'export DOTNET_ROOT=/usr/local/bin' >> ~/.bashrc
 echo 'export PATH=$PATH:$DOTNET_ROOT' >> ~/.bashrc
 source ~/.bashrc
 ```

</details>

## 4. プリザンターのセットアップ

### 1. インストーラの実行

インストーラを使用することで、最新バージョン資源を自動でダウンロードし、入力した値を元にService.json、Rds.jsonの値を自動設定します。

#### MySQL使用時の手順は以下の通りです。

1. 以下コマンドを実行して、インストーラを実行します。

    ```text
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、以下手順を実施してください**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「/web/」に配置します。

        1. 以下コマンドを実行します。  
           **/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            /web/Pleasanter_1.5.x.x.zip
            ```

            ```text
            pleasanter-setup -r /web/Pleasanter_1.5.x.x.zip
            ```

2. プリザンターをインストールするディレクトリを入力します。  
    「/web/pleasanter」 にインストールする場合は空白で Enter キーを押下してください。
    ```text
    Install Directory [Default: /web/pleasanter] :

    ```

3.  プリザンターを起動するユーザを入力します。**ec2-user** を入力し Enter キーを押下してください

    ```text
    Please enter the user who will execute Pleasanter.

    ```

4. サービス名を入力します。
    「Implem.Pleasanter」の場合は空白で Enter キーを押下してください。
    ```text
    ServiceName [Default: Implem.Pleasanter] :

    ```

5. 使用する DBMS に対応する番号を入力します。
    ここでは「3」（MySQL）を入力しEnterキーを押下してください。
    ```text
    DBMS [1: SQL Server, 2: PostgreSQL, 3: MySQL] :

    ```

6. 利用するポート番号を入力します。
    DBMSのデフォルトのポート番号の場合は空白で Enter キーを押下してください。
    ```text
    Please enter port number[Default: 3306]

    ```

7. 接続文字列の Server にセットする値を入力します。  
        RDSインスタンスの **エンドポイント** を入力し、 Enter キーを押下してください。  
        例：{DB識別子等の文字列}.rds.amazonaws.com
    ```text
    ConnectionString Server [Default: localhost] :

    ```

8. SaConnectionString の UID にセットする値を入力します。
    RDSインスタンスに設定した **マスターユーザー名** を入力し Enter キーを押下してください。
    ```text
    SaConnectionString UID [Default: root] :

    ```

9. SaConnectionString の PWD にセットする値を入力します。  
    RDSインスタンスに設定した **マスターパスワード** を入力し Enter キーを押下してください。  
    ※パスワードはマスクされた状態で表示されます。
    ```text
    SaConnectionString PWD :
    Enter your password:

    ```

10. OwnerConnectionString の PWD にセットする値を入力します。
    ※パスワードはマスクされた状態で表示されます。
    ```text
    OwnerConnectionString PWD :
    Enter your password:

    ```

11. UserConnectionString の PWD にセットする値を入力します。
    ※パスワードはマスクされた状態で表示されます。
    ```text
    UserConnectionString PWD :
    Enter your password:

    ```

12. MySqlConnectingHost にセットする値を入力します。  
「%」の場合は空白で Enter キーを押下してください。  
```text
MySQL Connecting Host [Default: %] :

```

**"MySqlConnectingHost"について**

Ver.1.4.18.0以降で追加された[Rds.json](../../parameters/rds-json.md)の"MySqlConnectingHost"について詳細は下記を参照ください。

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

-   以下の要件が特段ない場合（既定値）　：　"%"  
-   指定の外部のホスト以外からMySQLへのアクセスを禁じる場合　：　"接続を許可するホスト名／IPアドレス（AWSの場合はプライベートIPアドレスを設定します）"。半角カンマ区切りで複数指定可（例："hostname01,hostname02"）

</details>

13. 「既定の言語」を入力します。
    対応する言語の番号を入力してください。
    ```text
    DefaultLanguage [1: English(Default), 2: Chinese, 3: Japanese, 4: German, 5: Korean, 6: Spanish, 7: Vietnamese] :

    ```

14. 「既定のタイムゾーン」を入力します。
    対応するタイムゾーンの番号を入力してください。
    ※「3」 を入力した場合は、使用するOS で利用できるタイムゾーンを入力してください。
    ```text
    Set the default time zone.
    TimeZoneDefault [1: UTC(Default), 2: Asia/Tokyo, 3: Other] :

    ```

15. サマリ画面が表示されます。  
    入力した値に間違いがない場合は、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
    ※パスワードはマスクされています。  
    ```text
    ――― Summary ―――
    Install Directory         : /web/pleasanter
    DBMS                      : MySQL
    SaConnectionString PWD    : ＊＊＊
    OwnerConnectionString PWD : ＊＊＊
    UserConnectionString PWD  : ＊＊＊
    Port                      : 3306
    Server                    : {DB識別子等の文字列}.rds.amazonaws.com
    Service Name              : Implem.Pleasanter
    MySqlConnectingHost       : %
    DefaultLanguage           : ja
    DefaultTimeZone           : Asia/Tokyo
    [Issues]
        Class       :
        Num         :
        Date        :
        Description :
        Check       :
        Attachments :
    [Results]
        Class       :
        Num         :
        Date        :
        Description :
        Check       :
        Attachments :
    ―――――――――
    Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’.:

    ```

16. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。
    下記ログが表示されたらセットアップは終了です。
    ```text
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

17. セットアップが終了すると、Webブラウザが起動して[Enterprise Editionトライアルの案内ページ](https://pleasanter.org/pleasanter-extensions-trial/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route01)が表示されます。

    ★画面を追加する

### 2. プリザンターの起動確認
1. 以下コマンドを実行して、ec2-userでプリザンターを起動します。

    ```
    cd /web/pleasanter/Implem.Pleasanter
    sudo -u ec2-user /usr/local/bin/dotnet Implem.Pleasanter.dll
    ```

2. 起動中に別のターミナルで以下コマンドを実行し、プリザンターが起動していることを確認します。「Ctrl+C」で終了します。

* 実行コマンド

```
curl -v http://localhost:5000/
```

* 実行結果

```
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

### 3. Pleasanterサービス用スクリプトの作成
/etc/systemd/system/pleasanter.service を以下の内容で作成します。
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
User = ec2-user
Group = root
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy = multi-user.target
```

### 4. サービスとして登録・サービスの起動
以下コマンドを実行してプリザンターのサービス起動およびサービス自動起動を有効化します。

```
sudo systemctl daemon-reload
sudo systemctl enable pleasanter
sudo systemctl start pleasanter
```

## 5. リバースプロキシ(nginx)のセットアップ
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
1. /etc/nginx/conf.d/pleasanter.conf を以下の内容で作成します。 server_name 行にはEC2インスタンスのパブリックIPアドレスを指定します。   

    **注意**  
    パブリックIPアドレスはEC2インスタンスの再起動時に変更されてしまいます。固定IPアドレス取得はElastic IP アドレスの利用をご検討ください。  

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

## 6. プリザンターの動作確認

1. プリザンターの起動を確認可能なアドレスは2種類あります。  
    パブリックIPアドレスおよびパブリックDNSは、EC2のインスタンスの管理画面から確認します。
    1. http://{EC2のパブリックIPアドレス}
    2. http://{EC2のパブリックDNS}  
        例：http://{文字列}.compute.amazonaws.com

2. プリザンターを起動後、プリザンターのログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
       ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/e5844c62d5424d1d91a0e7349425789e.png)

3. ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
       ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/58cafc7bb4ee464fab31b7990e7cd790.png)

### 正しくリダイレクトされない場合
nginxの設定が正しいか確認してください。記述内容の / の有無など細かな違いで動作が変わる場合があります。  

### プリザンターの画面が開かない場合
上記までの手順において特にエラーも出ずに完了したにも関わらず、ブラウザでアクセスすると「Welcome to nginx!」といったページ(エラー表示ではない)が表示される場合、ブラウザのセキュリティ設定により、プリザンターのログイン画面に遷移できていない可能性があります。  
お使いのブラウザのセキュリティ設定を確認してください。

## プリザンターのバージョンアップ
本手順でインストールしたプリザンターのバージョンアップ手順は以下マニュアル参照してください。  
[インストーラを利用したバージョンアップ手順(Linux)](../../version-up-migration/version-up-installer/version-up-installer-linux.md)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能の追加に伴いマニュアル新規作成|

## 関連情報
[インストーラを利用したバージョンアップ手順(Linux)](../../version-up-migration/version-up-installer/version-up-installer-linux.md)
