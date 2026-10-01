---
title: RateLimit.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: ratelimit-json
translationKey: ratelimit-json
shortname: RateLimit.json
created: 2026-06-19
updated: 2026-07-14
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/b15923f5b5bb4f5e9b44ada7821f0c74.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/f6ae3ced07544e1b8ff4ec4e88c16b9e.svg#only-dark)](https://pleasanter.org/support/)

（本機能は[Extensionsトライアル](../../products-info/extensions-trial/index.md)で試用可能です）

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)をご確認ください。

「RateLimit.json」はプリザンターの起動時に読み込まれます。設定値を変更した場合は、プリザンターの再起動後に反映されます。

## 設定値

本パラメータファイルの設定値は下記の通りです。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Mode|"Off"|レートリミット機能全体の動作モードを指定します。設定方法は後述。|
|ApplyPaths|[ "/" ]|レートリミットを適用するパス（接頭辞）を指定します。既定値は全パス（"/"）です。|
|ExcludePaths|[ "/mcp", "/healthz", … ]|レートリミットの適用対象から除外するパスを指定します（「GlobalLimiter」・機能カテゴリ別ポリシーの両方に適用）。詳細は後述の「ExcludePathsについて」を参照してください。|
|KeyResolver|設定方法は後述|Partitionが"Auto"のポリシーで使用する、パーティションキーの解決順を指定します。|
|Exclusions|設定方法は後述|レートリミットの対象外とするユーザを指定します。|
|GlobalLimiter|設定方法は後述|全リクエスト共通の上位ポリシー（最終防壁）です。|
|Policies|設定方法は後述|機能カテゴリ別のポリシー（General / List / Admin など）です。|
|RejectedResponse|設定方法は後述|上限超過時の応答に関する設定です。|

### Modeの設定

トップレベルの「Mode」で、レートリミット機能全体の動作を切り替えます。

|設定値|説明|
|:--|:--|
|Off|（既定値）レートリミット機能を無効にします。ミドルウェアを登録しないため、性能への影響はありません。|
|LogOnly|上限超過を観測してログ（仮想拒否ログ）に記録しますが、リクエストの遮断（429の返却）は行いません。閾値を調整する際の観測に利用します。|
|On|上限超過時に「429 Too Many Requests」を返してリクエストを遮断します。|

各ポリシー（GlobalLimiter / Policies 配下）の「Mode」を個別に指定することで、ポリシーごとに動作を上書きできます（後述）。

### Exclusionsの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|LoginIds|[ "batch", "monitor" ]|レートリミットの対象外とするユーザのログインIDを指定します。バッチ処理用アカウントや監視ツールなど、制限の対象としたくないユーザを指定します。ログインID（文字列）で照合し、大文字・小文字は区別しません。|

### KeyResolverの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Order|[ "User", "Ip" ]|Partitionが"Auto"のポリシーで、どの順にパーティションキーを解決するかを指定します。先頭から順に評価し、最初に解決できた単位（ログインユーザまたはIP）を使用します。|

### GlobalLimiter / Policies 共通の設定項目

「GlobalLimiter」および「Policies」配下の各ポリシーは、共通して以下の項目で構成されます。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Mode|"Inherit"|ポリシー個別の動作モードを指定します。"Inherit"（既定）はトップレベルの「Mode」を継承します。"Off" / "LogOnly" / "On" を指定すると、そのポリシーだけ個別に上書きできます。|
|Algorithm|"TokenBucket"|制限アルゴリズムを指定します。設定方法は後述の「Algorithm（制限アルゴリズム）」を参照してください。|
|Partition|"User"|制限の単位を指定します。設定方法は後述の「Partition（制限の単位）」を参照してください。|
|QueueLimit|0|上限到達時に待機させるリクエスト数を指定します。既定値は0（待機させず即座に拒否）です。|
|（アルゴリズム固有の項目）|—|アルゴリズムごとに指定する項目が異なります。後述の「Algorithm（制限アルゴリズム）」を参照してください。|

### Partition（制限の単位）

|設定値|説明|
|:--|:--|
|User|ログインユーザ（ログインID）単位で制限します。未認証のリクエストは対象外です。|
|Ip|接続元IPアドレス単位で制限します。|
|ApiKey|APIキー単位で制限します。|
|Auto|「KeyResolver」の「Order」に従って単位を解決します（既定では User → Ip の順）。|

> 制限はパーティション（単位）ごとに独立してカウントされます。たとえば「User」単位のポリシーでは、利用者ごとに別々の上限が適用されます。

