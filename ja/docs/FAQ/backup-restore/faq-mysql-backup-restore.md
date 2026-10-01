---
title: MySQL データベース バックアップ・リストア手順
category: FAQ：バックアップ、リストア
order: '200'
status: ''
parts: ''
urlstring: faq-mysql-backup-restore
translationKey: faq-mysql-backup-restore
shortname: ''
created: 2024-09-18
updated: 2025-07-08
---

本手順はユーザマニュアルのインストール手順で構築したプリザンターのデータベース(Implem.Pleasanter)を対象としています。

## 手順

1.  バックアップ
    1.  バックアップ
    1.  定期的にバックアップ
1.  リストア
    1.  同じ環境へリストア
    1.  異なる環境へリストア

## 1. バックアップ

### 1. バックアップ

バックアップファイルを取得します。この手順では /backup ディレクトリ配下に取得します。

``` bash
sudo mkdir /backup
sudo chown -R 【mysqldumpを実行するユーザ名】 /backup
mysqldump -u root -p Implem.Pleasanter > /backup/Implem.Pleasanter.dump
```

### 2. 定期的にバックアップ

定期的にバックアップおよびバックアップファイルの削除を行いたい場合は、下記のようにcronを設定してください。

``` cron title="毎日2:00にデータベースのバックアップを取得"
00 02 * * * /bin/mysqldump -u root -p【MySQLのrootアカウントのパスワードを-pとの間に空白を入れずに記述】 Implem.Pleasanter > /backup/`date "+\%Y\%m\%d"`_Implem.Pleasanter.dump
```

``` cron title="毎日1:00に一週間以上前のファイルを削除"
00 01 * * * /bin/find /backup -maxdepth 1 -mtime +7 -type f -delete
```

``` bash title="上記の設定で実行するコマンド"
sudo crontab -u 【バックアップ取得を実行するLinuxユーザ名※】 -e
```

!!! note
    プリザンターを実行するLinuxユーザと同一で問題ありません。

## 2. リストア

### 1. 同じ環境へリストア

1.  リストア後切り戻せるように、リストア実行前のバックアップを取得します。

    ``` bash
    mysqldump -u root -p Implem.Pleasanter > 【リストア前に取得するバックアップファイルの出力先パス/ファイル名】
    ```

1.  MySQLのrootアカウントでデータベースにログインします。

    ``` bash
    mysql -u root -p
    ```

1.  SQLでデータベース（Implem.Pleasanter）を削除、再作成を行い、データベースからログアウトします。

    ``` sql
    drop database `Implem.Pleasanter`;
    create database `Implem.Pleasanter` collate utf8mb4_general_ci;
    quit;
    ```

1.  リストアのコマンドを実行します。この手順では /backup ディレクトリ配下のバックアップファイルでデータベースを復元します。

    ``` bash
    mysql -u root -p Implem.Pleasanter < /backup/Implem.Pleasanter.dump
    ```

### 2. 異なる環境へリストア

データベースは、上記「同じ環境へリストアを行う場合」と同様の手順で移行します。アプリケーションが該当データベースにアクセスする際に使用するMySQLユーザアカウントは、SQLで新規作成します。

#### 1. データベースの移行

1.  移行先でMySQLにログインします。

    ``` bash
    mysql -u root -p
    ```

1.  SQLでデータベース（Implem.Pleasanter）作成を行い、データベースからログアウトします。

    ```sql
    create database `Implem.Pleasanter` collate utf8mb4_general_ci;
    quit;
    ```

1.  移行先でリストアのコマンドを実行します。この手順では移行先の /migrate ディレクトリ配下のバックアップファイルでデータベースを移行します。

    ``` bash
    mysql -u root -p Implem.Pleasanter < /migrate/Implem.Pleasanter.dump
    ```

#### 2. MySQLユーザアカウントの追加

1.  移行先でMySQLにログインします。

    ``` bash
    mysql -u root -p
    ```

