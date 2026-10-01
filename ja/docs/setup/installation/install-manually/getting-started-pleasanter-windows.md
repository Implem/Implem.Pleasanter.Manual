---
title: プリザンターをWindowsにインストールする
category: プリザンターのインストール
order: '200'
status: ''
parts: ''
urlstring: getting-started-pleasanter-windows
translationKey: getting-started-pleasanter-windows
shortname: プリザンターのインストール,Windowsにインストール
created: 2021-07-15
updated: 2026-01-13
---

## 概要

本説明は、以下に示す環境にプリザンターの動作環境を構築するための手順を示したものです。

|対象|環境・バージョン|
|------|:--------------|
|OS|Windows Server|
|DB|SQL Server、PostgreSQL、MySQLのいずれか|
|Webサーバ|IIS|
|Platform|.NET 10（プリザンター1.5以降を利用する場合）<br>.NET 8（プリザンター1.4を利用する場合）|
|Pleasanter|PostgreSQL使用時：プリザンター 1.4.0.0以降<br>MySQL使用時：プリザンター 1.4.9.0以降|

**<span class="pl-attention">プリザンター1.5以降で、DBにSQL Serverを使用する場合は、必ず以下のマニュアルを確認してください。</span>**  
**[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../prerequisites/sqlserver-connection-string-v15.md)**

## 注意事項

1. ver1.4.6以降でのインストール時に、CodeDefinerに引数を指定しないで実行した場合、言語：英語、タイムゾーン：UTCでセットアップされますので、必要に応じて言語とタイムゾーンをご指定ください。
1. ver1.4.5以前をインストールする場合は初回インストール時のCodeDefinerのコマンドが変更されているため、以下ページを参照してください。  
[ver1.4.6以降で初回インストール時のCodeDefinerの手順について](../prerequisites/codedefiner-changed-steps.md)
1. MySQLはver1.4.9.0以降で使用できます。ver1.4.9.0より前のプリザンターはMySQLに対応していません。
1. MySQLにおいてWebサーバとDBサーバを分離した構成にする場合は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../additional/db-server/mysql-connecting-host-description.md)  」または「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../additional/db-server/mysql-create-user-by-sql.md)」を参照ください。

## 手順

構築手順は以下の通りです。
1. 事前準備
1. プリザンターのセットアップ
1. CodeDefinerの実行
1. IISのセットアップ
1. プリザンターの起動確認

## 1. 事前準備

プリザンターをインストールするために、事前準備が必要です。  
未実施の場合は以下の手順に沿ってすべてインストールしてください。  

[プリザンターをWindowsにインストールする際の事前準備](getting-preparation-pleasanter-windows.md)