### Algorithm（制限アルゴリズム）

制限アルゴリズムとは、レートリミットにおいて一定時間内に行える操作の回数を制限するためのルールです。アルゴリズムごとにアクセスの判定方法や制限の特性が異なるため、利用シーンに応じて適切な方式を選択できます。

#### ①FixedWindow（固定ウィンドウ）

一定時間（ウィンドウ）ごとにカウンタをリセットし、その枠内での操作回数を制限する方式です。ウィンドウの境界付近で操作が集中すると、場合によってはレートリミットの2倍近いスループットを許容する可能性があります。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| PermitLimit | 30 | ウィンドウ内の許可リクエスト数を設定します。 |
| WindowSeconds | 60 | ウィンドウの長さ（秒）を設定します。 |

#### ②SlidingWindow（スライディングウィンドウ）

直近の一定期間（ウィンドウ）だけを対象に操作回数を制限する方式です。本機能ではカウンタ近似方式という、ウィンドウを複数のセグメントに分割し、セグメント単位で操作回数を制限する方式を採用しています。一般的に、Fixed Windowよりもウィンドウ境界でのバーストが発生しづらいとされています。

SegmentsPerWindowを増やすと、時間分解能が細かくなり、メモリ消費と更新頻度が増えます。逆にSegmentsPerWindowを減らすと、FixedWindow方式に近づきます。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| PermitLimit | 30 | ウィンドウ内の許可リクエスト数を設定します。 |
| WindowSeconds | 60 | ウィンドウの長さ（秒）を設定します。 |
| SegmentsPerWindow | 5 | ウィンドウのセグメント分割数を設定します。 |

#### ③TokenBucket（トークンバケット）

バケット内のトークンを消費する形で操作回数を制限する方式です。バケット内にトークンが存在する限り処理は即時許可され、枯渇した場合は拒否されます。バケット内のトークンは一定間隔で補充されます。単位時間あたりのリミットを設けつつ、瞬間的なスループット増加にも対応したい場合に向いています。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| TokenLimit | 10 | バケットの最大トークン数を設定します。 |
| TokensPerPeriod | 5 | 補充期間ごとの追加トークン数を設定します。 |
| ReplenishmentPeriodSeconds | 1 | トークン補充間隔（秒）を設定します。 |

#### ④Concurrency（同時実行数制限）

負荷制御に近い方式です。単位時間あたりの回数ではなく、同時実行数を制限します。同時実行開始時にカウントを増やし、完了時に減らします。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| PermitLimit | 3 | 最大同時リクエスト数を設定します。 |

### Policies（機能カテゴリ別ポリシー）

「Policies」配下には以下の既定ポリシーがあります。各ポリシーは前述の「共通の設定項目」「Algorithm（制限アルゴリズム）」で構成されます。既定値および各ポリシーの対象は下表のとおりです。各ポリシーの役割や閾値調整の考え方は、機能マニュアル「[レートリミット機能：ポリシーと閾値の調整](../additional/performance/ratelimit-policy-threshold-setting.md)」を参照してください。

|ポリシー名|単位|アルゴリズム|既定の上限|主な対象|
|:--|:--|:--|:--|:--|
|General|User|TokenBucket|容量10 / 毎秒+5|一般的な画面操作|
|List|User|SlidingWindow|直近60秒で30回|一覧・検索・グリッド・集計ビュー|
|Admin|User|FixedWindow|60秒ごとに30回|管理操作（ユーザ／組織／グループ管理など）|
|Heavy|User|Concurrency|同時1|画面側の重い処理（エクスポート・インポートなど）|
|ApiHeavy|ApiKey|Concurrency|同時1|API経由の重い処理|
|Api|Auto|TokenBucket|容量30 / 毎秒+10|REST API 全般|
|AnonymousIp|Ip|FixedWindow|60秒で60回|未認証アクセス（ログイン試行など）|
|PublicForm|Ip|TokenBucket|容量5 / 毎秒+2|公開フォームの送信|

### RejectedResponseの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|IncludeRetryAfter|true|上限超過時の応答に「Retry-After」ヘッダ（再試行までの目安秒数）を付与する場合はtrueを指定します。|
|LogRejected|true|Modeが「On」の場合は、実際に拒否したリクエストを構造化ログに記録するかを指定します。falseにしても件数（メトリクス）は常に記録されます。Modeが「LogOnly」のときの仮想拒否ログは、本設定に関わらず常に出力されます。|

