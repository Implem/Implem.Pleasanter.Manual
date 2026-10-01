---
title: Rds.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: rds-json
translationKey: rds-json
shortname: Rds.json
created: 2019-04-30
updated: 2025-07-08
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Dbms|"SQLServer"|利用するデータベースに合わせて"SQLServer"、"PostgreSQL"、"MySQL"のいずれかを指定。.NET Framework版では"SQLServer"から変更不可。"MySQL"はver1.4.9.0以降のみ対応。|
|Provider|"Local"|通常は"Local"を指定。Azure SQL Databaseを利用する場合には"Azure"を指定。|
|SaConnectionString|sa権限の接続文字列|データベースインスタンスにsa権限で接続するための接続文字列を指定。システム環境変数に登録可能。|
|OwnerConnectionString|dbowner権限の接続文字列|Pleasanterのデータベースにdbowner権限で接続するための接続文字列を指定。システム環境変数に登録可能。|
|UserConnectionString|dbreader,dbwriter権限の接続文字列|Pleasanterのデータベースにdbreader,dbwriter権限で接続するための接続文字列を指定。システム環境変数に登録可能。|
|SqlCommandTimeOut|600|SQLコマンドのタイムアウト時間を秒単位で指定。|
|MinimumTime|3|データベースが識別可能な最小時間単位をミリ秒で指定。**本パラメータは変更不可。**|
|DeadlockRetryCount|4|デッドロック発生時の最大再試行回数を指定。|
|DeadlockRetryInterval|1000|デッドロック発生時に再試行を行うまでの間隔をミリ秒単位で指定。|
|DisableIndexChangeDetection|false|バージョンアップ時にデータベースのインデックスの差異を検出しない場合はtrueを指定。手動でインデックスを設定する場合などに設定したインデックスが失われないようtrueを指定する。|
|SysLogsSchemaVersion|1|[システムログの拡張機能](../../managers-guide/system-log-administration/syslog-extension.md)を利用する場合は2を指定。|
|MySqlConnectingHost|"%"|MySQLの場合のみ、MySQLへのユーザアクセス権について下記「MySqlConnectingHostの設定値」の通り指定する。SQLServerおよびPostgreSQLでは設定不要。|

## MySqlConnectingHostの設定値

-   同一サーバにMySQLとプリザンターが共存する環境を構築する場合  

    |条件|設定値|
    |:--|:--|
    |以下の要件が特段ない場合（既定値）|"%"|
    |外部のホストからMySQLへのアクセスを禁じる場合 |"localhost"|

-   MySQLとプリザンターのサーバを分離して構築する場合  

    |条件|設定値|
    |:--|:--|
    |以下の要件が特段ない場合（既定値）|"%"|
    |指定の外部のホストのみMySQLへアクセスを許可する場合|"接続を許可するホスト名／IPアドレス"。半角カンマ区切りで複数指定可（例："hostname01,hostname02"）|

    MySQLとプリザンターのサーバを分離して構築する場合は追加手順が必要です。詳細は「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../additional/db-server/mysql-connecting-host-description.md)」を参照してください。

## システム環境変数への登録方法

SaConnectionString、OwnerConnectionString、UserConnectionString、MySqlConnectingHostは[システム環境変数に登録](credentials-in-environment-variables.md)できます。システム環境変数への登録については以下ページも参照ください。  
[パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)

### 1. 命名規則

接続文字列についてシステム環境変数の命名規則は以下の通りです。

``` text
（サービス名）_Rds_（データベースの種類）_（ユーザの種類）ConnectionString
```

|項目|必須|説明|
|---|---|---|
|サービス名|○|[Service.json](service-json.md)の「EnvironmentName」または「Name」を指定|
|データベースの種類||次のいずれかの値を指定。"SQLServer"、"PostgreSQL"、"MySQL"|
|ユーザの種類||次のいずれかの値を指定。"Sa"、"Owner"、"User"|

#### SaConnectionStringの設定例

|データベース|変数|設定例|
|:--|:--|:--|
|SQL Server|Implem.Pleasanter_Rds_SQLServer_SaConnectionString|Server=(local);Database=master;UID=sa;PWD=<設定したパスワード>;Connection Timeout=30;|
|PostgreSQL|Implem.Pleasanter_Rds_PostgreSQL_SaConnectionString|Server=localhost;Database=postgres;UID=postgres;PWD=<設定したパスワード>|
|MySQL|Implem.Pleasanter_Rds_MySQL_SaConnectionString|Server=localhost;Database=mysql;UID=root;PWD=<設定したパスワード>|

