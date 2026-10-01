---
title: インストーラでプリザンターをRed Hat Enterprise Linux 8にインストールする
category: プリザンターのインストール(インストーラ)
order: '700'
status: ''
parts: ''
urlstring: getting-started-installer-pleasanter-rhel-8
translationKey: getting-started-installer-pleasanter-rhel-8
shortname: プリザンターのインストール,プリザンターのインストール（インストーラ）,インストーラ,Linuxにインストール
created: 2024-11-26
updated: 2026-07-17
---

## 概要

本手順は[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターの動作環境を構築する手順です。モジュールの配置やパラメータ設定を手動で行う今までの手順でもインストール可能です。手動インストールの手順は以下を参照ください。
[プリザンターをRed Hat Enterprise Linux 8にインストールする](../install-manually/getting-started-pleasanter-rhel-8.md)

|対象|内容|
|---|---|
|OS|Red Hat Enterprise Linux 8.10|
|DB|PostgreSQL 17 / MySQL 8.4|
|Webサーバ|nginx 1.14.1|
|Platform|.NET 8.0.408|
|Pleasanter|PostgreSQL使用時：プリザンター 1.4.0.0以降<br />MySQL使用時：プリザンター 1.4.9.0以降|

## 注意事項

1. MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。
1. MySQLにおいてWebサーバとDBサーバを分離した構成にする場合は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../additional/db-server/mysql-connecting-host-description.md)  」または「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)」を参照ください。

## 制限事項

