---
title: Migration.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: Migration-json
translationKey: Migration-json
shortname: Migration.json
created: 2023-09-14
updated: 2026-02-24
---

## 概要

[CodeDefiner](../../FAQ/system-requirements-and-setup/faq-codedefiner-about.md)を使用して異なる種類のDBにプリザンターのデータを移行する際、移行元DBの設定を記述します。なお、移行先DBの設定は、Migration.jsonではなく[Rds.json](rds-json.md)に記述します。

移行全般に関する詳細は、以下手順を確認してください。

-   [異なる種類のDBにプリザンターのデータを移行する手順](../version-up-migration/migration/migrate.md)

※"SourceConnectionString"は接続文字列を記載するパラメータです。DBの移行処理以外では使用しませんので、安全のため通常はnullを設定してください。  
※プリザンターのバージョンによってMigration.jsonの仕様は異なります。本マニュアルの該当バージョンの記述をご覧ください。

**<span class="pl-attention">移行先プリザンターが1.5以降で、移行元DBにSQL Serverを使用する場合は、必ず以下のマニュアルを確認してください。</span>**  
**[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../installation/prerequisites/sqlserver-connection-string-v15.md)**

---

# バージョン1.4.13.0以降のMigration.json

## 制限事項

1. 下表のとおり、移行可能なデータベースの種類に制限がございます。

|移行元|移行先|本手順の使用可否|備考|
|:--|:--|:--|:--|
|SQL Server|PostgreSQL|可| - |
|SQL Server|MySQL|可| バージョン1.4.12.0以前のプリザンターでは、移行できません |
|PostgreSQL|SQL Server|不可| - |
|PostgreSQL|MySQL|不可| - |
|MySQL|SQL Server|不可| - |
|MySQL|PostgreSQL|不可| - |

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Dbms|"SQLServer"|移行元のDBを指定。"SQL Server"のみ指定可能|
|Provider|"Local"|"Local"のみ指定可能|
|ServiceName|"Implem.Pleasanter"|移行元のDB名を指定|
|SourceConnectionString|"Server=(local);Database=#OldServiceName#;UID=sa;PWD=<saのパスワード>;"|〈テンプレート〉 ※1 ※2<br>"Server={移行元DBの接続先};Database=#OldServiceName#;UID={移行元DBのユーザ};PWD={パスワード};"<br>|
|ExcludeTables|["SysLogs"]|移行対象外とするテーブルを配列形式で設定します。<br>以下テーブルが移行対象外となります。<br>・{テーブル名}<br>・{テーブル名}_history<br>・{テーブル名}_deleted|
|AbortWhenException|true|以下「移行先処理中にエラーが発生した際の動作（バージョン1.4.13.0以降）」を参照|

※1 {移行元DBのユーザ}は移行元DBの参照権限が必要です。
※2 #OldServiceName#は"ServiceName"を置き換えるプレースホルダーです。  

なお、開発環境などTLSサーバ証明書が設定されていないSQL Serverを移行元DBとして使用する場合、SourceConnectionStringの末尾へ**TrustServerCertificate=True;**を追加してください。  
詳細は[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../installation/prerequisites/sqlserver-connection-string-v15.md)を確認してください。  

## 移行先処理中にエラーが発生した際の動作（バージョン1.4.13.0以降）

### AbortWhenException = trueの場合

移行処理を即座に中止します。

例：

``` text
テーブル1.データ1 = 移行成功
テーブル1.データ2 = 移行成功
テーブル1.データ3 = 移行エラー
テーブル1.データ4           → 移行しない。

テーブル2.データ5           → 移行しない。
テーブル2.データ6           → 移行しない。
```
データ3の移行エラーを検知すると、移行処理を即座に中止します。データ1、2は移行先DBに登録されますが、データ4以降のすべてのデータは移行されません。

### AbortWhenException = falseの場合

エラーデータの移行をスキップして移行を継続します。

例：

``` text
テーブル1.データ1 = 移行成功
テーブル1.データ2 = 移行成功
テーブル1.データ3 = 移行エラー
テーブル1.データ4           → 移行処理を継続。

テーブル2.データ5           → 移行処理を継続。
テーブル2.データ6           → 移行処理を継続。
```
データ3の移行エラーを検知すると、データ3の移行をスキップします。その後データ4、データ5、データ6・・・の移行処理を再開し、最後のデータまで移行対象となります。

---

# バージョン1.4.12.0以前のMigration.json

## 制限事項

1. 下表のとおり、移行可能なデータベースの種類に制限がございます。

|移行元|移行先|本手順の使用可否|備考|
|:--|:--|:--|:--|
|SQL Server|PostgreSQL|可| - |
|SQL Server|MySQL|不可| バージョン1.4.12.0以前のプリザンターでは、移行できません |
|PostgreSQL|SQL Server|不可| - |
|PostgreSQL|MySQL|不可| - |
|MySQL|SQL Server|不可| - |
|MySQL|PostgreSQL|不可| - |

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|SourceConnectionString|"Server=(local);Database=Implem.Pleasanter;UID=sa;PWD=<saのパスワード>;"|〈テンプレート〉 ※1<br>"Server={移行元DBの接続先};Database={移行元DB名};UID={移行元DBのユーザ};PWD={パスワード};"|
|ExcludeTables|["SysLogs"]|移行対象外とするテーブルを配列形式で設定します。<br>以下テーブルが移行対象外となります。<br>・{テーブル名}<br>・{テーブル名}_history<br>・{テーブル名}_deleted|

※1 {移行元DBのユーザ}は移行元DBの参照権限が必要です。  

なお、開発環境などTLSサーバ証明書が設定されていないSQL Serverを移行元DBとして使用する場合、SourceConnectionStringの末尾へ**TrustServerCertificate=True;**を追加してください。  
詳細は[プリザンター1.5以降でDBにSQL Serverを使用する際の接続文字列についての注意事項](../installation/prerequisites/sqlserver-connection-string-v15.md)を確認してください。  

## 移行先処理中にエラーが発生した際の動作（バージョン1.4.12.0以前）

移行エラーを検知した場合は、該当テーブル（_history、_deletedを含む）のそれ以降のデータに対する処理がスキップされ、次のテーブルの先頭からデータの移行処理を再開します。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.13.0 以降|Dbmsを追加<br>Providerを追加<br>ServiceNameを追加<br>AbortWhenExceptionを追加<br>SourceConnectionStringの既定値をnullに変更<br>|

## 関連情報

[異なる種類のDBにプリザンターのデータを移行する手順](../version-up-migration/migration/migrate.md)
