---
title: インストーラでプリザンターをUbuntuにインストールする
category: プリザンターのインストール(インストーラ)
order: '400'
status: ''
parts: ''
urlstring: getting-started-installer-pleasanter-ubuntu
translationKey: getting-started-installer-pleasanter-ubuntu
shortname: プリザンターのインストール,プリザンターのインストール（インストーラ）,インストーラ,Linuxにインストール
created: 2024-11-26
updated: 2026-07-17
---

## 概要

本手順は[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用してプリザンターの動作環境を構築する手順です。モジュールの配置やパラメータ設定を手動で行う今までの手順でもインストール可能です。手動インストールの手順は以下を参照ください。
[プリザンターをUbuntuにインストールする](../install-manually/getting-started-pleasanter-ubuntu.md)

|対象|内容|
|---|---|
|OS|Ubuntu 24.04|
|DB|PostgreSQL 18 / MySQL 8.4|
|Webサーバ|nginx 1.24.0|
|Platform|.NET 10.0.100|
|Pleasanter|プリザンター 1.5.0.0以降|

## 注意事項

1. MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。
1. MySQLにおいてWebサーバとDBサーバを分離した構成にする場合は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../additional/db-server/mysql-connecting-host-description.md)  」または「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)」を参照ください。

## 制限事項