### ExcludePathsについて

「ExcludePaths」に指定したパスは、「GlobalLimiter」と機能カテゴリ別のポリシー（General / List / Admin など）の両方で適用対象から除外されます（該当パスへのリクエストにはレートリミットが行われません）。

既定では以下のパスが指定されています。

```json
"ExcludePaths": [
    "/mcp",
    "/healthz",
    "/favicon.ico",
    "/Css",
    "/Scripts",
    "/fonts",
    "/images",
    "/binaries",
    "/backgroundtasks",
    "/reminderschedules",
    "/api/backgroundtasks",
    "/cspreport",
    "/errors",
    "/resources"
]
```

### PublicFormの調整（社内NAT環境など）

「PublicForm」は接続元IPアドレス単位（Ip）で制限します。社内NATなど、多数の利用者が同一のIPアドレスを共有する環境では、上限に達しやすくなります。共有規模に応じて、以下を目安に閾値の拡大を検討してください。

|利用形態|TokenLimit|TokensPerPeriod|
|:--|:--|:--|
|個別利用（顧客向けなど）|5|2|
|社員50〜100名規模の社内NAT共有|20|10|
|大規模な社内NAT（500名以上）|50|25|

### 設定例

各ポリシーの記述例は以下の通りです。「GlobalLimiter」と「Policies」配下の各ポリシーは、同じ形式で記述します。

```json
﻿{
    "Mode": "On",
    "ApplyPaths": ["/"],
    "ExcludePaths": [
        "/mcp",
        "/healthz",
        "/favicon.ico",
        "/Css",
        "/Scripts",
        "/fonts",
        "/images",
        "/binaries",
        "/backgroundtasks",
        "/reminderschedules",
        "/api/backgroundtasks",
        "/cspreport",
        "/errors",
        "/resources"
    ],
    "KeyResolver": {
        "Order": ["User", "Ip"]
    },
    "Exclusions": {
        "LoginIds": []
    },
    "GlobalLimiter": {
        "Mode": "Inherit",
        "Algorithm": "TokenBucket",
        "Partition": "Auto",
        "TokenLimit": 100,
        "TokensPerPeriod": 50,
        "ReplenishmentPeriodSeconds": 1,
        "QueueLimit": 0
    },
    "Policies": {
        "General": {
            "Mode": "Inherit",
            "Algorithm": "TokenBucket",
            "Partition": "User",
            "TokenLimit": 10,
            "TokensPerPeriod": 5,
            "ReplenishmentPeriodSeconds": 1,
            "QueueLimit": 0
        },
        "List": {
            "Mode": "Inherit",
            "Algorithm": "SlidingWindow",
            "Partition": "User",
            "PermitLimit": 30,
            "WindowSeconds": 60,
            "SegmentsPerWindow": 6,
            "QueueLimit": 0
        },
        "Admin": {
            "Mode": "Inherit",
            "Algorithm": "FixedWindow",
            "Partition": "User",
            "PermitLimit": 30,
            "WindowSeconds": 60,
            "QueueLimit": 0
        },
        "Heavy": {
            "Mode": "Inherit",
            "Algorithm": "Concurrency",
            "Partition": "User",
            "PermitLimit": 1,
            "QueueLimit": 0
        },
        "ApiHeavy": {
            "Mode": "Inherit",
            "Algorithm": "Concurrency",
            "Partition": "ApiKey",
            "PermitLimit": 1,
            "QueueLimit": 0
        },
        "Api": {
            "Mode": "Inherit",
            "Algorithm": "TokenBucket",
            "Partition": "Auto",
            "TokenLimit": 30,
            "TokensPerPeriod": 10,
            "ReplenishmentPeriodSeconds": 1,
            "QueueLimit": 0
        },
        "AnonymousIp": {
            "Mode": "Inherit",
            "Algorithm": "FixedWindow",
            "Partition": "Ip",
            "PermitLimit": 60,
            "WindowSeconds": 60,
            "QueueLimit": 0
        },
        "PublicForm": {
            "Mode": "Inherit",
            "Algorithm": "TokenBucket",
            "Partition": "Ip",
            "TokenLimit": 5,
            "TokensPerPeriod": 2,
            "ReplenishmentPeriodSeconds": 1,
            "QueueLimit": 0
        }
    },
    "RejectedResponse": {
        "IncludeRetryAfter": true,
        "LogRejected": true
    }
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.6.0 以降|RateLimit.jsonを追加|

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
