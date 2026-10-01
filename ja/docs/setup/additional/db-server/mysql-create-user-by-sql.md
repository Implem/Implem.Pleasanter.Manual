---
title: WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）
category: 追加設定：DBサーバ
order: '310'
status: ''
parts: ''
urlstring: mysql-create-user-by-sql
translationKey: mysql-create-user-by-sql
shortname: ''
created: 2024-10-03
updated: 2026-01-13
---

**Ver.1.4.18.0以降で手順が変わりました。**
**Ver.1.4.18.0以降の手順は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](mysql-connecting-host-description.md)」を参照してください。**

---

## 概要

プリザンターのDBにMySQLを使用する際、プリザンターの配備先と異なるサーバにDBを構築する場合の手順です。本手順が必要となる背景は「[FAQ：MySQLでWebサーバとDBサーバを分離した構成にしたい](../../../FAQ/system-requirements-and-setup/faq-mysql-multiple-server.md)」の説明を参照ください。

## 制限事項

1. 本手順を実施する際、プリザンターのバージョンは1.4.10.0 以降としてください。プリザンターはVer1.4.9.0以降でMySQLに対応しましたが、本手順はVer1.4.10.0以降でなければ実施できません。
2. SQL ServerおよびPostgreSQLでは本手順は実施不要です。

## 本手順の構成

本手順では、プリザンターを現在運用してしていない環境で新規にセットアップする場合、および、既にプリザンターを運用している環境でプリザンターとDBのサーバを分離する場合の各手順を掲載しています。

1. プリザンターを現在運用してしていない環境で新規にセットアップする場合
本手順の「1. 新規環境構築手順」を参照してください。

2. 既にプリザンターを運用している環境でプリザンターとDBのサーバを分離する場合  
本手順の「2. 既存DBの分離手順」を参照してください。

実行するSQLの内容は共通です。本手順の「【共通手順】外部接続用のユーザアカウントを追加するSQLの構文」を参照してください。

## 1. 新規環境構築手順

###  新規環境構築 - 準備

1. あらかじめ以下マニュアルの通り「CodeDefinerの実行」または「インストーラの実行」の前までセットアップを実施してください。  

    -   [インストーラでセットアップする手順](../../installation/install-with-installer/index.md)  
    -   [手動でセットアップする手順](../../installation/install-manually/index.md)

2. プリザンターおよびMySQLのサーバの設定（サーバ名やIPアドレス等）をあらかじめ決めてください。
3. [Service.json](../../parameters/service-json.md)および[Rds.json](../../parameters/rds-json.md)をあらかじめ設定してください。  
[パラメータ設定：Service.json](../../parameters/service-json.md)  
[パラメータ設定：Rds.json](../../parameters/rds-json.md)  

###  新規環境構築 - 手順

新規にプリザンターの環境を構築する際、SQLでDBユーザアカウントを追加する手順は以下の通りです。

1. [Rds.json](../../parameters/rds-json.md)を編集し、3箇所のデータベース接続文字列について（"SaConnectionString"、"OwnerConnectionString"、"UserConnectionString"）、Serverにデータベースサーバを指定してください。
2. SQLを実行するため、MySQLのサーバ上でMySQLにログインします。  

##### MySQLにログインするコマンド

※Linuxの場合は以下コマンドでMySQLにログインします。  
※Windowsの場合はAzure Data Studio等のGUIツールを使用してMySQLにログインします。また、Pathを通して「mysql」コマンドを実行できるように設定している場合は、以下コマンドでMySQLにログインすることも可能です。   
```
mysql -u root -p
```

3. 後述の「【共通手順】外部接続用のユーザアカウントを追加するSQLの構文」を参照し、計3件のMySQLユーザアカウントを新規作成します。
4. 必要に応じて、プリザンターを配備したサーバにてデータベース接続クライアントを使用し、手順3.で作成したMySQLユーザアカウントの疎通を確認してください。疎通できない場合、各サーバのファイアウォール設定や、MySQLの設定ファイルの記載内容で接続制限がかかっている可能性があるため、設定を見直してください。
5. プリザンター初回セットアップの「CodeDefinerの実行」以降または「インストーラの実行」以降の手順を実施します。

## 2. 既存DBの分離手順

### 既存DBの分離 - 準備

1. プリザンターおよびMySQLのサーバの設定（サーバ名やIPアドレス等）をあらかじめ決めてください。
2. [Service.json](../../parameters/service-json.md)および[Rds.json](../../parameters/rds-json.md)をあらかじめ設定してください。  
[パラメータ設定：Service.json](../../parameters/service-json.md)  
[パラメータ設定：Rds.json](../../parameters/rds-json.md)
3. SQLを実行する前に、プリザンターのサービスを停止します。
4. MySQLを以前から運用中のものと異なるサーバに移転する場合は、以下手順を参照しDBのバックアップ・リストアを行ってください。  
[FAQ：MySQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-mysql-backup-restore.md)  
└ 異なる環境へリストアを行う場合

