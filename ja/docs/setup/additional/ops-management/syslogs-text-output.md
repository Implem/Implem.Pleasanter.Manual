---
title: システムログをテキスト出力できるようにする
category: 追加設定：運用管理
order: '100'
status: ''
parts: ''
urlstring: syslogs-text-output
translationKey: syslogs-text-output
shortname: システムログのテキスト出力
created: 2024-11-01
updated: 2024-12-10
---

## 概要

プリザンターのシステムログをテキスト出力する方法について説明します。

## 手順

### パラメータ変更

システムログをテキスト出力するには、パラメータ設定を編集して機能を有効にします。

1. App_Data/Parameters/SysLog.jsonを開きます。
1. 「EnableLoggingToFile」パラメータを「true」に設定します。
1. プリザンターを再起動します。

パラメータの指定方法につきましては、[SysLog.json](../../parameters/sys-log-json.md)を確認してください。

### ログ出力の詳細設定

システムログの出力機能そのものは NLog を利用しています。  
出力先や内容は appsettings.json で設定します。

大まかな構成はこのようになっています。

```json
{
  "Logging": {
    "LogLevel": {
      // ... 省略
    }
  },
  "NLog": {
    "target": {
      "jsonfile": {
        "type": "File",
        "fileName": "logs/${パス}/syslogs.json",
        "layout": {
          "type": "JsonLayout",
          "Attributes": [
              // ... 省略
          ]
        }
      },
      "csvfile": {
        "type": "File",
        "fileName": "logs/${パス}/syslogs.csv",
        "layout": {
            "type": "CsvLayout",
            "columns": [
                // ... 省略
            ]
        }
      }
    },
    "rules": [
      {
        "logger": "syslogs",
        "minLevel": "Info",
        "writeTo": "csvfile"
      }
    ]
  }
}
```

| 項目名 |設定例| 説明 |
|:--|:--|:--|
|Logging|省略|ASP.NET Core のログ出力レベルの設定です。|
|NLog|省略|NLog の設定です。|
|NLog.target|省略|出力先の設定を複数定義できます。 ※1|
|NLog.target.jsonfile|省略|JSON形式で出力する設定です。|
|NLog.target.jsonfile.fileName|logs/${パス}/syslogs.json|出力先のパスやファイル名を指定します。|
|NLog.target.jsonfile.layout|省略|出力する項目を指定します。 ※2|
|NLog.target.csvfile|省略|CSV形式で出力する設定です。|
|NLog.target.csvfile.fileName|logs/${パス}/syslogs.csv|出力先のパスやファイル名を指定します。|
|NLog.target.csvfile.layout|省略|出力する項目を指定します。|
|NLog.rules|省略|ログの出力先を指定します。|
|NLog.rules.logger|syslogs| "syslogs"がシスログの出力用の定義です。|
|NLog.rules.minLevel|Info|出力するログレベルを指定します。|
|NLog.rules.writeTo|csvfile|出力先を指定します。デフォルトではCSV形式になっています。|

-   ※1: [Targets \| NLog](https://nlog-project.org/config/?tab=targets)
-   "fileName" : 相対パスの場合は "App_Data" と同じ階層が基準になります。
-   ※2: [Layouts \| NLog](https://nlog-project.org/config/?tab=layouts)

    -   [CsvLayout · NLog/NLog Wiki](https://github.com/NLog/NLog/wiki/CsvLayout)
    -   [JsonLayout · NLog/NLog Wiki](https://github.com/NLog/NLog/wiki/JsonLayout)

### 出力項目の設定

ここでは "layout" について説明します。  
"type" ごとに定義の仕方が異なりますが、デフォルトではJSON形式とCSV形式を定義しています。

### 共通

CSV形式とJSON形式の両方で出力する項目は共通です。
また、SysLogsテーブルの内容の前にテキスト形式に固有の項目が出力されます。

-   timestamp  ‥ ログ出力時の日時です。(CreatedTimeではありません。出力しないことも可能です)
-   level    ‥ ログのレベルです。SysLogsテーブルのSysLogTypeと同じ意味のレベルです。
-   message  ‥ ログの内容です。システムログの場合は2種類のメッセージが出力されます。

    -   WriteSysLog  ‥ DBの挿入タイミングで出力されます。
    -   UpdateSysLog ‥ DBの更新タイミングで出力されます。
    -   2行でDBのシステムログ1レコードに対応します。SysLogIdが同じです。

### CSV形式

システムログの[SysLogsテーブル](../../../FAQ/operations-and-maintenance/faq-contents-of-syslogs.md)の内容がCSV形式で出力されます。  

```text
"timestamp","level","message","CreatedTime","SysLogId",...,"Updator","UpdatedTime"
"2024-...","INFO","WriteSysLog","2024-...",9999,...,0,"日時"
```

1件のシステムログは改行されずに1行で出力されます。

### JSON形式

システムログの[SysLogsテーブル](../../../FAQ/operations-and-maintenance/faq-contents-of-syslogs.md)の内容がJSON形式で出力されます。  

```json
{ "timestamp": "2024-...",..., "syslog": { "syslog": {"CreatedTime":"...", "SysLogId":999, ... "Updator":0, "UpdatedTime":"日時"} } }
{ ... }
{ ... }
```

-   1件のシステムログは改行されずに1行で出力されます。
-   "syslog" は SysLogsテーブルの内容がそのままJSON形式に変換されて出力されます。

項目の詳細につきましては、[FAQ：システムログ(SysLogsテーブル)の内容について](../../../FAQ/operations-and-maintenance/faq-contents-of-syslogs.md)を参照してください。

## 関連情報

-   [パラメータ設定：SysLog.json](../../parameters/sys-log-json.md)
-   [Targets \| NLog](https://nlog-project.org/config/?tab=targets)
-   [Layouts \| NLog](https://nlog-project.org/config/?tab=layouts)
-   [CsvLayout · NLog/NLog Wiki](https://github.com/NLog/NLog/wiki/CsvLayout)
-   [JsonLayout · NLog/NLog Wiki](https://github.com/NLog/NLog/wiki/JsonLayout)
-   [FAQ：システムログ(SysLogsテーブル)の内容について](../../../FAQ/operations-and-maintenance/faq-contents-of-syslogs.md)
