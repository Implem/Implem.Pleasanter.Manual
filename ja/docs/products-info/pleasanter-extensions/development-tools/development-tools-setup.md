---
title: セットアップ、起動方法
category: 開発支援ツール
order: '2000'
status: ''
parts: ''
urlstring: development-tools-setup
translationKey: development-tools-setup
shortname: Pleasanter Extensions,Development Tools,セットアップ,起動方法,Settings.json
created: 2025-01-27
updated: 2025-02-14
---

## 概要

[Development Tools](development-tools-convert-sitesettings.md)のセットアップおよび起動手順を説明します。

## セットアップ / 起動手順

1. 本ソフトウェアのモジュールをPC内の任意のディレクトリにコピーします。
1. サポートWebにアクセスしサポートID管理のテーブルから Enterprise Edition License Pack をダウンロードして解凍します。
1. コピー先の Implem.License.dll をEnterprise Edition License Pack の forNetCore フォルダ内にある Implem.License.dll で上書きコピーします。
1. コピー先の Settings.json を編集し接続先のデータベースおよびローカルPC内のソースコードのパス等を指定します。
1. コピー先の Implem.PleasanterManagementStudio.exe を実行すると起動します。

## Settings.json の設定内容

環境に合わせて内容を編集してください。編集後は Implem.PleasanterManagementStudio を再起動してください。各要素の説明は下記のとおりです。同梱されている Settings.json はサンプルです。

### ルート要素

|No|要素|内容|
|:----|:----|:----|
|1|Environments|接続先のデータベース環境 Environment 要素を定義します。|

### Environment要素

|No|要素|内容|
|:----|:----|:----|
|1|Name|任意のユニークな識別名を指定します。|
|2|TenantId|1 を指定します。|
|3|UserId|データベースに書き込む際のユーザIDを指定します。|
|4|Title|環境の名称を指定します。|
|5|Dbms|SQLServer または PostgreSQL を指定します。|
|6|ConnectionString|Pleasanterのデータベースにdbowner権限で接続するための接続文字列を指定します。Serverの指定は本ツールを利用する端末からアクセス可能な内容（ホスト名またはIPアドレス）で指定してください。DB、UID、PWDは接続するプリザンターの設定内容を指定してください。デフォルト設定の場合、DBはImplem.Pleasanter、UIDはImplem.Pleasanter_Ownerです。その他のキーワードはRds.jsonを参考に接続するデータベースに合わせて適宜設定してください。|
|7|TimeZone|Azure SQL DatabaseなどUTC環境の場合には UTC を指定します。|
|8|DestinationName|サイト設定の移行機能を使用する際の移行先の Environment の Name を指定します。|
|9|DisableConvert|サイトIDやユーザIDのコンバートを行わず SiteSettings をそのまま移行する場合は true を指定します。|
|10|TargetSites|サイト設定の移行機能を使用する際の移行元のサイト情報 TargetSite 要素を定義します。|
|11|BasePath|ソースコードのアップロード機能を使用する際の起点となるディレクトリのパスを指定します。|
|12|Codes|ソースコードのアップロード機能を使用する際のソースコードのパスやアップロード先のサイト情報を含む Code 要素を指定します。|
|13|Extensions|ソースコードのアップロード機能を使用する際のソースコードのパスや拡張機能の設定情報を含む Extension 要素を指定します。|
|14|UserSqls|任意のSQLを記述したUserSQLファイルのパスを指定します。|

### TargetSite要素

|No|要素|内容|
|:----|:----|:----|
|1|SourceId|移行元のサイトIDを指定します。|
|2|DestinationId|移行先のサイトIDを指定します。省略した場合、新規に作成され、その後は移行先に作成された _Converted テーブルの情報をもとに移行先のサイトIDを自動識別します。|
|3|Subtree|true を設定すると配下のフォルダ、テーブルを全て移行します。|

### Code要素

|No|要素|内容|
|:----|:----|:----|
|1|SiteId|コードのアップロード先のサイトIDを指定します。|
|2|Id|コードのIdを指定します。テーブルの管理に既に存在する場合には上書きし、存在しない場合には追加します。|
|3|Title|コードのタイトルを指定します。|
|4|Type|コードの種類（Scripts / ServerScripts / Styles）を指定します。|
|5|Path|コードのパスをBasePath配下のパスで指定します。|

### Extension要素

|No|要素|内容|
|:----|:----|:----|
|1|ExtensionId|Extensions テーブルの ExtensionId を指定します。既に存在する場合には上書きし、存在しない場合には追加します。|
|2|ExtensionName|Extensions テーブルの ExtensionName を指定します。|
|3|ExtensionType|コードの種類（Script / ServerScript / Sql / Style）を指定します。|
|4|Path|コードのパスをBasePath配下のパスで指定します。|

### UsersSQL要素

|No|要素|内容|
|:----|:----|:----|
|1|Path|UserSQLファイルのパスをBasePath配下のパスで指定します。|
|2|Description|SQLの説明を記述します。|

## Settings.jsonサンプル