運用中のMySQLを引き続き同一のサーバで使用する場合、DBのバックアップ・リストアは不要です。

### 既存DBの分離 - 手順

既にプリザンターを運用している環境でプリザンターとDBのサーバを分離する手順は以下の通りです。

1. [Rds.json](../../parameters/rds-json.md)を編集し、3箇所のデータベース接続文字列について（"SaConnectionString"、"OwnerConnectionString"、"UserConnectionString"）、Serverにデータベースサーバを指定してください。
2. SQLを実行するため、MySQLのサーバ上でMySQLにログインします。準備の際にDBのバックアップ・リストアを行った場合は、リストア先のMySQLにログインしてください。

##### MySQLにログインするコマンド

※Linuxの場合は以下コマンドでMySQLにログインします。  
※Windowsの場合はAzure Data Studio等のGUIツールを使用してMySQLにログインします。また、Pathを通して「mysql」コマンドを実行できるように設定している場合は、以下コマンドでMySQLにログインすることも可能です。   
```
mysql -u root -p
```

3. 後述の「【共通手順】外部接続用のユーザアカウントを追加するSQLの構文」を参照し、計3件のMySQLユーザアカウントを新規作成します。
4. 必要に応じて、プリザンターを配備したサーバにてデータベース接続クライアントを使用し、手順3.で作成したMySQLユーザアカウントの疎通を確認してください。疎通できない場合、各サーバのファイアウォール設定や、MySQLの設定ファイルの記載内容で接続制限がかかっている可能性があるため、設定を見直してください。
5. プリザンターのサービスを起動します。
6. ブラウザからプリザンターを使用できることを確認します。

## 【共通手順】外部接続用のユーザアカウントを追加するSQLの構文

SQLを実行し、外部のサーバから接続可能なMySQLアカウントを計3件新規作成します。

1. MySQLのrootアカウント
2. テーブル作成・変更等の権限をもつMySQLユーザアカウント（以下「Ownerアカウント」と表記）
3. テーブル参照等の権限をもつMySQLユーザアカウント（以下「Userアカウント」と表記）

各SQLは create user 文と grant 文の2行から成っており、localhost接続で同名のユーザアカウントを使用する場合と同一のパスワードと権限を設定するためのものです。

### MySQLのrootアカウントによる外部接続を許可するSQLの構文

```
create user 'root'@'<接続元>' identified by '<MySQLのrootアカウントのパスワード文字列>';
grant all on *.* to 'root'@'<接続元>' with grant option;
```

<details markdown="1">
<summary>可変部の説明</summary>

MySQLの初期セットアップ手順で設定したパスワード、および、[Rds.json](../../parameters/rds-json.md)に記載した"SaConnectionString"の内容と一致する内容を記載します。

|可変部|設定例|説明|
|:--|:--|:--|
|MySQLのrootアカウントのパスワード文字列|password|[Rds.json](../../parameters/rds-json.md)の"SaConnectionString"のPWDと一致する文字列|
|接続元|192.168.1.100|MySQLに対する接続元。詳細は後述の「接続元指定のルール」を参照。複数の接続元を指定する場合は1～2行目のSQLを接続元の件数分実行すること|

〈[Rds.json](../../parameters/rds-json.md)の"SaConnectionString"の例〉

```
"SaConnectionString": "Server=db.hostname;Port=3306;Database=mysql;UID=root;PWD=password",
```

〈SQL例〉

```
create user 'root'@'192.168.1.100' identified by 'password';
grant all on *.* to 'root'@'192.168.1.100' with grant option;
```

</details>

### Ownerアカウントによる外部接続を許可するSQLの構文

```
create user '<Ownerの名称>'@'<接続元>' identified by '<Ownerのパスワード文字列>';
grant create, alter, index, drop on `<データベース名>`.* to '<Ownerの名称>'@'<接続元>';
grant select, insert, update, delete, create routine, alter routine on `<データベース名>`.* to '<Ownerの名称>'@'<接続元>' with grant option;
```

<details markdown="1">
<summary>可変部の説明</summary>

[Rds.json](../../parameters/rds-json.md)に記載した"OwnerConnectionString"の内容と一致する内容を記載します。

|可変部|設定例|説明|
|:--|:--|:--|
|データベース名|Implem.Pleasanter|[Service.json](../../parameters/service-json.md)の"Name"と一致する文字列|
|Ownerの名称|Implem.Pleasanter_Owner|[Rds.json](../../parameters/rds-json.md)の"OwnerConnectionString"のUIDと一致する文字列。#ServiceName#部分は上記「データベース名」に置き換えること|
|Ownerのパスワード文字列|SetAdminsPWD|[Rds.json](../../parameters/rds-json.md)の"OwnerConnectionString"のPWDと一致する文字列|
|接続元|%|MySQLに対する接続元。詳細は後述の「接続元指定のルール」を参照。複数の接続元を指定する場合は1～2行目のSQLを接続元の件数分実行すること|

