---
title: Pleasanter MCPをClaude Desktopで使う（設定ファイル）
category: Pleasanter MCP
order: '300'
status: ''
parts: ''
urlstring: pleasanter-mcp-claude-config
translationKey: pleasanter-mcp-claude-config
shortname: ''
created: 2026-02-26
updated: 2026-04-17
---

## 概要

Claude Desktopの設定ファイルを編集することでPleasanter MCPサーバを使用する方法を解説します。

### 確認事項

1.  以下の手順を実施する前に、[Pleasanter MCPを使う](index.md)の手順が完了していることを確認してください。
1.  Claude Desktopの拡張機能を利用する方法は[Pleasanter MCPをClaude Desktopで使う（拡張機能）](pleasanter-mcp-claude-extensions.md)の手順を確認してください。

### Node.jsのインストール

以下のURLからNode.jsをダウンロードし、画面の指示に従ってインストールしてください。

``` text
https://nodejs.org/ja/download
```

![Node.js のダウンロードページ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/097a296d54bd4165b5e5c795f6a1d3ab.png)

### Claude Desktopのインストール

以下のURLからClaude Desktopをダウンロードし、画面の指示に従ってインストールしてください。

``` text
https://claude.com/ja-jp/download
```

![Claude Desktop のダウンロードページ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/496ea87c966740518c3434b715df270d.png)

初回ログイン時、メールアドレスを入力すると認証コードが届きます。認証コードを入力すると、Claude Desktopの利用を開始できます。

### Claude Desktopの設定

Claude Desktopの設定画面を開いてください。

![Claude Desktop の設定画面](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/bf1191012a7e4ef5ae84c5b94db40017.png)

「開発者」を選択し、「設定を編集」ボタンをクリックしてください。

![Claude Desktop の設定画面の「開発者」。「設定を編集」ボタンがある](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/bc1deff5b33d4e64a17d0528d5129312.png)

エクスプローラーが起動し、C:\Users\ユーザ名\AppData\Roaming\Claude\フォルダーが開き、claude_desktop_config.jsonが選択された状態となります。

![エクスプローラーで Claude のフォルダーが開き、claude_desktop_config.json が選択された状態](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/ce38c558f62d42ff88be48a5722d2ceb.png)

claude_desktop_config.jsonをメモ帳などで開き、以下の内容をコピーして貼り付けてください。

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
        "X-API-Key:${PLEASANTER_API_KEY}",
        "--allow-http"
      ]
    }
  }
}
```

1.  {サーバ名}や{パス}はセットアップの状況によって異なる場合があります。
1.  実際に利用しているURLを確認して適宜変更してください。
1.  以下は各環境におけるURLの例です。

    | サーバ名    | パス       | URLの例                            |
    | :---------- | :--------- | :--------------------------------- |
    | localhost   | なし       | http://localhost/mcp               |
    | example.com | pleasanter | https://example.com/pleasanter/mcp |

MCPサーバへの接続がうまくいかない原因の多くは、このファイルの編集ミスです。設定がうまくいかない場合は、[FAQ：変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../FAQ/features-for-developers/faq-json-format.md)を参考にしてください。

### ユーザ環境変数にAPIキーを登録する

タスクバーの「スタート」ボタンをクリックしてEnvと入力し、「環境変数を編集」を選択してください。

![スタートメニューで Env と入力し、「環境変数を編集」が候補に出たところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/5add864285b64a0790cd0bc08001b87e.png)

画面上側のユーザー環境変数の「新規」ボタンをクリックし、以下の情報を設定してください。

| 変数名             | 変数値                                                     |
| :----------------- | :--------------------------------------------------------- |
| PLEASANTER_API_KEY | [Pleasanter MCPを使う](index.md)で発行したAPIキー |

??? tip "他のMCPサーバが設定済みの場合"

    claude_desktop_config.jsonに他のMCPサーバが設定済みの場合、たとえば、以下の赤字部分のように編集します。既存の設定の末尾に半角カンマ（,）を補ったり、コピーする範囲を変更したりしていることに注意してください。
    
    ![他の MCP サーバが設定済みの claude_desktop_config.json に書き足す例。追加する部分が赤字で示されている](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/041af05dab824b9faa62044b6ba28f80.png)

### Claude Desktopの終了

設定が済んだら、変更を反映するためにClaude Desktopを完全に終了します。Claude Desktopを完全に終了するには、タスクトレイから「終了」を選択する必要があります。

![タスクトレイの Claude Desktop のメニュー。「終了」が選べる](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/47a79c4dd3124eb2be3313ea580dfbd3.png)

### コネクタの疎通確認

Claude Desktopを起動して「設定」画面を開き、「開発者」を選択してください。正しく設定できていれば、「running」という表示を確認できます。うまくいかない場合は、claude_desktop_config.jsonの設定を中心に手順を見直してください。

![Claude Desktop の設定画面の「開発者」。Pleasanter MCP が「running」と表示されている](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/4e6a080a539740db9e04989300294b07.png)

### Claude Desktopの動作確認

新規チャットを開いて（++ctrl+shift+o++）、以下のメッセージを入力してください。

``` text
プリザンターのMCPで使えるツールを教えてください。
```

以下のような表示を得られれば、初期設定は完了です。AIの性質上、同じ質問をしても、完全に同じ表示を得られる保証はないことに注意してください。

![Claude Desktop のチャットで、Pleasanter MCP で使えるツールの一覧が返ってきたところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/34d558d56890450c9d3013e2f8f78948.png)

## 注意事項

1.  AIが生成する回答には誤りが含まれる可能性があります。回答内容は必ず確認してください。
1.  このマニュアルはプリザンター1.5.3.0リリース時のClaude Desktop（Claude for Windows）に基づきます。
1.  Claude Desktopは頻繁にバージョンアップされており、画面の一部が変更されることがあります。適宜読み替えをお願いいたします。

## 対応バージョン

| 対応バージョン | 内容                                         |
| :------------- | :------------------------------------------- |
| 1.5.2.0 以降   | 機能追加                                     |
| 1.5.3.0 以降   | レコードの新規作成、レコードの削除機能を追加 |

## 関連情報

-   [Pleasanter MCPを使う](index.md)
-   [Pleasanter MCPをClaude Desktopで使う（拡張機能）](pleasanter-mcp-claude-extensions.md)
-   [FAQ：変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../FAQ/features-for-developers/faq-json-format.md)
