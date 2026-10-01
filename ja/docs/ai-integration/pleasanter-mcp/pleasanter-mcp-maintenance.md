---
title: Pleasanter MCPを運用する
category: Pleasanter MCP
order: '0'
status: ''
parts: ''
urlstring: pleasanter-mcp-maintenance
translationKey: pleasanter-mcp-maintenance
shortname: Pleasanter MCPを運用する
created: 2026-03-04
updated: 2026-03-10
---

## 概要

Pleasanter MCPの運用に役立つ機能をまとめます。

### レートリミット機能

AIエージェントによるアクセスを制御するために、Pleasanter MCPにはレートリミット機能が備わっています。レートリミットは、サーバへのリクエスト（アクセス）回数を一定時間内に制限する仕組みです。

詳細は[McpServer.json](../../setup/parameters/mcpserver-json.md)を参照してください。

### MCPログ管理機能

Pleasanter MCPは、MCPリクエスト・レスポンスの詳細を、MCPログとしてデータベースへ記録できます。この機能は設定ファイル[McpServer.json](../../setup/parameters/mcpserver-json.md)を編集して有効化できます。

#### ログの閲覧

データベースに記録されたログは、プリザンターの「MCPログ」画面で閲覧できます。「MCPログ」画面には、特定の条件で絞り込んだログをCSVファイルへエクスポートする機能も備わっています。詳細は[MCPログ管理機能](../../managers-guide/mcp-log-adminnistration/index.md)を参照してください。

#### ログの削除

ログは定期的に削除することができます。詳細は[BackgroundService.json](../../setup/parameters/background-service-json.md)を参照してください。

## 対応バージョン

| 対応バージョン | 内容     |
| -------------- | -------- |
| 1.5.2.0 以降   | 機能追加 |

## 関連情報

-   [McpServer.json](../../setup/parameters/mcpserver-json.md)
-   [BackgroundService.json](../../setup/parameters/background-service-json.md)
-   [MCPログ管理機能](../../managers-guide/mcp-log-adminnistration/index.md)