[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用したインストールはVer1.4.0.0以降が対象です。Ver1.3.50.2以前をインストールする際は手動インストールの手順を参照ください。
[プリザンターをRed Hat Enterprise Linux 8にインストールする](../install-manually/getting-started-pleasanter-rhel-8.md)

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
   1. Http(80) へのアクセス許可
1. プリザンターの動作確認

## 1. .NETのセットアップ

以下コマンドを実行して、.NET をインストールします。

```
sudo wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
sudo chmod +x ./dotnet-install.sh
sudo ./dotnet-install.sh -c 8.0 -i /usr/local/bin
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
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo dnf install -y postgresql17-server postgresql17-contrib
```

#### 2.  PostgreSQLデータベースの初期化

以下コマンドを実行して、データベースの初期化を行います。※ -A: 認証方式の指定、-W: パスワード入力プロンプトを表示するオプション  
実行後、パスワード入力プロンプトが表示しますので、パスワードを入力します。  ここで設定したパスワードは手順3.2.で使用しますので忘れないように控えてください。

```
sudo su - postgres -c '/usr/pgsql-17/bin/initdb -E UTF8 -A scram-sha-256 -W'
```

#### 3. PostgreSQLのログ出力設定

/var/lib/pgsql/17/data/postgresql.conf を開き、以下の設定を編集します。

```
log_destination = 'stderr'
logging_collector = on
log_line_prefix = '[%t]%u %d %p[%l]'
```

#### 4. PostgreSQLのサービス再起動、サービス化 

以下コマンドを実行してPostgreSQLのサービス再起動およびサービス自動起動を有効化します。

```
sudo systemctl restart postgresql-17.service
sudo systemctl enable postgresql-17.service
```

#### 5. 外部からDBへのアクセスを許可する場合の設定

1. /var/lib/pgsql/17/data/postgresql.conf の以下の2行のコメントを解除して下記のように設定します。  

    ```
    # - Connection Settings -
    listen_addresses = '*'  # what IP address(es) to listen on;
    port = 5432             # (change requires restart)
    ```

2. /var/lib/pgsql/17/data/pg_hba.conf に以下の行を追加します。Address欄にはアクセスを許可するIPアドレスの範囲を指定します。  

    ```
    # TYPE  DATABASE        USER            ADDRESS                 METHOD
    host    all             all             192.168.1.0/24          scram-sha-256
    ```

3. 設定後、以下コマンドを実行して、PostgreSQLのサービスを再起動します。

    ```
    sudo systemctl restart postgresql-17
    ```

</details>

<details markdown="1">
<summary style="font-weight:bold">2. MySQLのセットアップ</summary>
MySQLのセットアップ手順は以下の通りです。

#### 1. MySQLのインストール

1. 以下コマンドを実行して、MySQLのパッケージとサーバをインストールします。

    ```
    sudo dnf install -y https://dev.mysql.com/get/mysql84-community-release-el8-1.noarch.rpm
    sudo dnf install mysql-server
    ```

    コマンドで指定したURLにつきましては下記公式リポジトリの指定と同一のURLです。  
    https://dev.mysql.com/downloads/repo/yum/ 

2. コマンドを実行し、サービスの状態を表示します。

    ```
    systemctl status mysqld.service
    ```

3. 以下のように「Active: inactive (dead)」の文字が表示され、サービスが停止されていることを確認します。

    ```
    ● mysqld.service - MySQL 8.0 database server
       Loaded: loaded (/usr/lib/systemd/system/mysqld.service; disabled; vendor preset: disabled)
       Active: inactive (dead)
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

## 3. インストーラのインストール

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

1. 下記コマンドを実行して.nupkgファイルを配置する任意のフォルダを作成します。
    ※本手順では/dotnet-toolsを作成する場合として説明します。
    ```
    sudo mkdir /dotnet-tools
    ```
1. [こちら](https://www.nuget.org/packages/Implem.PleasanterSetup/) からImplem.PleasanterSetupのNuget Galleryを開き、画像の①「Download package」より.nupkgファイルをダウンロードします。
    ![Implem.PleasanterSetup の NuGet ギャラリーのページ。「Download package」がある](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/3ec2711d699e4c9eb1f978122e9bb5fc.png)
1. 手順2.2でダウンロードした.nupkgファイルを**/dotnet-tools**に配置します。
1. 画像の②のコマンドをコピーします。
1. 下記コマンド実行します。

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

<details markdown="1">
<summary style="font-weight:bold">PostgreSQL使用時の手順</summary>

1. 以下コマンドを実行して、インストーラを実行します。

    ```
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、下記手順を実施してください**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)からプリザンターをダウンロードし、「/web/」に配置します。

        1. 下記コマンドを実行します。  
           **/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            /web/Pleasanter_1.4.x.x.zip
            ```

            ```
            pleasanter-setup -r /web/Pleasanter_1.4.x.x.zip
            ```

2. プリザンターをインストールするディレクトリを入力します。  
    「/web/pleasanter」 にインストールする場合は空白で Enter キーを押下してください。
    ![インストーラがプリザンターのインストール先ディレクトリを尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/f13dfbf34ae042d3b0d29fc2a019868f.png)

3.  **<プリザンターを起動するユーザ>** を入力します。
    ![インストーラがプリザンターを起動するユーザを尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/e8c3b81488f54ab7ab82eb815a3cc292.png)

4. サービス名を入力します。
    「Implem.Pleasanter」の場合は空白で Enter キーを押下してください。
    ![インストーラがサービス名を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/380abbfe3b694fa1808943276872facf.png)

5. 使用する DBMS に対応する番号を入力します。
    ここでは「2」を入力しEnterキーを押下してください。
    ![インストーラが使用する DBMS の番号を尋ねている画面。PostgreSQL の「2」を入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/559fbf8821c547f69a7af7df541afcba.png)  

6. 利用するポート番号を入力します。
    DBMSのデフォルトのポート番号の場合は空白で Enter キーを押下してください。
    ![インストーラがデータベースのポート番号を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/8ad6a0ac806b48c8bc36ebeacf9cf4f5.png)

7. 接続文字列の Server にセットする値を入力します。
    「localhost」の場合は空白で Enter キーを押下してください。
    ![インストーラが接続文字列の Server の値を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/9f639bff6ef144dc8e7db66e87cc9852.png)

8. SaConnectionString の UID にセットする値を入力します。
    「postgres」の場合は空白で Enter キーを押下してください。
    ![インストーラが SaConnectionString の UID を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/fae77d65e09d4eee98949e7f1a0af88b.png)

9. SaConnectionString の PWD にセットする値を入力します。
    ※パスワードはマスクされた状態で表示されます。
    ![インストーラが SaConnectionString の PWD を尋ねている画面。入力はマスクされる](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/816178b1b7924d33af100c6eec8c9c24.png)  

10. OwnerConnectionString の PWD にセットする値を入力します。
    ※パスワードはマスクされた状態で表示されます。
    ![インストーラが OwnerConnectionString の PWD を尋ねている画面。入力はマスクされる](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/63271bb2323541ef8334d7b78b93d97a.png)

11. UserConnectionString の PWD にセットする値を入力します。
    ※パスワードはマスクされた状態で表示されます。
    ![インストーラが UserConnectionString の PWD を尋ねている画面。入力はマスクされる](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/1ffab3c8df6649dfb546941d37422456.png)

12. 「既定の言語」を入力します。
    対応する言語の番号を入力してください。
    ![インストーラが「既定の言語」の番号を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/0979eb4f35444d6eaad342196ba8700f.png)

13. 「既定のタイムゾーン」のタイムゾーンを入力します。
    対応するタイムゾーンの番号を入力してください。
    ※「3」 を入力した場合は、使用するOS で利用できるタイムゾーンを入力してください。
    ![インストーラが「既定のタイムゾーン」の番号を尋ねている画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/f624f5b006a349dcaa2d676b2c2ecf95.png)

14. サマリ画面が表示されます。  
    入力した値に間違いがない場合は、「Shall I install Pleasanter with this content? Please enter ‘y(yes)' or 'n(no)’. : 」 の後に **y** を入力しEnterキーで実行してください。  
    ※パスワードはマスクされています。  
    ![入力値を一覧にしたインストーラのサマリ画面。インストールするかを確認している](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/ed79489a02c943278299da3894693ca0.png)

15. 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力して実行してください。

    ```
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