開発環境サーバのIPアドレスが「192.168.1.10」、本番環境サーバのIPが「192.168.1.20」の例です

``` json
{
    "Environments": [
        {
            "Name": "Development",
            "TenantId": 1,
            "UserId": 1,
            "Title": "開発環境",
            "Dbms": "SQLServer",
            "ConnectionString": "Server=192.168.1.10;Database=Implem.Pleasanter;UID=Implem.Pleasanter_Owner;PWD=SetAdminsPWD;Connection Timeout=30;",
            "TimeZone": null,
            "DestinationName": "Production",
            "DisableConvert": false,
            "TargetSites": [
                {
                    "SourceId": 1
                },
                {
                    "SourceId": 2
                },
                {
                    "SourceId": 3
                },
                {
                    "SourceId": 4
                }
            ],
            "BasePath": "C:\\Implem\\PleasanterExtensions\\Implem.PleasanterManagementStudio",
            "Codes": [
                {
                    "SiteId": 2,
                    "Id": 1,
                    "Title": "サンプルスクリプト1",
                    "Type": "Scripts",
                    "Path": "Samples\\Codes\\Scripts\\Script1.js"
                },
                {
                    "SiteId": 2,
                    "Id": 2,
                    "Title": "サンプルスクリプト2",
                    "Type": "Scripts",
                    "Path": "Samples\\Codes\\Scripts\\Script2.js"
                },
                {
                    "SiteId": 2,
                    "Id": 1,
                    "Title": "サンプルサーバスクリプト1",
                    "Type": "ServerScripts",
                    "Path": "Samples\\Codes\\ServerScripts\\ServerScript1.js"
                },
                {
                    "SiteId": 2,
                    "Id": 2,
                    "Title": "サンプルサーバスクリプト2",
                    "Type": "ServerScripts",
                    "Path": "Samples\\Codes\\ServerScripts\\ServerScript2.js"
                },
                {
                    "SiteId": 2,
                    "Id": 1,
                    "Title": "サンプルスタイル1",
                    "Type": "Styles",
                    "Path": "Samples\\Codes\\Styles\\Style1.css"
                },
                {
                    "SiteId": 2,
                    "Id": 2,
                    "Title": "サンプルスタイル2",
                    "Type": "Styles",
                    "Path": "Samples\\Codes\\Styles\\Style2.css"
                }
            ],
            "Extensions": [
                {
                    "ExtensionId": 1,
                    "ExtensionName": "サンプル拡張スクリプト1",
                    "ExtensionType": "Script",
                    "Path": "Samples\\Extensions\\Scripts\\Script1.json.js"
                },
                {
                    "ExtensionId": 2,
                    "ExtensionName": "サンプル拡張スクリプト2",
                    "ExtensionType": "Script",
                    "Path": "Samples\\Extensions\\Scripts\\Script2.json.js"
                },
                {
                    "ExtensionId": 3,
                    "ExtensionName": "サンプル拡張サーバスクリプト1",
                    "ExtensionType": "ServerScript",
                    "Path": "Samples\\Extensions\\ServerScripts\\ServerScript1.json.js"
                },
                {
                    "ExtensionId": 4,
                    "ExtensionName": "サンプル拡張サーバスクリプト2",
                    "ExtensionType": "ServerScript",
                    "Path": "Samples\\Extensions\\ServerScripts\\ServerScript2.json.js"
                },
                {
                    "ExtensionId": 5,
                    "ExtensionName": "サンプル拡張SQL1",
                    "ExtensionType": "Sql",
                    "Path": "Samples\\Extensions\\Sqls\\Sql1.json.sql"
                },
                {
                    "ExtensionId": 6,
                    "ExtensionName": "サンプル拡張SQL2",
                    "ExtensionType": "Sql",
                    "Path": "Samples\\Extensions\\Sqls\\Sql2.json.sql"
                },
                {
                    "ExtensionId": 7,
                    "ExtensionName": "サンプル拡張スタイル1",
                    "ExtensionType": "Style",
                    "Path": "Samples\\Extensions\\Styles\\Style1.json.css"
                },
                {
                    "ExtensionId": 8,
                    "ExtensionName": "サンプル拡張スタイル2",
                    "ExtensionType": "Style",
                    "Path": "Samples\\Extensions\\Styles\\Style2.json.css"
                }
            ],
            "UserSqls": [
                {
                    "Path": "Samples\\UserSqls\\OutgoingMails.sql"
                },
                {
                    "Path": "Samples\\UserSqls\\SysLogs.sql"
                }
            ]
        },
        {
            "Name": "Production",
            "TenantId": 1,
            "UserId": 1,
            "Title": "本番環境",
            "Dbms": "PostgreSQL",
            "ConnectionString": "Server=192.168.1.20;Database=Implem.Pleasanter;UID=Implem.Pleasanter_Owner;PWD=SetAdminsPWD;",
            "TimeZone": null
        }
    ]
}
```

## 関連情報

-   [Development Tools：サイト設定の移行](development-tools-convert-sitesettings.md)