[インストーラ](getting-started-installer-pleasanter-almalinux.md)を使用したインストールはVer1.5.0.0以降が対象です。Ver1.4.23.3以前をインストールする際は手動インストールの手順を参照ください。  
[プリザンターをUbuntuにインストールする](../install-manually/getting-started-pleasanter-ubuntu.md)

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
sudo ./dotnet-install.sh -c 10.0 -i /usr/local/bin
dotnet --version
```

詳細につきましては下記公式ページの **スクリプトでのインストール** をご参照ください。  
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-scripted-manual#scripted-install  

また、dotnetコマンドを実行した際に特定のファイルに関するエラーが発生するケースがございます。その際は下記ページをご参照ください。
https://learn.microsoft.com/ja-jp/dotnet/core/install/linux-package-mixup?pivots=os-linux-ubuntu

## 2. データベースのセットアップ

以下の「PostgreSQLのセットアップ」または「MySQLのセットアップ」のいずれかを参照し、データベースをセットアップします。

<details markdown="1">
<summary style="font-weight:bold">1. PostgreSQLのセットアップ</summary>
PostgreSQLのセットアップ手順は以下の通りです。

#### 1. PostgreSQLのインストール

以下コマンドを実行してPostgreSQLをインストールします。

```
sudo apt install curl ca-certificates
sudo install -d /usr/share/postgresql-common/pgdg
sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
sudo sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
sudo apt update
sudo apt -y install postgresql-18
```

#### 2. PostgreSQLユーザの設定

1. 以下コマンドを実行して、PostgreSQL管理用のユーザー"postgres"(OSのユーザー)にパスワードを設定します。  
       コマンド実行後にパスワード入力プロンプトが表示しますので、パスワードを入力します。  

    ```
    sudo passwd postgres
    ```

2. 以下コマンドを実行して、PostgreSQLにログインします。

    ```
    sudo su - postgres
    psql -U postgres
    ```

3. 以下コマンドを実行して、PostgreSQLの管理ユーザー "postgres" のパスワードを設定します。ここで設定したパスワードは手順3.2.で使用しますので忘れないように控えてください。

    ```
    postgres=# alter role postgres with password '<新しいパスワード>';
    ```

#### 3. PostgreSQLのログ出力設定

/etc/postgresql/18/main/postgresql.confを開き、以下の設定を編集します。

```
log_destination = 'stderr'
logging_collector = on
log_line_prefix = '[%t]%u %d %p[%l]'
```

#### 4. PostgreSQLのサービス再起動、サービス化 

以下コマンドを実行してPostgreSQLのサービス再起動およびサービス自動起動を有効化します。

```
sudo systemctl restart postgresql
sudo systemctl enable postgresql
```

#### 5. 外部からDBへのアクセスを許可する場合の設定

1. /etc/postgresql/18/main/postgresql.conf の以下の2行のコメントを解除して下記のように設定します。  

    ```
    # - Connection Settings -
    listen_addresses = '*'  # what IP address(es) to listen on;
    port = 5432             # (change requires restart)
    ```

2. /etc/postgresql/18/main/pg_hba.conf に以下の行を追加します。Address欄にはアクセスを許可するIPアドレスの範囲を指定します。  

    ```
    # TYPE  DATABASE        USER            ADDRESS                 METHOD
    host    all             all             192.168.1.0/24          scram-sha-256
    ```

3. 設定後、以下コマンドを実行して、PostgreSQLのサービスを再起動します。

    ```
    sudo systemctl restart postgresql
    ```

</details>

<details markdown="1">
<summary style="font-weight:bold">2. MySQLのセットアップ</summary>
MySQLのセットアップ手順は以下の通りです。

#### 1. MySQLのインストール

1. 以下コマンドを実行して、MySQLのDEBパッケージをダウンロードし、インストールします。

    ```
    sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.36-1_all.deb
    sudo dpkg -i mysql-apt-config_0.8.36-1_all.deb
    ```

    コマンドで指定したURLにつきましては下記公式リポジトリの指定と同一のURLです。  
    https://dev.mysql.com/downloads/repo/apt/  

2. CUIの画面上で「パッケージの設定」画面が表示されます。以下のように「MySQL Server & Cluster (Currently selected: mysql-8.4-lts)」が表示されていることを確認してください。
    ![「パッケージの設定」の画面。選択中の「MySQL Server & Cluster」のバージョンが表示されている](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/9e43a5a7c9214a8a8c8e267989a55283.png)

3. キーボードを操作して「Ok」を選択し、Enterキーを押します。

4. 以下コマンドを実行して、MySQLのサーバをインストールします。

    ```
    sudo apt-get update
    sudo apt-get install mysql-server -y
    ```

5. CUIの画面上でMySQLのrootアカウントのパスワード設定を求められます。任意のパスワード文字列を入力後、キーボードを操作して〈了解〉を選択しEnterキーを押してください。ここで設定したパスワードは手順3.2.で使用しますので忘れないように控えてください。
    ![MySQL の root アカウントのパスワードを入力する CUI の画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/8cf558ad19f64d959042ce8259e22769.png)

6. パスワードの再入力を求められます。同一のパスワード文字列を入力後、キーボードを操作して〈了解〉を選択しEnterキーを押してください。
    ![MySQL の root アカウントのパスワードを再入力する CUI の画面](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/085e5f007daf4fad9cc7e2435782e978.png)

7. コマンドを実行し、サービスの状態を表示します。

    ```
    systemctl status mysql.service
    ```

8. 以下のように「Active: active (running)」の文字が表示され、サービスが起動されていることを確認します。

    ```
    ● mysql.service - MySQL Community Server
         Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
         Active: active (running) since Sat 2024-10-08 19:00:00 JST; 1min 8s ago
           Docs: man:mysqld(8)
                 http://dev.mysql.com/doc/refman/en/using-systemd.html
    （以下省略）
    ```

#### 2. MySQLのサービス自動起動を有効化

1. 以下コマンドを実行してMySQLのサービス自動起動を有効化します。

    ```
    sudo systemctl enable mysql
    ```

#### 3. MySQLユーザの設定

**MySQLのrootアカウントのパスワードを変更しない場合、以下の手順は実施不要です。**

MySQLのrootアカウントでは、上記「MySQLのインストール」の操作中に設定したパスワードを使用してください。OSまたはMySQLのバージョンによっては、インストール中にrootのパスワード設定を求められない場合があります。その場合、または、rootのパスワードを修正する場合は以下の手順を参照してください。

1. /etc/mysql/mysql.conf.d/mysqld.cnf の [mysqld] 配下に以下の設定を追記します。

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
    alter user 'root'@'localhost' identified by '<MySQLのrootアカウントの新しいパスワード>';
    ```

