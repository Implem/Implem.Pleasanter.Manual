---
title: WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）
category: 追加設定：DBサーバ
order: '300'
status: ''
parts: ''
urlstring: mysql-connecting-host-description
translationKey: mysql-connecting-host-description
shortname: ''
created: 2025-06-16
updated: 2025-10-30
---

## 概要

プリザンターのDBにMySQLを使用する際、プリザンターの配備先と異なるサーバにDBを構築する場合の手順です。本手順が必要となる背景は「[FAQ：MySQLでWebサーバとDBサーバを分離した構成にしたい](../../../FAQ/system-requirements-and-setup/faq-mysql-multiple-server.md)」の説明を参照ください。

## 制限事項

1. 本手順の新規セットアップをインストーラで実施する場合、インストーラのバージョンは1.1.0以降のバージョンを利用ください。
1. SQL ServerおよびPostgreSQLでは本手順は実施不要です。
1. Ver.1.4.17.1以前の手順は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](mysql-create-user-by-sql.md)」を参照してください。

## 本手順の構成

本手順では、プリザンターを現在運用してしていない環境で新規にセットアップする場合、および、既にプリザンターを運用している環境でプリザンターとDBのサーバを分離する場合の各手順を掲載しています。

1. プリザンターを現在運用してしていない環境で新規にセットアップする場合
本手順の「1. 新規環境構築手順」を参照してください。

2. 既にプリザンターを運用している環境でプリザンターとDBのサーバを分離する場合  
本手順の「2. 既存DBの分離手順」を参照してください。

## 1. 新規環境構築手順

###  新規環境構築 - 準備

1. プリザンターおよびMySQLのサーバの設定（サーバ名やIPアドレス等）をあらかじめ決めてください。

###  新規環境構築 - 手順

新規にプリザンターの環境を構築する際、SQLでDBユーザアカウントを追加する手順は以下の通りです。

1. 新規セットアップのマニュアルの手順を初めから順番に実施し、データベースサーバ上で「MySQLのセットアップ」までおこないます。  

    -   [インストーラでセットアップする手順](../../installation/install-with-installer/index.md)  
    -   [手動でセットアップする手順](../../installation/install-manually/index.md)

2. SQLを実行するため、MySQLのサーバ上でMySQLにログインします。  
Linuxの場合は以下コマンドでMySQLにログインします。  
Windowsの場合はAzure Data Studio等のGUIツールを使用してMySQLにログインします。また、Pathを通して「mysql」コマンドを実行できるように設定している場合は、以下コマンドでMySQLにログインすることも可能です。   
``` text title="MySQLにログインするコマンド"
mysql -u root -p
```
3. [Rds.json](../../parameters/rds-json.md)の"SaConnectionString"のユーザとして指定する「MySQLの管理ユーザアカウント＠<接続元>」アカウントがMySQL上に存在するか確認します。  
確認用コマンドの結果、user：root、host：% など外部から接続可能なアカウントが存在する場合は、手順1.4は実施不要のため、手順1.5に進んでください。  
確認用コマンドは以下の通りです。  
```text
SELECT user, host FROM mysql.user;
```

**<接続元>について**

|条件|設定値|
|:--|:--|
|以下の要件が特段ない場合|%|
|指定の外部のホストのみMySQLへアクセスを許可する場合|接続を許可するホスト名／IPアドレス。複数の接続元を許可している場合は複数レコードが取得される。|

4. 「MySQLの管理ユーザアカウント＠<接続元>」アカウントがMySQL上に存在しない場合は、アカウントを追加します。
```text
create user 'root'@'<接続元>' identified by '<MySQLのrootアカウントのパスワード文字列>';
grant all on *.* to 'root'@'<接続元>' with grant option;
```
**接続を許可するホストを複数指定する場合**

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

SQL文は許可する全接続元について実行します。以下は実行SQLの例です。  

```text
create user 'root'@'192.168.1.100' identified by 'password';
grant all on *.* to 'root'@'192.168.1.100' with grant option;
create user 'root'@'192.168.1.200' identified by 'password';
grant all on *.* to 'root'@'192.168.1.200' with grant option;
```

</details>

5. データベースサーバのファイアウォールの設定を変更し、MySQLのサービスに対する外部からの接続を許可します。
6. マニュアルの手順通りにセットアップを最後まで進めます。  
インストーラまたは手動で設定する[Rds.json](../../parameters/rds-json.md)の3箇所のデータベース接続文字列について（"SaConnectionString"、"OwnerConnectionString"、"UserConnectionString"）、Serverにデータベースサーバを指定してください。
7. インストーラまたは手動で設定する[Rds.json](../../parameters/rds-json.md)の"MySqlConnectingHost"について以下の通りに指定してください。  

    |条件|設定値|
    |:--|:--|
    |以下の要件が特段ない場合（既定値）|%|
    |指定の外部のホストのみMySQLへアクセスを許可する場合|接続を許可するホスト名／IPアドレス。半角カンマ区切りで複数指定可（例：hostname01,hostname02）|