1.  SQLでMySQLのユーザアカウントを2件追加し、データベースからログアウトします。

    !!! warning
        以下のSQLでは、ユーザマニュアルのインストール手順で作成したMySQLのユーザアカウントと同一のユーザアカウントを移行先のデータベース上に作成します。

    ```sql
    create user '【Ownerのユーザ名】'@'localhost' identified by '【Ownerのパスワード文字列】';
    grant create, alter, index, drop on `【データベース名】`.* to '【Ownerのユーザ名】'@'localhost';
    grant select, insert, update, delete, create routine, alter routine on `【データベース名】`.* to '【Ownerのユーザ名】'@'localhost' with grant option;
    create user '【Userのユーザ名>'@'localhost' identified by '【Userのパスワード文字列>';
    grant select, insert, update, delete, create routine, alter routine on `【データベース名】`.* to '【Userのユーザ名】'@'localhost';
    quit;
    ```

    上記SQLにおける可変部の設定値は下記の通りです。

    | 可変部                  | 設定例                  | 説明                                                                                                                                                    |
    | :---------------------- | :---------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | データベース名          | Implem.Pleasanter       | 上記「データベースの移行」で追加したデータベース名                                                                                                      |
    | Ownerのユーザ名         | Implem.Pleasanter_Owner | [Rds.json](../../setup/parameters/rds-json.md)の"OwnerConnectionString"のUIDと一致する文字列。#ServiceName#部分は上記「データベース名」に置き換えること |
    | Ownerのパスワード文字列 | SetAdminsPWD            | [Rds.json](../../setup/parameters/rds-json.md)の"OwnerConnectionString"のPWDと一致する文字列                                                            |
    | Userのユーザ名          | Implem.Pleasanter_User  | [Rds.json](../../setup/parameters/rds-json.md)の"UserConnectionString"のUIDと一致する文字列。#ServiceName#部分は上記「データベース名」に置き換えること  |
    | Userのパスワード文字列  | SetUsersPWD             | [Rds.json](../../setup/parameters/rds-json.md)の"UserConnectionString"のPWDと一致する文字列                                                             |

    ##### 作成するSQLの例

    例：[Rds.json](../../setup/parameters/rds-json.md)に記載されている接続文字列が以下の設定である場合

    ``` json title="Rds.json"
    "OwnerConnectionString": "Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_Owner;PWD=SetAdminsPWD",
    "UserConnectionString": "Server=localhost;Port=3306;Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD",
    ```

    上記の[Rds.json](../../setup/parameters/rds-json.md)の設定にもとづくMySQLユーザアカウント作成SQLの例：

    ``` sql
    create user 'Implem.Pleasanter_Owner'@'localhost' identified by 'SetAdminsPWD';
    grant create, alter, index, drop on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'localhost';
    grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_Owner'@'localhost' with grant option;
    create user 'Implem.Pleasanter_User'@'localhost' identified by 'SetUsersPWD';
    grant select, insert, update, delete, create routine, alter routine on `Implem.Pleasanter`.* to 'Implem.Pleasanter_User'@'localhost';
    ```

#### 3. 外部からMySQに接続するためのMySQLユーザアカウントの追加

WebサーバとDBサーバを分離した構成にする場合は、以下の手順を参照して外部からMySQに接続するためのユーザアカウントを追加します。

##### Ver.1.4.18.0以降の場合

〈追加手順〉  
[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.18.0以降）](../../setup/additional/db-server/mysql-connecting-host-description.md)  
└1. 新規環境構築手順

##### Ver.1.4.17.1以前の場合**

〈追加手順〉  
[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../setup/additional/db-server/mysql-create-user-by-sql.md)  
└【共通手順】外部接続用のユーザアカウントを追加するSQLの構文

なお、「[WebサーバとDBサーバを分離した構成でMySQLを利用できるように設定する（Ver.1.4.17.1以前）](../../setup/additional/db-server/mysql-create-user-by-sql.md)」対象のプリザンターのバージョンはver1.4.10.0以降です。ver1.4.9.xではMySQLのインストール先と異なるホストでプリザンターを運用することはできないため、注意してください。

## 対応バージョン

| 対応バージョン | 内容                                                                                                                              |
| :------------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| 1.4.9.0 以降   | MySQLへの対応に伴いFAQを新規作成                                                                                                  |
| 1.4.10.0 以降  | 「異なる環境へリストアを行う場合」に「外部からMySQに接続するためのMySQLユーザアカウントの追加」Ver.1.4.17.1以前の場合の手順を追加 |
| 1.4.18.0 以降  | 「異なる環境へリストアを行う場合」に「外部からMySQに接続するためのMySQLユーザアカウントの追加」Ver.1.4.18.0以降の場合の手順を追加 |