5. 以下コマンドを実行して、MySQLからrootアカウントをログアウトします。

    ```
    quit;
    ```

6. /etc/mysql/mysql.conf.d/mysqld.cnf の [mysqld] 配下に追記した記述を削除します。その際 [mysqld] は削除しないでください。  

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

1. /etc/mysql/mysql.conf.d/mysqld.cnf の [mysqld] 配下にあるlog-errorに記載されているログファイルのパスを確認します。  
    設定ファイルのパスは、OSまたはMySQLのバージョンにより異なる場合があります。

    ```
    [mysqld]
    log-error=/var/log/mysql/error.log
    ```

2. エラーログの出力先を変更する場合は、mysqld.cnfファイルの編集後、以下コマンドを実行してMySQLのサービスを再起動します。

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

以下コマンドを実行して、インストーラ をインストールします。プリザンターバージョン1.5.0.0以降をインストールするには、最新のインストーラーを使用してください。

（プリザンターバージョン1.4.23.0以前をインストールする場合は、[こちら](../install-manually/getting-started-pleasanter-ubuntu.md)を参照してください。）

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

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「/web/」に配置します。

        1. 下記コマンドを実行します。  
           **/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            /web/Pleasanter_1.5.x.x.zip
            ```

            ```
            pleasanter-setup -r /web/Pleasanter_1.5.x.x.zip
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
    下記ログが表示されたらセットアップは終了です。
    ```
    <SUCCESS> Starter.ConfigureDatabase: Database configuration has been completed.
    <SUCCESS> Starter.Main: All of the processes have been completed.
    Setup is complete.
    ```

16. セットアップが終了すると、Webブラウザが起動して[Enterprise Editionトライアルの案内ページ](https://pleasanter.org/pleasanter-extensions-trial/?utm_source=installer&utm_medium=app&utm_campaign=extension-trial&utm_content=route01)が表示されます。

    ![PostgreSQL 使用時の手順で、セットアップ完了後に表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/d71d76516eed44f3ab7aeca1559a3400.png)

</details>

<details markdown="1">
<summary style="font-weight:bold">MySQL使用時の手順</summary>

1. 以下コマンドを実行して、インストーラを実行します。

    ```
    pleasanter-setup
    ```

    **ネットワーク環境に接続されていない場合は、下記手順を実施してください**

    ??? note "（こちらをクリックすると詳細が開閉します）"

        1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から最新バージョンのプリザンターをダウンロードし、「/web/」に配置します。

        1. 下記コマンドを実行します。  
           **/web/** ディレクトリ配下の構成が以下のようになっていることを確認してください。

            ```text
            /web/Pleasanter_1.5.x.x.zip
            ```

            ```
            pleasanter-setup -r /web/Pleasanter_1.5.x.x.zip
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

    ![MySQL 使用時の手順で、セットアップ完了後に表示される Enterprise Edition トライアルの案内ページ](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/1718968ea97d4c9bb629afdb72e9b0f4.png)

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
*   Trying 127.0.0.1:5000...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 5000 (#0)
> GET / HTTP/1.1
> Host: localhost:5000
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 302 Found
< Date: Tue, 23 Feb 2021 09:04:33 GMT
< Server: Kestrel
< Content-Length: 0
< Location: http://localhost:5000/users/login?ReturnUrl=%2F
< X-Frame-Options: SAMEORIGIN
< X-Xss-Protection: 1; mode=block
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
sudo apt install -y nginx
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
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw status numbered
```

## 6. プリザンターの動作確認

1. プリザンターを起動後、プリザンターのログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
       ![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-with-installer/assets/8f4b033195b746c2939d76d9f7420a1f.png)

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
|1.5.0.0 以降|PostgreSQL 18に対応|

## 関連情報
[PostgreSQLが14以前のバージョンで、1.3.43.0以前のプリザンターをLinuxの環境へ導入したい](../../../FAQ/system-requirements-and-setup/faq-postgresql-14-install-pleasanter-for-linux.md)