---
title: MCPログ管理機能
category: MCPログ管理機能
order: '0'
status: ''
parts: ''
urlstring: pleasanter-mcp-log
translationKey: pleasanter-mcp-log
shortname: MCPログ管理機能
created: 2026-03-04
updated: 2026-03-10
---

## 概要

データベース内に出力されたMCPログをプリザンターで閲覧することができます。

## 前提条件

1. ログ出力を有効化するには、設定ファイル[McpServer.json](../../setup/parameters/mcpserver-json.md)のパラメータEnableLoggingToDatabaseをtrueに設定する必要があります。

## 制限事項

1. [特権ユーザ](../user-administration/user-management-privileged-users.md)のみ利用できます。
1. レコードの更新はできません。
1. 表示するカラムは変更できません。
1. 作成日時の降順で表示され、任意でのソートはできません。
1. 必ず[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)の条件を1つ以上指定してください。条件指定がない場合は[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)ボタンをクリックしてもMCPログは表示しません。
1. エクスポート時の書式は変更できません。
1. エクスポートは[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)ボタンクリック後に表示したレコードで指定した条件に合致したログがエクスポートされます。

## MCPログの閲覧

特権ユーザが以下のURLを開くと、MCPログの一覧画面が表示されます。

```text
http(s)://{サーバ名}/{パス}/mcplogs
```

1. {サーバ名}や{パス}はセットアップの状況によって異なる場合があります。
1. 実際に利用しているURLを確認して適宜変更してください。
1. 以下は各環境におけるURLの例です。

    |サーバ名|パス|URLの例|
    |:--|:--|:--|
    |localhost|なし|http://localhost/mcplogs|
    |example.com|pleasanter|https://example.com/pleasanter/mcplogs|

![MCPログの一覧画面](https://pleasanter.org/files/images/ja/managers-guide/mcp-log-adminnistration/assets/5857bc5e675b4810ba9f262e7a749333.png)

#### フィルタの設定

MCPログの一覧画面上部でフィルタを設定すると、条件に一致するログがレコードとして表示されます。条件を設定後、フィルタボタンをクリックしてください。

![フィルタを設定したMCPログの一覧画面](https://pleasanter.org/files/images/ja/managers-guide/mcp-log-adminnistration/assets/04ff79b9d591470da0cc9aaa1261a824.png)

ログレコード行をクリックすると、詳細が単票形式で表示されます。読取専用のため、更新や削除ができないことに注意してください。前・次ボタンをクリックすると、前後のログを確認できます。

![MCPログの詳細を単票形式で表示した画面](https://pleasanter.org/files/images/ja/managers-guide/mcp-log-adminnistration/assets/0e1d87d0ffd247fe9b7009ab58a2cd18.png)

#### MCPログに出力される情報

MCPログには以下の情報が出力されます。

|DBのカラム名|MCPログ画面の項目名|説明|
|:--|:--|:--|
|McpLogId|MCPログID|MCPログの管理番号（自動付与）|
|StartTime|開始日時|以下が開始されたタイムスタンプ<br>・特定のイベント<br>・ツール呼び出し<br>・サーバとのやり取り|
|EndTime|終了日時|以下が終了されたタイムスタンプ<br>・特定のイベント<br>・ツール呼び出し<br>・サーバとのやり取り|
|McpRequestId|MCPリクエストID|MCPリクエストの管理番号（自動付与）|
|McpSessionId|MCPセッションID|MCPセッションの管理番号（自動付与）|
|McpMethod|MCPメソッド|リクエストに使用されたメソッド|
|TargetName|対象名|リクエストに使用されたツール名、プロンプト名|
|UserId|ユーザ|APIキーと紐づくプリザンターのユーザID|
|ApiKeyPrefix|APIキー接頭辞|APIキーの先頭16文字|
|Elapsed|経過時間|開始日時と終了日時との差|
|Status|状況|HTTPステータスコード|
|JsonRpcErrorCode|JSON-RPCエラーコード|JSON-RPCエラーコード（負値でエラー）|
|ErrMessage|エラーメッセージ|JSON形式のエラーメッセージボディ|
|RequestData|リクエストデータ|JSON-RPC形式のリクエストボディ|
|ResponseData|レスポンスデータ|JSON-RPC形式のレスポンスボディ|
|UserHostAddress|クライアントIP|クライアントのIPアドレス|
|UserAgent|ユーザーエージェント|ユーザエージェント名|
|Ver|バージョン|バージョン|

#### MCPログのエクスポート

MCPログをCSVファイルとしてエクスポートできます。

1. 上記の「MCPログの閲覧」の手順でエクスポートしたいMCPログを表示してください。
1. コマンドボタンエリアの[エクスポート](../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしてください。
1. 表示されたダイアログで文字コードを選択し、[エクスポート](../../developers-guide/api/table-operations/api-export.md)ボタンをクリックしてください。

なお、エクスポートする際の上限数は、設定ファイル[McpServer.json](../../setup/parameters/mcpserver-json.md)のパラメータLogExportLimitで設定できます。

## MCPログの削除

MCPログの削除はバックグラウンドサービスで実行します。詳細は設定ファイル[BackgroundService.json](../../setup/parameters/background-service-json.md)を確認してください。

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.2.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：McpServer.json](../../setup/parameters/mcpserver-json.md)
-   [ユーザ管理機能：特権ユーザの設定](../user-administration/user-management-privileged-users.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../developers-guide/api/table-operations/api-export.md)
-   [パラメータ設定：BackgroundService.json](../../setup/parameters/background-service-json.md)