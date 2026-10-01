---
title: 拒否ログ・メトリクスの出力先設定
category: 追加設定：パフォーマンス
order: '0'
status: ''
parts: ''
urlstring: ratelimit-metrics
translationKey: ratelimit-metrics
shortname: 拒否ログ・メトリクスの出力先設定
created: 2026-07-10
updated: 2026-07-14
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/02cb2ba6edab487db830646961d907d9.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/d2da9a205bd44c6288b5e4badf32d3e4.svg#only-dark)](https://pleasanter.org/support/)

（本機能は[Extensionsトライアル](../../../products-info/extensions-trial/index.md)で試用可能です）

## 概要

レートリミットの拒否ログおよびメトリクススナップショットの出力先を設定する方法について説明します。機能全体の概要・動作モードについては「[レートリミット機能](ratelimit.md)」を、閾値調整の考え方については「[レートリミット機能：ポリシーと閾値の調整](ratelimit-policy-threshold-setting.md)」を参照してください。

レートリミットのログ出力機能はNLogを利用しています。出力先や出力形式はappsettings.jsonのNLogセクションで設定します。

標準設定では、拒否ログおよびメトリクススナップショットはファイルに出力されます。Dockerなどで、標準出力（stdout）をログ収集基盤で収集する環境では、必要に応じてstdout出力を有効化できます。

## 出力されるログ

レートリミットでは、次の2種類のログを扱います。

|ロガー|内容|既定の出力先|備考|
|:--|:--|:--|:--|
|ratelimitlogs|拒否ログの詳細|File|IP、ログインID、ユーザーID、テナントID、リクエストパスなどを含む場合があります。|
|ratelimitmetrics|拒否件数の集計スナップショット|File|ポリシー名、パーティション種別、モード別の件数です。詳細な個人識別情報は含みません。|

ratelimitmetricsは、LogOnlyで実測してからOnに切り替える際の件数確認に利用できます（詳細は「[レートリミット機能：ポリシーと閾値の調整](ratelimit-policy-threshold-setting.md)」を参照してください）。

## レートリミット機能の有効化

レートリミットのログおよびメトリクスは、[RateLimit.json](../../parameters/ratelimit-json.md)で対象ポリシーのモードがLogOnlyまたはOnの場合に出力されます。

1. [RateLimit.json](../../parameters/ratelimit-json.md)を開いてください。
1. 対象ポリシーのModeを、LogOnlyまたはOnに設定してください。
1. プリザンターを再起動してください。

対象ポリシーのModeがOffの場合、appsettings.jsonのNLog設定を行っていても、レートリミットのログおよびメトリクスは出力されません。

## 設定ファイル

出力先の設定はappsettings.jsonのNLogセクションで行います。

## 標準設定：Fileのみ

標準設定では、stdoutには出力せず、ファイルにのみ出力します。

```json
{
  "NLog": {
    "rules": [
      {
        "logger": "console",
        "minLevel": "Info",
        "writeTo": "logconsole"
      },
      {
        "logger": "syslogs",
        "minLevel": "Info",
        "writeTo": "csvfile"
      },
      {
        "logger": "mcplogs",
        "minLevel": "Info",
        "writeTo": "mcplogsfile"
      },
      {
        "logger": "ratelimitlogs",
        "minLevel": "Warn",
        "writeTo": "ratelimitlogsfile"
      },
      {
        "logger": "ratelimitmetrics",
        "minLevel": "Info",
        "writeTo": "ratelimitlogsfile"
      }
    ]
  }
}
```

この設定では、次のファイルに出力されます。

```text
logs/{yyyy}/{MM}/{dd}/ratelimitlogs.json
```

## stdout 出力用ターゲット

stdoutに出力する場合は、NLog.targetsにConsole targetを追加します。ファイル出力と同じJSON形式にするため、ratelimitlogsfileと同じ形のlayoutを指定します。

```json
{
  "NLog": {
    "targets": {
      "ratelimitlogsconsole": {
        "type": "AsyncWrapper",
        "target": {
          "type": "Console",
          "detectConsoleAvailable": true,
          "writeBuffer": true,
          "layout": {
            "type": "JsonLayout",
            "Attributes": [
              {
                "name": "timestamp",
                "layout": "${date:format=O}"
              },
              {
                "name": "level",
                "layout": "${level:upperCase=true}"
              },
              {
                "name": "message",
                "layout": "${message}"
              },
              {
                "name": "ratelimitlog",
                "encode": false,
                "layout": {
                  "type": "JsonLayout",
                  "includeEventProperties": "true"
                }
              },
              {
                "name": "exception",
                "encode": false,
                "layout": {
                  "type": "jsonLayout",
                  "Attributes": [
                    {
                      "name": "type",
                      "layout": "${exception:format=type}"
                    },
                    {
                      "name": "message",
                      "layout": "${exception:format=message}"
                    },
                    {
                      "name": "stacktrace",
                      "layout": "${exception:format=tostring}"
                    }
                  ]
                }
              }
            ]
          }
        }
      }
    }
  }
}
```