8. ブラウザからプリザンターを使用できることを確認します。

## 2. 既存DBの分離手順

### 既存DBの分離 - 準備

1. プリザンターおよびMySQLのサーバの設定（サーバ名やIPアドレス等）をあらかじめ決めてください。
2. 分離を実行する前に、プリザンターのサービスを停止します。
3. MySQLを以前から運用中のものと異なるサーバに移転する場合は、以下手順を参照しDBのバックアップ・リストアを行ってください。  
[FAQ：MySQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-mysql-backup-restore.md)  
└ 異なる環境へリストアを行う場合

運用中のMySQLを引き続き同一のサーバで使用する場合、DBのバックアップ・リストアは不要です。

### 既存DBの分離 - 手順

既にプリザンターを運用している環境でプリザンターとDBのサーバを分離する手順は以下の通りです。

1. [Rds.json](../../parameters/rds-json.md)を編集し、3箇所のデータベース接続文字列について（"SaConnectionString"、"OwnerConnectionString"、"UserConnectionString"）、Serverにデータベースサーバを指定してください。
2. [Rds.json](../../parameters/rds-json.md)を編集し、"MySqlConnectingHost"について以下の通りに指定してください。  

    |条件|設定値|
    |:--|:--|
    |以下の要件が特段ない場合（既定値）|"%"|
    |指定の外部のホストのみMySQLへアクセスを許可する場合|"接続を許可するホスト名／IPアドレス"。半角カンマ区切りで複数指定可（例："hostname01,hostname02"）|

3. SQLを実行するため、MySQLのサーバ上でMySQLにログインします。  
Linuxの場合は以下コマンドでMySQLにログインします。  
Windowsの場合はAzure Data Studio等のGUIツールを使用してMySQLにログインします。また、Pathを通して「mysql」コマンドを実行できるように設定している場合は、以下コマンドでMySQLにログインすることも可能です。   
``` text title="MySQLにログインするコマンド"
mysql -u root -p
```
4. [Rds.json](../../parameters/rds-json.md)の"SaConnectionString"のユーザとして指定する「MySQLの管理ユーザアカウント＠<接続元>」アカウントがMySQL上に存在するか確認します。  
確認用コマンドの結果、user：root、host：% など外部から接続可能なアカウントが存在する場合は、手順2.5は実施不要のため、手順2.6に進んでください。  
確認用コマンドは以下の通りです。  
```text
SELECT user, host FROM mysql.user;
```

**<接続元>について**

|条件|設定値|
|:--|:--|
|以下の要件が特段ない場合|%|
|指定の外部のホストのみMySQLへアクセスを許可する場合|接続を許可するホスト名／IPアドレス。複数の接続元を許可している場合は複数レコードが取得される。|

5. 「MySQLの管理ユーザアカウント＠<接続元>」アカウントがMySQL上に存在しない場合は、アカウントを追加します。
```text
create user 'root'@'<接続元>' identified by '<MySQLのrootアカウントのパスワード文字列>';
grant all on *.* to 'root'@'<接続元>' with grant option;
```
**接続を許可するホストを複数指定する場合**

<details markdown="1">
<summary>（こちらをクリックすると詳細が開閉します） </summary>

SQL文は許可する全接続元について実行します。以下は実行SQLの例です。  

```text
create user 'root'@'192.168.1.100' identified by 'password';
grant all on *.* to 'root'@'192.168.1.100' with grant option;
create user 'root'@'192.168.1.200' identified by 'password';
grant all on *.* to 'root'@'192.168.1.200' with grant option;
```

</details>

6. データベースサーバのファイアウォールの設定を変更し、MySQLのサービスに対する外部からの接続を許可します。
7. CodeDefinerを_rdsモードで実行します。  
``` text title="Windowsの実行例"
cd C:\web\pleasanter\Implem.CodeDefiner
dotnet Implem.CodeDefiner.dll _rds
```
``` text title="Linuxの実行例"
cd /web/pleasanter/Implem.CodeDefiner
sudo -u <プリザンターを起動するユーザ> /usr/local/bin/dotnet Implem.CodeDefiner.dll _rds
```
途中で 「Type "y" (yes) if the license is correct, otherwise type "n" (no).」 と表示されたら y を入力してください。
8. プリザンターのサービスを起動します。
9. ブラウザからプリザンターを使用できることを確認します。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.18.0 以降|MySQLのDBへの接続元ホストにlocalhost（DBと同一のサーバ）以外を指定する機能の追加に伴いマニュアルを公開|