---
title: 異なる種類のDBにプリザンターのデータを移行する手順
category: 移行
order: '900'
status: ''
parts: ''
urlstring: migrate
translationKey: migrate
shortname: ''
created: 2025-02-03
updated: 2026-01-13
---

## 概要

[CodeDefiner](../../../FAQ/system-requirements-and-setup/faq-codedefiner-about.md)を使用して異なる種類のDBにプリザンターのデータを移行する手順です。

下図で示す通り、プリザンターのサーバを新規構築する際、既に稼働している別のプリザンターのサーバからDBの全データを移行し、同じ状態のプリザンターを構築することが可能です。ID値が移行元DBと同一のものとなりますので、移行先DBにプリザンターのデータを事前に登録しておくことはできません。（移行先DBにデータが登録されていると、データの移行処理が一意制約違反エラーで失敗します。）

![CodeDefinerで移行元DBから移行先DBへ全データを移行する構成図](https://pleasanter.org/files/images/ja/setup/version-up-migration/migration/assets/9424d0872c3e4f5ba61bd3405736b0f6.png)

※同じ種類のDB間でデータ移行を行う場合は、本手順ではなく、バックアップ・リストア手順を実施してください。

-   SQL Server：[異なる環境にプリザンターのデータベース(SQL Server)を移行する手順](migrate-to-other-environment-pleasanter-net5.md)を参照
-   PostgreSQL：[FAQ：PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)を参照
-   MySQL：[FAQ：MySQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-mysql-backup-restore.md)を参照

## 制限事項

1.  下表のとおり、移行可能なデータベースの種類に制限がございます。

    | 移行元     | 移行先     | 本手順の使用可否 | 備考                                                     |
    | :--------- | :--------- | :--------------- | :------------------------------------------------------- |
    | SQL Server | PostgreSQL | 可               | -                                                        |
    | SQL Server | MySQL      | 可               | バージョン1.4.12.0以前のプリザンターでは、移行できません |
    | PostgreSQL | SQL Server | 不可             | -                                                        |
    | PostgreSQL | MySQL      | 不可             | -                                                        |
    | MySQL      | SQL Server | 不可             | -                                                        |
    | MySQL      | PostgreSQL | 不可             | -                                                        |

1.  格納可能な最大文字数の違い等、DB毎の仕様の違いにより、データ移行中にエラーが生じる可能性がございます。本手順を本番環境で実施いただく前にリハーサルを実施し、エラーデータの有無やリカバリ手順を確認した上で、本番環境の作業を実施してください。
1.  数百メガバイト単位の添付ファイル等の大容量データは、移行時処理中にプログラムの許容範囲オーバーでエラーとなる可能性がございます。
1.  数憶文字単位の大容量の文字列データは、移行時処理中にプログラムの許容範囲オーバーでエラーとなる可能性がございます。

## 前提条件

1.  本手順を進めていく中でパラメータファイルに記述するDB接続情報について、移行元DBの情報を[Migration.json](../../parameters/migration-json.md)に、移行先DBの情報を[Rds.json](../../parameters/rds-json.md)に記載します。[Rds.json](../../parameters/rds-json.md)は同じ設定をプリザンターの起動以降も使用します。[Migration.json](../../parameters/migration-json.md)に記載する移行元DBの情報は本手順の移行処理以外では使用しませんので、セキュリティの観点より移行完了後は"SourceConnectionString"をnullに更新してください。

## 事前準備

### 1. 移行元DBの確認

1.  移行元プリザンターが移行先プリザンターと同じバージョンになるように、必要に応じてバージョンアップします。本手順では、移行元DBと移行先DBのテーブル定義を一致させる必要があるため、両者が同一バージョンになるように調整してください。  
   ※移行元プリザンターのバージョンを先行させてしまうと、定義不足によりデータ移行ができなくなりますので、ご遠慮ください。
1.  移行元DBの接続情報はこの後の手順で[Migration.json](../../parameters/migration-json.md)に記載します。必要に応じて移行元DBの[Rds.json](../../parameters/rds-json.md)および[Service.json](../../parameters/service-json.md)の内容を確認してください。
1.  移行元DBが移行先のプリザンターから見て外部のサーバにある場合は、移行元DBに外部からの接続を許可する設定が必要です。必要に応じて設定してください。

### 2. プリザンターのセットアップ（前半部）

セットアップマニュアルの手順を途中まで実施します。

=== "Windowsにインストールする場合"

    -   [インストーラでプリザンターをWindowsにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-windows.md)
    -   [プリザンターをWindowsにインストールする](../../installation/install-manually/getting-started-pleasanter-windows.md)

    上記いずれかの手順でプリザンターを新規セットアップする場合、以下セットアップ手順（途中まで）を行います。

    ??? note "詳細を確認する"

        各マニュアルの先頭から順序通りに、以下チェックリストの手順を実施します。

        __セットアップ手順チェックリスト__

        - [x] 事前準備
        - [x] （インストーラの場合）インストーラのインストール
        - [x] プリザンターのセットアップ

        __「CodeDefinerの実行」「IISのセットアップ」「プリザンターの動作確認」は実施しないでください。__

=== "インストーラでLinuxにインストールする場合"

    -   [インストーラでプリザンターをUbuntuにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-ubuntu.md)
    -   [インストーラでプリザンターをAlmaLinuxにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)
    -   [インストーラでプリザンターをRed Hat Enterprise Linux 8にインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-rhel-8.md)
    -   [インストーラでプリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-rhel9.md)

    上記いずれかの手順でプリザンターを新規セットアップする場合、以下セットアップ手順（途中まで）を行います。

    ??? note "詳細を確認する"

        各マニュアルの先頭から順序通りに、以下チェックリストの手順を実施します。

        __セットアップ手順チェックリスト__

        - [x] .NETのセットアップ
        - [x] データベースのセットアップ
        - [x] インストーラのインストール
        - [x] プリザンターのセットアップの「インストーラの実行」

        __「プリザンターの起動確認」以降は実施しないでください。__

=== "インストーラを使用せずLinuxにインストールする場合"

    -   [プリザンターをUbuntuにインストールする](../../installation/install-manually/getting-started-pleasanter-ubuntu.md)
    -   [プリザンターをAlmaLinuxにインストールする](../../installation/install-manually/getting-started-pleasanter-almalinux.md)
    -   [プリザンターをRed Hat Enterprise Linux 8にインストールする](../../installation/install-manually/getting-started-pleasanter-rhel-8.md)
    -   [プリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../installation/install-manually/getting-started-pleasanter-rhel.md)

    上記いずれかの手順でプリザンターを新規セットアップする場合、以下セットアップ手順（途中まで）を行います。

    ??? note "詳細を確認する"

        各マニュアルの先頭から順序通りに、以下チェックリストの手順を実施します。

        __セットアップ手順チェックリスト__

        - [x] .NETのセットアップ
        - [x] データベースのセットアップ
        - [x] プリザンターのセットアップの「アプリケーションの準備」と「データベースの構成」

        __「CodeDefinerの実行」以降は実施しないでください。__

        </details>

=== "Dockerを使用する場合"

    -   [Dockerイメージを使用しパラメータを既定値から変更して起動する](../../installation/running-with-docker/change-parameters-at-docker-image.md)
    -   [Dockerイメージを使用しDBにMySQLを指定して起動する](../../installation/running-with-docker/setup-by-docker-image-and-mysql.md)

    上記いずれかの手順でプリザンターを新規セットアップする場合、以下セットアップ手順（途中まで）を行います。

    ??? note "詳細を確認する"

    各マニュアルの先頭から順序通りに、以下チェックリストの手順を実施します。

    __セットアップ手順チェックリスト__

    - [x] ファイル配置

    __「コンテナイメージのビルド」以降は実施しないでください。__

## DB移行の流れ

1.  [Migration.json](../../parameters/migration-json.md)の変更
1.  CodeDefinerをmigrateモードで実行
1.  [Migration.json](../../parameters/migration-json.md)の変更
1.  プリザンターのセットアップ（後半部）
1.  （移行がエラーで中止した場合）エラーログの確認

### 1. Migration.jsonの変更

移行元DBの情報等を記載します。
[Migration.json](../../parameters/migration-json.md)のマニュアルを確認の上、バージョンに沿った内容で記載してください。

#### Dockerでプリザンターを起動する場合

[Migration.json](../../parameters/migration-json.md)を含むパラメータファイルの変更後、以下コマンドを実行し、コンテナイメージをビルドします。

``` bash
docker compose build
```

### 2. CodeDefinerをmigrateモードで実行

以下フローチャート結果に応じて、引数`/l`および`/z`の引数の設定有無を確認してください。

#### フローチャート

1.  質問：プリザンターのインストーラを実行しましたか？[^1]
    当てはまる場合は、「2-a. 引数 /l および /z を指定しないコマンド」を実行してください。
1.  質問：インストーラなし、かつ、バージョンver.1.4.6以降ですか？
    当てはまる場合は、「2-b. 引数 /l および /z を指定するコマンド」を実行してください。
1.  それ以外の場合は、「2-a. 引数 /l および /z を指定しないコマンド」を実行してください。

[^1]: Dockerを使用する場合は「インストーラなし」と判断してください。

#### 2-a. 引数 /l および /z を指定しないコマンド

=== "Windowsの場合"

    コマンドプロンプトで以下コマンドを実行します。  

    ``` bat
    cd {Implem.CodeDefinerのパス}
    dotnet Implem.CodeDefiner.dll migrate
    ```

=== "Linuxの場合"

    ターミナルで以下コマンドを実行します。

    ``` bash
    cd {Implem.CodeDefinerのパス}
    sudo -u {Linuxユーザ名} /usr/local/bin/dotnet Implem.CodeDefiner.dll migrate
    ```

=== "Dockerの場合"

    `docker compose run`を実行します。

    ``` bash
    docker compose run --rm codedefiner mingate
    ```

#### 2-b. 引数 /l および /z を指定するコマンド

##### 引数 /l および /z について

以下コマンドは日本語環境をセットアップする例です。

| 引数 | 設定例     | 説明                                                 |
| :--- | :--------- | :--------------------------------------------------- |
| /l   | ja         | Service.jsonのDefaultLanguageの値を書き換えます [^2] |
| /z   | Asia/Tokyo | Service.jsonのTimeZoneDefaultの値を書き換えます [^2] |

[^2]:
    /l に指定する言語、および、/z に指定するタイムゾーンについては、以下マニュアルページを参照ください。
    [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)

=== "Windowsの場合"

    コマンドプロンプトで以下コマンドを実行します。  

    ``` bat
    cd {Implem.CodeDefinerのパス}
    dotnet Implem.CodeDefiner.dll migrate /l "ja" /z "Tokyo Standard Time"
    ```

=== "Linuxの場合"

    ターミナルで以下コマンドを実行します。

    ``` bash
    cd {Implem.CodeDefinerのパス}
    sudo -u {Linuxユーザ名} /usr/local/bin/dotnet Implem.CodeDefiner.dll migrate /l "ja" /z "Asia/Tokyo"
    ```

=== "Dockerの場合"

    `docker compose run`を実行します。

    ``` bash
    docker compose run --rm codedefiner mingate /l "ja" /z "Asia/Tokyo"
    ```

#### 開始時メッセージ

開始時に以下メッセージが表示されます。  
++y++ キー、++enter++ キーの順序で押下し、処理を先に進めてください。

``` text hl_lines="2"
Type "y" (yes) if the license is correct, otherwise type "n" (no).
y
```

#### 移行処理の流れ

処理は2ステップ実行されます。

1.  移行先DBに、Implem.Pleasanterデータベースおよびデータのない空のテーブルを作成する処理
1.  移行元DBから移行先へデータを移行する処理

!!! warning
    データ量およびデータサイズによっては、上記 2. の移行処理が終了するまで時間を要する場合があります。

#### 移行処理の終了

移行が終了すると、画面上のメッセージの末尾に以下が表示されます

``` text
<SUCCESS> Starter.MigrateDatabase: The migration is complete.
<SUCCESS> Starter.Main: All of the processes have been completed
```

メッセージの表示後、以下手順を実施してください。

3\. [Migration.json](../../parameters/migration-json.md)の変更
4\. プリザンターのセットアップ（後半部）

#### 移行処理中のエラー

移行中にエラーが発生すると、画面上のメッセージの末尾に以下が表示されます

-   バージョン1.4.13.0以降かつ[Migration.json](../../parameters/migration-json.md)の"AbortWhenException" = trueの場合

    ``` text
    <ERROR>システムのエラーメッセージ
    ～システムのエラーメッセージの終端

    Abort. Press any key to close.
    ```

-   バージョン1.4.13.0以降かつ[Migration.json](../../parameters/migration-json.md)の"AbortWhenException" = falseの場合

    ``` text
    <ERROR> Starter.MigrateDatabase: The migration process was completed, but some data encountered errors. See {ファイルパス}.
    <ERROR> Starter.Main: There were {<ERROR>の件数} errors. Please check the log file ({ファイルパス}).
    ```

-   バージョン1.4.12.0以前の場合

    ``` text
    <ERROR> Starter.Main: There were {<ERROR>の件数} errors. Please check the log file ({ファイルパス}).
    ```

メッセージの表示後、以下手順を実施してください。

3\. [Migration.json](../../parameters/migration-json.md)の変更
5\. （移行がエラーで中止した場合）エラーログの確認

「4. プリザンターのセットアップ（後半部）」は移行先データベースでプリザンターを起動する手順のため、エラーのリカバリが完了するまで実施しないでください。

### 3. [Migration.json](../../parameters/migration-json.md)の変更

[Migration.json](../../parameters/migration-json.md)の「SourceConnectionString」には移行元DBの接続情報が記載されています。[Migration.json](../../parameters/migration-json.md)は、前述の「2. CodeDefinerをmigrateモードで実行」におけるコマンド実行以外では使用しませんので、実行後すみやかにnullに変更してください。

``` json title="Migration.json"
"SourceConnectionString": null,
```

### 4. プリザンターのセットアップ（後半部）

事前準備「2. プリザンターのセットアップ（前半部）」以降の、セットアップ残手順を最後まで実施します。

=== "Windowsにインストールする場合"

    各マニュアルの最後まで順序通りに、以下チェックリストの手順を実施します。

    **〈セットアップ手順チェックリスト〉**

    □ IISのセットアップ
    □ プリザンターの起動確認

    ※「CodeDefinerの実行」は実施しないでください。

=== "インストーラでLinuxにインストールする場合"

    各マニュアルの最後まで順序通りに、以下チェックリストの手順を実施します。

    **〈セットアップ手順チェックリスト〉**

    □ プリザンターのセットアップの「プリザンターの起動確認」「Pleasanterサービス用スクリプトの作成」「サービスとして登録・サービスの起動」
    □ リバースプロキシ(nginx)のセットアップ
    □ プリザンターの動作確認

=== "インストーラを使用せずLinuxにインストールする場合"

    各マニュアルの最後まで順序通りに、以下チェックリストの手順を実施します。

    **〈セットアップ手順チェックリスト〉**

    □ プリザンターのセットアップの「プリザンターの起動確認」「Pleasanterサービス用スクリプトの作成」「サービスとして登録・サービスの起動」
    □ リバースプロキシ(nginx)のセットアップ
    □ プリザンターの動作確認

    ※「CodeDefinerの実行」は実施しないでください。

=== "Dockerを使用する場合"

    各マニュアルの最後まで順序通りに、以下チェックリストの手順を実施します。

    **〈セットアップ手順チェックリスト〉**

    □ プリザンター起動

    ※「CodeDefinerの実行」は実施しないでください。

### 5. （移行がエラーで中止した場合）エラーログの確認

「2. CodeDefinerをmigrateモードで実行」の後、CodeDefiner標準ログと、エラーデータ一覧ログの2種類、ログファイルが作成されます。

ログファイルの格納先：{Implem.CodeDefinerのパス}/logs

1.  CodeDefiner標準ログファイル：「Implem.CodeDefiner_{年月日}_{時分秒}.log」
1.  エラーデータ一覧ログファイル：「Implem.CodeDefiner_{年月日}_{時分秒}._Migratelog」（バージョン1.4.13.0以降の場合に作成されます）

#### CodeDefiner標準ログファイル

CodeDefinerの実行時に表示されたメッセージと同一のログが記録されます。
バージョン1.4.12.0以前の場合は、CodeDefiner標準ログファイルの内容からエラーが発生したテーブルを判断してください。

#### エラーデータ一覧ログファイル

バージョン1.4.13.0以降の場合に作成されます。
テーブル単位のエラー情報、または、データ単位のエラー情報が記録されます。

##### テーブル単位のエラー

###### 発生原因

主に接続エラーです。外部的な原因や、移行元DBのデータ量が大きくプログラム内で保持しきれなかった場合等に発生します。

###### 例

``` text
[ERROR]    Table:"Binaries"    System.Data.SqlClient.SqlException caught.
```

-   Table：原因のテーブル名  
-   処理中にエラーを検知したテーブルの情報のみ出力します。  
-   エラー発生後、該当テーブル内のデータの移行がスキップされた可能性があります。

__必ず移行前後のテーブル（**_historyと_deletedを含む**）を比較し、状況を確認してください。__

##### データ単位のエラー

###### 発生原因

該当データのINSERT用SQL処理中のエラーです。作業ミスによる一意制約違反や、データサイズが大きすぎる場合等に発生します。

###### 例

``` text
[ERROR]    Table:"Binaries"    Data:"BinaryId"=999, "TenantId"=999, "ReferenceId"=999, "Guid"=ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ, "Ver"=1, "BinaryType"=Attachments, "Title"=Attachment.zip, "Body"=, "Bin"=System.Byte[], "Thumbnail"=, "Icon"=, "FileName"=Attachment.zip, "Extension"=.zip, "Size"=999, "ContentType"=application/x-zip-compressed, "BinarySettings"=, "Comments"=, "Creator"=999, "Updator"=999, "CreatedTime"=2025/01/01 12:00:00.000, "UpdatedTime"=2025/01/01 12:00:00.000
```

-   Table：原因のテーブル名  
-   Data：原因のデータ内容  
-   INSERT用SQL処理でエラーを検知したデータの情報のみ出力します。

__必ず移行前後のテーブル（_historyと_deletedを含む）を比較し、状況を確認してください。__

##### リカバリ手順

1.  ログ内容からエラーが検知されたテーブルを把握
1.  該当テーブル（**_historyと_deletedを含む**）の移行前後のDB内容を比較
1.  移行されなかったデータの確認
1.  リカバリ作業の実施。詳細は、後述のFAQを参照してください。

## FAQ

### Q1

移行対象外のDBの組み合わせを[Migration.json](../../parameters/migration-json.md)および[Rds.json](../../parameters/rds-json.md)に記載することはできないのでしょうか？

---

バージョン1.4.13.0以降、パラメータをチェックするようになったため、指定可能な内容以外を記述した場合はCodeDefinerの起動エラーとなり、DB移行ができません。

Migration.json

-   Dbmsは "SQLServer" のみ指定可能です。
-   Providerは "Local" のみ指定可能です。

Rds.json

-   Dbmsは "PostgreSQL"、"MySQL" のいずれかのみ指定可能です。
-   Providerは "Local" のみ指定可能です。

バージョン1.4.12.0以前の場合、SQL ServerからPostgreSQLへ移行する組み合わせ以外は想定されていません。万が一各パラメータファイルの接続情報に対象外のDBの情報を記述して実行した場合、システムが想定していないエラーの原因になりますので、ご遠慮ください。

### Q2

DBへの接続エラーとみられるエラーを検知しました。設定に問題があるのでしょうか？

---

以下の原因が考えられます。

1.  移行先DBに関する[Rds.json](../../parameters/rds-json.md)のミス
1.  移行先DBの設定ミス（外部参照設定やファイアウォール等）
1.  移行元DBに関する[Migration.json](../../parameters/migration-json.md)のミス
1.  移行元DBの設定ミス（外部参照設定やファイアウォール等）

上記1. および2. は、CodeDefinerの処理開始直後に検知されます。  
上記3. および4. は、移行先DBの設定に問題がない場合、Implem.Pleasanterサービス作成処理の終了後、移行処理の開始時に検知されます。

移行前後のどちらのDBへの接続でエラーになったか、上記の基準で判断の上、設定を見直してください。

### Q3

移行先DBへのImplem.Pleasanterサービス作成処理までは正常に実行されましたが、データ移行処理の最初に接続エラーで終了しました。移行元DBの接続情報を修正して再度移行処理を行う際、移行先DBに作成されたImplem.Pleasanterは削除が必要ですか？

---

削除は不要です。

「2. CodeDefinerをmigrateモードで実行」と同じコマンドを再実行してください。前回作成された空のImplem.Pleasanterサービスをそのまま使用し、移行します。  
「Type "y" (yes) if the license is correct, otherwise type "n" (no).」の確認メッセージが表示された際も、同様に「y」「Enter」キーを押下してください。

### Q4

移行に失敗したデータの修復方法を教えてください。（移行元DBで原因データを修正し、全移行処理をやり直す場合）

---

エラーデータの件数が多い場合に有効です。

1.  移行前後のDB内容を比較し（_historyと_deletedを含む）、移行されなかったデータを確認
1.  移行されなかったデータについて、移行前DBの各カラム内容を確認
1.  CodeDefiner標準ログに出力されたメッセージや、移行先DBの列定義と上記2. の内容を比較して、前回INSERT処理のエラー原因を判断
1.  移行前DBにおいて、移行エラーになったデータの原因箇所をすべて修正 [^3]
1.  移行先DBにデータベースクライアントを使用して接続し、DROP DATABASE文でImplem.Pleasanterサービスを削除
1.  本マニュアルの移行手順を再実施

[^5]: データベースクライアントを使用しUPDATE文を実行する方法、または、プリザンターを起動して修正する方法の2通りがある。文章形式のデータはUPDATE文で修正して問題ないケースが多いが、JSON形式やバイナリファイルはプリザンター上で修正することが望ましい。

### Q5

移行に失敗したデータの修復方法を教えてください。（移行後DBを維持したまま、移行に失敗したデータをひとつずつ登録する場合）

---

エラーデータの件数が少ない場合に有効です。

1.  移行前後のDB内容を比較し（_historyと_deletedを含む）、移行されなかったデータを確認
1.  移行されなかったデータについて、移行前DBの各カラム内容を確認
1.  CodeDefiner標準ログに出力されたメッセージや、移行先DBの列定義と上記2. の内容を比較して、前回INSERT処理のエラー原因を判断
1.  INSERT文を記述。その際、上記3. で確認したエラー原因の値を修正
1.  移行先DBにデータベースクライアントを使用して接続し、上記4. で記述したINSERT文を実行
1.  移行が必要なすべてのデータについて2. ～5.を実施

### Q6

MySQLへの移行処理中に以下エラーメッセージが表示されました。「max_allowed_packet」の数値は変更できますか？

```
MySqlConnector.MySqlException (0x80004005): Error submitting 100MB packet; ensure 'max_allowed_packet' is greater than 100MB.
```

`100MB` の部分は環境により異なります。

---

MySQLサーバの「max_allowed_packet」の数値を大きく設定することで、エラーが解消される可能性がございます。[^4]

[^4]: 参考：[MySQL :: MySQL 8.4 Reference Manual :: B.3.2.8 Packet Too Large](https://dev.mysql.com/doc/refman/8.4/en/packet-too-large.html)

「max_allowed_packet」が記述されているMySQL設定ファイルの配備先は環境によって異なります。
MySQL設定ファイルの修正後は、MySQLのサービス再起動を実施してください。

### Q7

ログのエラーデータ一覧に表示されていない内容があるようです。ログファイルに問題がありますか？

---

ログファイル出力の仕様により、1024文字を超えるデータの超過分やJSON形式のデータは、ログファイルに出力されません。移行元データの正確な内容は、データベースクライアントソフトや、データベースクライアントのコマンドを使用して確認してください。

## 対応バージョン

| 対応バージョン | 内容                                                               |
| :------------- | :----------------------------------------------------------------- |
| -              | プリザンターのDBをSQL ServerからPostgreSQLへ移行する機能の初期公開 |
| 1.4.13.0 以降  | プリザンターのDBをSQL ServerからMySQLに移行する機能の追加          |

## 関連項目

-   [CodeDefiner](../../../FAQ/system-requirements-and-setup/faq-codedefiner-about.md)
-   [異なる環境にプリザンターのデータベース(SQL Server)を移行する手順](migrate-to-other-environment-pleasanter-net5.md)
-   [FAQ：PostgreSQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-postgresql-backup-restore.md)
-   [FAQ：MySQL データベース バックアップ・リストア手順](../../../FAQ/backup-restore/faq-mysql-backup-restore.md)
-   [パラメータ設定：Migration.json](../../parameters/migration-json.md)
-   [パラメータ設定：Rds.json](../../parameters/rds-json.md)
-   [パラメータ設定：Service.json](../../parameters/service-json.md)
-   [インストーラでプリザンターをWindowsにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-windows.md)
-   [プリザンターをWindowsにインストールする](../../installation/install-manually/getting-started-pleasanter-windows.md)
-   [インストーラでプリザンターをUbuntuにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-ubuntu.md)
-   [インストーラでプリザンターをAlmaLinuxにインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)
-   [インストーラでプリザンターをRed Hat Enterprise Linux 8にインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-rhel-8.md)
-   [インストーラでプリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../installation/install-with-installer/getting-started-installer-pleasanter-rhel9.md)
-   [プリザンターをUbuntuにインストールする](../../installation/install-manually/getting-started-pleasanter-ubuntu.md)
-   [プリザンターをAlmaLinuxにインストールする](../../installation/install-manually/getting-started-pleasanter-almalinux.md)
-   [プリザンターをRed Hat Enterprise Linux 8にインストールする](../../installation/install-manually/getting-started-pleasanter-rhel-8.md)
-   [プリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../installation/install-manually/getting-started-pleasanter-rhel.md)
-   [Dockerイメージを使用しパラメータを既定値から変更して起動する](../../installation/running-with-docker/change-parameters-at-docker-image.md)
-   [Dockerイメージを使用しDBにMySQLを指定して起動する](../../installation/running-with-docker/setup-by-docker-image-and-mysql.md)
-   [FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](../../../FAQ/system-requirements-and-setup/faq-supported-language.md)
-   [MySQL :: MySQL 8.4 Reference Manual :: B.3.2.8 Packet Too Large](https://dev.mysql.com/doc/refman/8.4/en/packet-too-large.html)