16. セットアップが終了すると、Webブラウザが起動して[Enterprise Editionトライアルの案内ページ](https://pleasanter.org/pleasanter-extensions-trial/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route01)が表示されます。

    ![PostgreSQL 使用時の手順で、セットアップ完了後に表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/35c4fecc6ab74a7fa78e3254199c11fb.png)

</details>

<details markdown="1">
<summary style="font-weight:bold">MySQL使用時の手順</summary>

1. 以下コマンドを実行して、インストーラを実行します。

    ```
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、下記手順を実施してください**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)からプリザンターをダウンロードし、「/web/」に配置します。

        1. 下記コマンドを実行します。  
           **/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            /web/Pleasanter_1.4.x.x.zip
            ```

            ```
            pleasanter-setup -r /web/Pleasanter_1.4.x.x.zip
            ```

2. プリザンターをインストールするディレクトリを入力します。  
    「/web/pleasanter」 にインストールする場合は空白で Enter キーを押下してください。
    ```text
    Install Directory [Default: /web/pleasanter] :

    ```

3.  **<プリザンターを起動するユーザ>** を入力します。

    ```text
    Please enter the user who will execute Pleasanter.

    ```

4. サービス名を入力します。
    「Implem.Pleasanter」の場合は空白で Enter キーを押下してください。
    ```text
    ServiceName [Default: Implem.Pleasanter] :

    ```

5. 使用する DBMS に対応する番号を入力します。
    ここでは「3」を入力しEnterキーを押下してください。
    ```text
    DBMS [1: SQL Server, 2: PostgreSQL, 3: MySQL] :

    ```

6. 利用するポート番号を入力します。
    DBMSのデフォルトのポート番号の場合は空白で Enter キーを押下してください。
    ```text
    Please enter port number[Default: 3306]

    ```

7. 接続文字列の Server にセットする値を入力します。
    「localhost」の場合は空白で Enter キーを押下してください。
    ```text
    ConnectionString Server [Default: localhost] :

    ```

8. SaConnectionString の UID にセットする値を入力します。
    「root」の場合は空白で Enter キーを押下してください。
    ```text
    SaConnectionString UID [Default: root] :

    ```

9. SaConnectionString の PWD にセットする値を入力します。
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

12. MySqlConnectingHost にセットする値を入力します。特段の要件がない場合は「%」、MySQLに対するアクセス制限を行う場合は[Rds.json](../../parameters/rds-json.md)を参照し適宜設定します。  
    「%」の場合は空白で Enter キーを押下してください。  
    Ver.1.4.17.1以前のバージョンをインストールする際は空白でEnterキーを押下します。  
    ```text
    MySQL Connecting Host [Default: %] :

    ```

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
    Server                    : localhost
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
    ```
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

17. セットアップが終了すると、Webブラウザが起動して[Enterprise Editionトライアルの案内ページ](https://pleasanter.org/pleasanter-extensions-trial/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route01)が表示されます。

    ![MySQL 使用時の手順で、セットアップ完了後に表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/a1705488055c4372be286a7b2dc02a28.png)

</details>

### 2. プリザンターの起動確認

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

### 3. Pleasanterサービス用スクリプトの作成
/etc/systemd/system/pleasanter.service を以下の内容で作成します。下記の **User** にはあらかじめ決めたプリザンターを起動するユーザを指定してください。

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

## 6. プリザンターの動作確認

1. プリザンターを起動後、プリザンターのログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
       ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/5477647dc121413190827affdc7fa1ff.png)

2. ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
       ![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/0ff466031f9f41719bb5eb9f8190c218.png)

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

## 関連情報
[PostgreSQLが14以前のバージョンで、1.3.43.0以前のプリザンターをLinuxの環境へ導入したい](../../../FAQ/system-requirements-and-setup/faq-postgresql-14-install-pleasanter-for-linux.md)