#### OwnerConnectionStringの設定例

|データベース|変数|設定例|
|:--|:--|:--|
|SQL Server|Implem.Pleasanter_Rds_SQLServer_OwnerConnectionString|Server=(local);Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<設定したパスワード>;Connection Timeout=30;|
|PostgreSQL|Implem.Pleasanter_Rds_PostgreSQL_OwnerConnectionString|Server=localhost;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<設定したパスワード>|
|MySQL|Implem.Pleasanter_Rds_MySQL_OwnerConnectionString|Server=localhost;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=<設定したパスワード>|

#### UserConnectionStringの設定例

|データベース|変数|設定例|
|:--|:--|:--|
|SQL Server|Implem.Pleasanter_Rds_SQLServer_UserConnectionString|Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=<設定したパスワード>;Connection Timeout=30;|
|PostgreSQL|Implem.Pleasanter_Rds_PostgreSQL_UserConnectionString|Server=localhost;Database=#ServiceName#;UID=#ServiceName#_User;PWD=<設定したパスワード>|
|MySQL|Implem.Pleasanter_Rds_MySQL_UserConnectionString|Server=localhost;Database=#ServiceName#;UID=#ServiceName#_User;PWD=<設定したパスワード>|

MySqlConnectingHostについてシステム環境変数の命名規則は以下の通りです。

``` text
（サービス名）_Rds_MySqlConnectingHost
```

|項目|必須|説明|
|---|---|---|
|サービス名|○|[Service.json](service-json.md)の「EnvironmentName」または「Name」を指定|

#### MySqlConnectingHostの設定例

|変数|設定例|
|:--|:--|
|Implem.Pleasanter_Rds_MySqlConnectingHost|192.168.1.100|

### 2. 優先順

本パラメータファイルとシステム環境の両方に設定した場合や省略形で設定した場合の優先順位は以下のとおりです。

#### SaConnectionStringの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「SaConnectionString」|
|2|環境変数の「（サービス名：EnvironmentName）_Rds_SaConnectionString」|
|3|環境変数の「（サービス名：EnvironmentName）_Rds_ConnectionString」|
|4|環境変数の「（サービス名：Name）_Rds_（データベースの種類）_SaConnectionString」|
|5|環境変数の「（サービス名：Name）_Rds_（データベースの種類）_ConnectionString」|
|6|環境変数の「（サービス名：Name）_Rds_SaConnectionString」|
|7|環境変数の「（サービス名：Name）_Rds_ConnectionString」|

#### OwnerConnectionStringの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「OwnerConnectionString」|
|2|環境変数の「（サービス名：EnvironmentName）_Rds_OwnerConnectionString」|
|3|環境変数の「（サービス名：EnvironmentName）_Rds_ConnectionString」|
|4|環境変数の「（サービス名：Name）_Rds_（データベースの種類）_OwnerConnectionString」|
|5|環境変数の「（サービス名：Name）_Rds_（データベースの種類）_ConnectionString」|
|6|環境変数の「（サービス名：Name）_Rds_OwnerConnectionString」|
|7|環境変数の「（サービス名：Name）_Rds_ConnectionString」|

#### UserConnectionStringの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「UserConnectionString」|
|2|環境変数の「（サービス名：EnvironmentName）_Rds_UserConnectionString」|
|3|環境変数の「（サービス名：EnvironmentName）_Rds_ConnectionString」|
|4|環境変数の「（サービス名：Name）_Rds_（データベースの種類）_UserConnectionString」|
|5|環境変数の「（サービス名：Name）_Rds_（データベースの種類）_ConnectionString」|
|6|環境変数の「（サービス名：Name）_Rds_UserConnectionString」|
|7|環境変数の「（サービス名：Name）_Rds_ConnectionString」|

#### MySqlConnectingHostの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「MySqlConnectingHost」|
|2|環境変数の「（サービス名：EnvironmentName）_Rds_MySqlConnectingHost」|
|3|環境変数の「（サービス名：Name）_Rds_MySqlConnectingHost」|

### 3. システム環境変数に登録する際の注意点

「2. 優先順」に記載の通りパラメータファイルに設定した値が最優先となるため、システム環境変数に登録する場合はパラメータファイルでは「null」を指定してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.9.0 以降|MySQLに対応|
|1.4.18.0 以降|MySqlConnectingHostを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [システムログの拡張機能](../../managers-guide/system-log-administration/syslog-extension.md)
-   [WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../additional/db-server/mysql-connecting-host-description.md)
-   [パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)
-   [パラメータ設定：Service.json](service-json.md)
