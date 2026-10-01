---
title: McpServer.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: mcpserver-json
translationKey: mcpserver-json
shortname: McpServer.json
created: 2026-02-25
updated: 2026-09-08
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定は下記の通りです。

### トップレベルオブジェクト

|パラメータ例|設定例|説明|
|:--|:--|:--|
| Enabled | false| MCPサーバの有効・無効を切り替えます。|
| ReadOnlyMode | false | trueの場合、参照系ツールのみ利用可能になります。<br>詳細は[読み取り専用モード](#ReadOnlyMode)を参照してください。 |
| LogExportLimit | 10000 | MCPログをCSVへエクスポートする際の上限数を設定します。 |
| RateLimit | － | レートリミットの設定オブジェクトです。<br>詳細は[レートリミット設定](#RateLimit)を参照してください。 |
| Logging | － | ログ出力の設定オブジェクトです。<br>詳細は[MCPログ設定](#Logging)を参照してください。 |

<a id="ReadOnlyMode"></a>
### 読み取り専用モード（ReadOnlyMode）

ReadOnlyModeがtrueの場合、読み取り専用モードとなり、以下の参照系ツールのみが利用可能になります。それ以外の書き込み系ツールは、拒否メッセージとともにブロックされます。

##### 参照系ツール一覧
<table>
    <thead>
        <tr>
            <th>分類</th>
            <th>ツール名</th>
            <th>機能</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3">レコード操作系</td>
            <td>GetItems</td>
            <td>サイト内のレコード一覧を取得</td>
        </tr>
        <tr>
            <td>GetItem</td>
            <td>単一レコードの詳細を取得</td>
        </tr>
        <tr>
            <td>CreateUpdateItemJson</td>
            <td>更新用JSONを生成（日本語→コード変換）</td>
        </tr>
        <tr>
            <td rowspan="2">サイト情報取得系</td>
            <td>GetSiteIdByTitle</td>
            <td>サイト名からサイトIDを検索</td>
        </tr>
        <tr>
            <td>GetSite</td>
            <td>サイトの設定情報を取得</td>
        </tr>
        <tr>
            <td>サイトテンプレート情報取得系</td>
            <td>GetSiteTemplates</td>
            <td>サイトテンプレートの一覧を取得</td>
        </tr>
        <tr>
            <td rowspan="2">ユーザ情報取得系</td>
            <td>GetUserIdByName</td>
            <td>ユーザ名からユーザIDを検索</td>
        </tr>
        <tr>
            <td>GetUsers</td>
            <td>ユーザ一覧を取得</td>
        </tr>
        <tr>
            <td rowspan="3">ビュー操作系</td>
            <td>CreateViewJson</td>
            <td>検索条件のView JSONを作成</td>
        </tr>
        <tr>
            <td>GetView</td>
            <td>ビュー設定を取得</td>
        </tr>
        <tr>
            <td>GetViewIdByViewName</td>
            <td>ビュー名からビューIDを検索</td>
        </tr>
    </tbody>
</table>

<a id="RateLimit"></a>
### レートリミット設定（RateLimit）

レートリミットは一定時間内に行える操作の回数を制限する仕組みです。Pleasanter MCPでは、4種類のレートリミット方式を利用できます。

1. 複数のレートリミット方式を同時に有効化した場合、すべてのリミッタが連結適用されます。レートリミットはAPIキー単位でパーティション分割されます。
1. レートリミット超過時はHTTP 429が返却され、Retry-Afterヘッダーが付与されます。レスポンスボディにはJSON-RPCエラー形式でメッセージが含まれます。
1. 利用制限の確認は、ユーザがリクエストを送信したタイミングで行われます。リクエストを受け取ったシステムが、次にリセットされる時刻を計算し、現在の利用状況が制限内に収まっているかを判定します。このチェックはバックグラウンドで定期的に実行されるのではなく、リクエストのたびにその場で判定される仕組みです。

#### ①FixedWindow（固定ウィンドウ）

一定時間（ウィンドウ）ごとにカウンタをリセットし、その枠内での操作回数を制限する方式です。ウィンドウの境界付近で操作が集中すると、場合によってはレートリミットの2倍近いスループットを許容する可能性があります。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| Enabled | false | 固定ウィンドウ方式の有効・無効を切り替えます。 |
| PermitLimit | 30 | ウィンドウ内の許可リクエスト数を設定します。 |
| WindowSeconds | 60 | ウィンドウの長さ（秒）を設定します。 |

#### ②SlidingWindow（スライディングウィンドウ）

直近の一定期間（ウィンドウ）だけを対象に操作回数を制限する方式です。Pleasanter MCPではカウンタ近似方式という、ウィンドウを複数のセグメントに分割し、セグメント単位で操作回数を制限する方式を採用しています。一般的に、Fixed Windowよりもウィンドウ境界でのバーストが発生しづらいとされています。

SegmentsPerWindowを増やすと、時間分解能が細かくなり、メモリ消費と更新頻度が増えます。逆にSegmentsPerWindowを減らすと、FixedWindow方式に近づきます。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| Enabled | false | スライディングウィンドウ方式の有効・無効を切り替えます。 |
| PermitLimit | 30 | ウィンドウ内の許可リクエスト数を設定します。 |
| WindowSeconds | 60 | ウィンドウの長さ（秒）を設定します。 |
| SegmentsPerWindow | 5 | ウィンドウのセグメント分割数を設定します。 |

#### ③TokenBucket（トークンバケット）

バケット内のトークンを消費する形で操作回数を制限する方式です。バケット内にトークンが存在する限り処理は即時許可され、枯渇した場合は拒否されます。バケット内のトークンは一定間隔で補充されます。単位時間あたりのリミットを設けつつ、瞬間的なスループット増加にも対応したい場合に向いています。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| Enabled | false | トークンバケット方式の有効・無効を切り替えます。 |
| TokenLimit | 10 | バケットの最大トークン数を設定します。 |
| TokensPerPeriod | 1 | 補充期間ごとの追加トークン数を設定します。 |
| ReplenishmentPeriodSeconds | 2 | トークン補充間隔（秒）を設定します。 |

#### ④Concurrency（同時実行数制限）

負荷制御に近い方式です。単位時間あたりの回数ではなく、同時実行数を制限します。同時実行開始時にカウントを増やし、完了時に減らします。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| Enabled | false | 同時実行数制限方式の有効・無効を切り替えます。 |
| PermitLimit | 3 | 最大同時リクエスト数を設定します。 |

<a id="Logging"></a>
### MCPログ設定（Logging）

MCPリクエスト・レスポンスのログに関する設定です。

|パラメータ例|設定例|説明|
|:--|:--|:--|
| EnableLoggingToDatabase | true | MCPログをデータベースに記録するかどうかを設定します。[MCPログ管理機能](../../managers-guide/mcp-log-adminnistration/index.md) を参照してください。|
| EnableLoggingToFile | false | MCPログをファイルに記録するかどうかを設定します。設定方法は[システムログのテキスト出力](../additional/ops-management/syslogs-text-output.md)と同様です。 |
| NotLoggingIp | [127.0.0.1] | MCPログを記録しないIPアドレスのリスト（CIDR表記対応）を設定します。 |
| ResponseDataMaxLength | 65536 | レスポンスデータの最大保存サイズ（バイト）を設定します。0で無制限となります。超過分は切り捨てられます。 |

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.2.0 以降|McpServer.jsonを追加|
|1.5.8.0 以降|参照系ツールとしてGetSiteTemplatesを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [MCPログ管理機能](../../managers-guide/mcp-log-adminnistration/index.md)
-   [システムログをテキスト出力できるようにする](../additional/ops-management/syslogs-text-output.md)