## 設定例1：件数だけstdoutに出力する

外部のログ収集基盤には件数のみを送り、IPやログインIDなどを含む詳細ログはファイルにのみ残す設定です。

```json
{
  "NLog": {
    "rules": [
      {
        "logger": "console",
        "minLevel": "Info",
        "writeTo": "logconsole"
      },
      {
        "logger": "syslogs",
        "minLevel": "Info",
        "writeTo": "csvfile"
      },
      {
        "logger": "mcplogs",
        "minLevel": "Info",
        "writeTo": "mcplogsfile"
      },
      {
        "logger": "ratelimitlogs",
        "minLevel": "Warn",
        "writeTo": "ratelimitlogsfile"
      },
      {
        "logger": "ratelimitmetrics",
        "minLevel": "Info",
        "writeTo": "ratelimitlogsfile,ratelimitlogsconsole"
      }
    ]
  }
}
```

この設定では、stdoutに出力されるのはRateLimitMetricsSnapshotのみです。

出力例:

```json
{"timestamp":"2026-07-09T14:03:00.0000000Z","level":"INFO","message":"RateLimitMetricsSnapshot","ratelimitlog":{"EventType":"RateLimitMetricsSnapshot","WindowStartedAt":"2026-07-09T14:02:00.0000000Z","WindowEndedAt":"2026-07-09T14:03:00.0000000Z","Counts":{"GlobalLimiter_ip_On":18452,"PublicForm_ip_On":211,"General_user_On":37}}}
```

Countsのキーは「ポリシー名\_パーティション種別\_モード（\_区切り）です。NLogのJSON出力仕様上、キーに「\|」などの記号は使えないため「\_」を区切り文字としています。

## 設定例2：拒否ログ詳細と件数をstdoutに出力する

拒否ログの詳細も外部のログ収集基盤へ送る設定です。

```json
{
  "NLog": {
    "rules": [
      {
        "logger": "console",
        "minLevel": "Info",
        "writeTo": "logconsole"
      },
      {
        "logger": "syslogs",
        "minLevel": "Info",
        "writeTo": "csvfile"
      },
      {
        "logger": "mcplogs",
        "minLevel": "Info",
        "writeTo": "mcplogsfile"
      },
      {
        "logger": "ratelimitlogs",
        "minLevel": "Warn",
        "writeTo": "ratelimitlogsfile,ratelimitlogsconsole"
      },
      {
        "logger": "ratelimitmetrics",
        "minLevel": "Info",
        "writeTo": "ratelimitlogsfile,ratelimitlogsconsole"
      }
    ]
  }
}
```

この設定では、次の両方がstdoutに出力されます。

|EventType|内容|
|:--|:--|
|RateLimitRejected|実際に拒否したリクエストの詳細|
|RateLimitWouldHaveRejected|LogOnlyで拒否相当と判定されたリクエストの詳細|
|RateLimitMetricsSnapshot|一定時間ごとの拒否件数集計|

詳細ログにはIP、ログインID、ユーザーID、テナントID、リクエストパスなどが含まれる場合があります。外部基盤へ送信する場合は、保存先の権限、保存期間、マスキング方針を確認してください。

## 注意事項

### WindowsサービスまたはIISで運用する場合

WindowsサービスまたはIISでは、stdoutよりもファイル出力とファイルシッパー（ログファイルの監視・転送ソフトウェア）の組み合わせを推奨します。

この場合は標準設定のままlogs/{yyyy}/{MM}/{dd}/ratelimitlogs.jsonを収集対象にしてください。

### APIキーの扱い

ApiKeyパーティションのキーはSHA-256でマスクされ、生のAPIキーはログに出力されません。

ただし、詳細ログにはIP、ログインID、ユーザーID、テナントID、リクエストパスなどが含まれる場合があります。stdoutへ詳細ログを出す場合は、ログ収集先のアクセス権限と保存期間を確認してください。

## 設定反映

設定を変更した後、プリザンターを再起動してください。

再起動後、LogOnlyまたはOnのポリシーで拒否相当のリクエストが発生すると、RateLimitMetricsSnapshotが出力されます。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.6.0 以降|レートリミット機能を追加|