〈[Rds.json](../../parameters/rds-json.md)の"OwnerConnectionString"の例〉

```
"OwnerConnectionString": "Server=db.hostname;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD",
```

〈SQL例〉

```
create user 'Implem.Pleasanter_Owner'@'%' identified by 'SetAdminsPWD';
grant create, alter, index, drop on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'%';
grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'%' with grant option;
```

</details>

### Userアカウントによる外部接続を許可するSQLの構文

```
create user '<Userの名称>'@'<接続元>' identified by '<Userのパスワード文字列>';
grant select, insert, update, delete, create routine, alter routine on `<データベース名>`.* to '<Userの名称>'@'<接続元>';
```

<details markdown="1">
<summary>可変部の説明</summary>

[Rds.json](../../parameters/rds-json.md)に記載した"UserConnectionString"の内容と一致する内容を記載します。

|可変部|設定例|説明|
|:--|:--|:--|
|データベース名|Implem.Pleasanter|[Service.json](../../parameters/service-json.md)の"Name"と一致する文字列|
|Userの名称|Implem.Pleasanter_User|[Rds.json](../../parameters/rds-json.md)の"UserConnectionString"のUIDと一致する文字列。#ServiceName#部分は上記「データベース名」に置き換えること|
|Userのパスワード文字列|SetUsersPWD|[Rds.json](../../parameters/rds-json.md)の"UserConnectionString"のPWDと一致する文字列|
|接続元|%|MySQLに対する接続元。詳細は後述の「接続元指定のルール」を参照。複数の接続元を指定する場合は1～2行目のSQLを接続元の件数分実行すること|

〈[Rds.json](../../parameters/rds-json.md)の"UserConnectionString"の例〉

```
"UserConnectionString": "Server=db.hostname;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD",
```

〈SQL例〉

```
create user 'Implem.Pleasanter_User'@'%' identified by 'SetUsersPWD';
grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_User'@'%';
```

</details>

## MySQLユーザアカウントおよび許可する接続元の確認

以下SQLを実行すると、MySQL上に存在するユーザアカウントと許可されている接続元の一覧が表示されます。

```
select user, host from mysql.user;
```

〈実行結果例〉
```
+-------------------------+---------------+
| user                    | host          |
+-------------------------+---------------+
| Implem.Pleasanter_Owner | %             |
| Implem.Pleasanter_User  | %             |
| root                    | 192.168.1.100 |
| Implem.Pleasanter_Owner | localhost     |
| Implem.Pleasanter_User  | localhost     |
| mysql.infoschema        | localhost     |
| mysql.session           | localhost     |
| mysql.sys               | localhost     |
| root                    | localhost     |
+-------------------------+---------------+
```

## 接続元指定のルール

IPアドレスを接続元に指定すると、該当IPアドレスから接続が許可されます。プリザンターを配備したサーバのIPアドレスを指定してください。

```
+-------------------------+---------------+
| user                    | host          |
+-------------------------+---------------+
| root                    | 192.168.10.12 |
```

ワイルドカード記号「%」を接続元に指定すると、すべての接続元から接続が許可されます。**rootアカウントについてはセキュリティ上、接続元に「%」を指定しないでください。**

```
+-------------------------+---------------+
| user                    | host          |
+-------------------------+---------------+
| Implem.Pleasanter_Owner | %             |
```

localhost接続については本手順以外の操作で許可されるため、「【共通手順】外部接続用のユーザアカウントを追加するSQLの構文」の中で実施は不要です。

```
+-------------------------+---------------+
| user                    | host          |
+-------------------------+---------------+
| root                    | localhost     |
```

※rootアカウントの場合はMySQLのインストール時に自動で設定されます。

※OwnerアカウントおよびUserアカウントは、プリザンターの初回セットアップの場合は、CodeDefinerの実行により自動で設定されます。既に運用中のプリザンターのDBを他の環境に移転する場合は、DBのリストアの作業においてOwnerアカウントおよびUserアカウントを追加する手順があります。
[FAQ：MySQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-mysql-backup-restore.md)  
└異なる環境へリストアを行う場合

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.10.0 以降|MySQLのアクセス制御機能によりOwner、Userの接続が拒否される場合がある問題の解消に伴いマニュアル公開<br>※プリザンターはVer1.4.9.0以降でMySQLに対応しましたが、本手順はVer1.4.10.0以降でなければ実施できません。|