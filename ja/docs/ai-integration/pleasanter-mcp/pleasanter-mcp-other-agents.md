---
title: Pleasanter MCPをその他のAIエージェントで使う
category: Pleasanter MCP
order: '0'
status: ''
parts: ''
urlstring: pleasanter-mcp-other-agents
translationKey: pleasanter-mcp-other-agents
shortname: ''
created: 2026-03-06
updated: 2026-03-12
---

## 概要

[Pleasanter MCP](index.md)は、Claude Desktop、Visual Studio Code以外のAIエージェントでも利用できます。

各AIエージェントのマニュアルで、MCPサーバの設定を書き込むべきファイルを調べ、以下の内容を貼り付けてください。

``` json title="MCPサーバとしてPleasanter MCPのみを利用する場合" linenums="1"
{
  "mcpServers": {
    "pleasanter": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "http://{サーバ名}/{パス}/mcp",
        "--transport",
        "http-first",
        "--header",
        "X-API-Key:《APIキー》",
        "--allow-http"
      ]
    }
  }
}
```

### リモートMCPサーバエンドポイント

上記の8行目、以下の部分にはMCPサーバエンドポイントを指定します。

``` text
http://{サーバ名}/{パス}/mcp
```

1.  {サーバ名}や{パス}はセットアップの状況によって異なる場合があります。
1.  実際に利用しているURLを確認して適宜変更してください。
1.  以下は各環境におけるURLの例です。

    | サーバ名    | パス       | URLの例                            |
    | :---------- | :--------- | :--------------------------------- |
    | localhost   | なし       | http://localhost/mcp               |
    | example.com | pleasanter | https://example.com/pleasanter/mcp |

MCPサーバへの接続がうまくいかない原因の多くは、このファイルの編集ミスです。設定がうまくいかない場合は、[FAQ：変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../FAQ/features-for-developers/faq-json-format.md)を参考にしてください。

### APIキー

上記の12行目、《APIキー》には、プリザンターで発行したAPIキーを指定します。

APIキーはログインパスワードと同じレベルで管理すべき認証情報です。APIキーは環境変数へ登録し、AIエージェントの設定ファイルには環境変数名を指定することを推奨します。

1.  環境変数の登録方法は、OS、シェルなどにより異なります。それぞれのマニュアルを確認してください。
1.  AIエージェントの設定ファイルで、環境変数の値を参照する記法については、各AIエージェントのマニュアルを確認してください。
1.  環境変数名は任意（例：PLEASANTER_API_KEY）です。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.2.0 以降   | 機能追加 |

## 関連情報

-   [Pleasanter MCPを使う](index.md)
-   [FAQ：変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../FAQ/features-for-developers/faq-json-format.md)