## 2. プリザンターのセットアップ

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。  
   プリザンター1.4.23.3以前をインストールする場合は、[GitHub](https://github.com/Implem/Implem.Pleasanter/releases)から任意のバージョンのzipファイル（例：Pleasanter_1.4.23.3.zip）をダウンロードします。

1. ダウンロードしたzipファイルを解凍し、サーバに配置します。
Cドライブに「web」フォルダーを作成し、そこに「pleasanter」 フォルダーを配置するものとして記述します。  

  C:\web\pleasanter\Implem.Pleasanter  
  C:\web\pleasanter\Implem.CodeDefiner  
  C:\web\pleasanter\Tools
![C:\web\pleasanter に配置したフォルダをエクスプローラーで開いたところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/dbc3b0ef75244e9e8187bd47bbd03862.png)

1. C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\Rds.jsonにデータベースへの接続情報を設定します。設定例を以下に示します。必要に応じてRds.jsonのマニュアルも参照してください。
[パラメータ設定：Rds.json](../../parameters/rds-json.md)

<details markdown="1">
<summary style="font-weight:bold">SQL Server使用時のRds.jsonの設定例</summary>

|No|プロパティ名|値|
|:----|:----|:----|
|1|Dbms|"SQLServer"|
|2|SaConnectionString|"Server=(local);Database=master;UID=sa;PWD=<span class="pl-attention">XXX</span>;Connection Timeout=30;"<br>※PWDの値はSQL Serverのsaアカウントのパスワードを入力してください。|
|3|OwnerConnectionString|"Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<span class="pl-attention">XXX</span>;Connection Timeout=30;"<br>※PWDの値は任意のパスワードを入力してください。|
|4|UserConnectionString|"Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=<span class="pl-attention">XXX</span>;Connection Timeout=30;"<br>※PWDの値は任意のパスワードを入力してください。|

```json
{
    "Dbms": "SQLServer",
    "Provider": "Local",
    "SaConnectionString": "Server=(local);Database=master;UID=sa;PWD=<SQL Serverのsaアカウントのパスワード>;Connection Timeout=30;",
    "OwnerConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD;Connection Timeout=30;",
    "UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD;Connection Timeout=30;",
    "SqlCommandTimeOut": 0,
    "MinimumTime": 3,
    "DeadlockRetryCount": 4,
    "DeadlockRetryInterval": 1000,
    "DisableIndexChangeDetection": true,
    "SysLogsSchemaVersion": 1,
    "MySqlConnectingHost": "%"
}
```

なお、開発環境など、TLSサーバ証明書が設定されていないSQL Serverをデータベースとして使用する場合、各接続情報の末尾へTrustServerCertificate=True;を追加してください。

#### RDS.json（該当部分を抜粋）

```
    "SaConnectionString": "Server=(local);Database=master;UID=sa;PWD=<SQL Serverのsaアカウントのパスワード>;Connection Timeout=30;TrustServerCertificate=true;",
    "OwnerConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<任意のパスワード>;Connection Timeout=30;TrustServerCertificate=true;",
    "UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=<任意のパスワード>;Connection Timeout=30;TrustServerCertificate=true;",
```

詳細は[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../prerequisites/sqlserver-connection-string-v15.md)を確認してください。
</details>

<details markdown="1">
<summary style="font-weight:bold">PostgreSQL使用時のRds.jsonの設定例</summary>

|No|プロパティ名|値|
|:----|:----|:----|
|1|Dbms|"PostgreSQL"|
|2|SaConnectionString|"Server=localhost;Port=5432;Database=postgres;UID=postgres;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値はPostgreSQLのpostgresアカウントのパスワードを入力してください。|
|3|OwnerConnectionString|"Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|
|4|UserConnectionString|"Server=localhost;Port=5432;Database=#ServiceName#;UID=#ServiceName#_User;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|

```json
{
    "Dbms": "PostgreSQL",
    "Provider": "Local",
    "SaConnectionString": "Server=localhost;Port=5432;Database=postgres;UID=postgres;PWD=<PostgreSQLのpostgresアカウントのパスワード>",
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
|2|SaConnectionString|"Server=localhost;Port=3306;Database=mysql;UID=root;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値はMySQLのrootアカウントのパスワードを入力してください。|
|3|OwnerConnectionString|"Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|
|4|UserConnectionString|"Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=<span class="pl-attention">XXX</span>"<br>※PWDの値は任意のパスワードを入力してください。|
|5|MySqlConnectingHost|特段の要件がない場合は"%"、MySQLに対するアクセス制限を行う場合は「[パラメータ設定：Rds.json](../../parameters/rds-json.md)」を参照し適宜設定。|

```json
{
    "Dbms": "MySQL",
    "Provider": "Local",
    "SaConnectionString": "Server=localhost;Port=3306;Database=mysql;UID=root;PWD=<MySQLのrootアカウントのパスワード>",
    "OwnerConnectionString": "Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD",
    "UserConnectionString": "Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD",
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

## 3. CodeDefinerの実行

コマンドプロンプトまたはPowerShellを起動し、以下コマンドを実行します。  
※下記コマンドは初回インストール時にのみ実行します。

```
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll _rds /l "<言語>" /z "<タイムゾーン>"
```

|引数|設定例|説明|
|:--|:--|:--|
|/l|ja|Service.jsonのDefaultLanguageの値を書き換えます(※1)|
|/z|Tokyo Standard Time|Service.jsonのTimeZoneDefaultの値を書き換えます(※1)|  

(※1) 言語、タイムゾーンは以下マニュアルページを参照ください。
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

日本語環境でご利用する場合は以下コマンドとなります。

```
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll _rds /l "ja" /z "Tokyo Standard Time"
```

途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら **y** を入力してください。

## 4. IISのセットアップ

1. 「サーバマネージャー」の「ツール(T)」メニューを開き「インターネット インフォメーション サービス（IIS)マネージャー」を起動します。

1. 「アプリケーションプール」の「DefaultAppPool」を選択し、「基本設定」をクリックします。
![IISマネージャーの「アプリケーションプール」画面。「DefaultAppPool」と「基本設定」がある](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/b0d96c97e3b74d10b9f7b2c313838b67.png)

1. .Net CLR バージョンを、「マネージドコードなし」に変更します。
![「アプリケーションプールの編集」ダイアログ。.NET CLR バージョンを「マネージドコードなし」にする](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/1c29fb8bbca74307912728bf09709a6e.png)

1. 左ペインより、サイト-「Default Web Site」を選択して、右ペインの詳細設定をクリックします。
![IISマネージャーで「Default Web Site」を選び、右ペインの「詳細設定」を開くところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/1ae3f880aa014778b37641a4c74e1805.png)

1. 物理パスを、「C:\web\pleasanter\Implem.Pleasanter」と入力します。
![「詳細設定」ダイアログ。物理パスにプリザンターの配置先を入力する](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/bb117b9a1075497384806f418895b6c8.png)

1.  左ペインより、サイト-「Default Web Site」を選択して、右ペインの「再起動」をクリックして、IISを再起動します。
![IISマネージャーで「Default Web Site」を選び、右ペインの「再起動」をクリックするところ](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/ca5a5b6a74474f709d92d0aafba9b9a0.png)

1. 再起動後、右ペインの「*.80(http)参照」をクリックし、プリザンターを起動します。
![IISマネージャーの右ペイン。「*.80(http)参照」の項目がある](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/e62a3e5ca4fb4ab69b54d8dd5f0bc122.png)

## 5. プリザンターの動作確認  

1. プリザンターのログイン画面にて「ログインID: Administrator」、「初期パスワード: pleasanter」を入力し、「ログイン」ボタンをクリックします。
![プリザンターのログイン画面。ログインIDと初期パスワードを入力する](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/5477647dc121413190827affdc7fa1ff.png)

1. ログイン後に「Administrator」ユーザーのパスワード変更を求められるので、任意のパスワードを入力し、「変更」ボタンをクリックします。  
![初回ログイン後に表示される、Administrator のパスワード変更画面](https://pleasanter.org/files/images/ja/setup/installation/install-manually/assets/d57262564d8e49568553a84b273d3797.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.9.0 以降|MySQLに対応|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能を追加|
|1.5.0.0 以降|Windows Server 2025、.NET 10、SQL Server 2025、PostgreSQL 18に対応|