---
title: Pleasanter MCPをVisual Studio Codeで使う
category: Pleasanter MCP
order: '400'
status: ''
parts: ''
urlstring: pleasanter-mcp-vscode
translationKey: pleasanter-mcp-vscode
shortname: Pleasanter MCPをVisual Studio Codeで使う
created: 2026-02-25
updated: 2026-09-08
---

## 概要

Pleasanter MCPをVisual Studio Codeで使う方法を解説します。

### 確認事項

1. 以下の手順を実施する前に、[Pleasanter MCPを使う](index.md)の手順が完了していることを確認してください。
1. 以下の手順はVisual Studio Codeがインストール済みであることを前提としています。

### Pleasanter MCP拡張機能のインストール

Pleasanter MCP拡張機能を使うと、Visual Studio CodeからPleasanter MCPを利用できるようになります。

「 拡張機能」ビューを開いてください（++ctrl+shift+x++）。「Marketplace で拡張機能を検索」テキストボックスにPleasanter MCPと入力し、「インストール」ボタンをクリックしてください。

![Visual Studio Code の拡張機能ビュー。Pleasanter MCP を検索したところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/e2a0d6085b2543d19020ccb19df2eb92.png)

### Pleasanter MCP拡張機能の初期設定

ショートカットキー ++ctrl+shift+p++ でコマンドパレットを開き、「Pleasanter MCP: 設定画面を開く」を実行してください。

![コマンドパレットで「Pleasanter MCP: 設定画面を開く」を選んだところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/930cce9cfed24876b134c5f4c95fff9c.png)

「Pleasanter URL」と「API key」を入力し、「Save」ボタンをクリックしてください。

![Pleasanter MCP の設定画面。「Pleasanter URL」と「API key」を入力し「Save」ボタンがある](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/e27a9ece312a4815b10581e9ed4a686b.png)

「Pleasanter URL」には、以下のようなURLを設定してください。

``` text
http(s)://{サーバ名}/{パス}/mcp
```

1.  {サーバ名}や{パス}はセットアップの状況によって異なる場合があります。
1.  実際に利用しているURLを確認して適宜変更してください。
1.  以下は各環境におけるURLの例です。

    | サーバ名    | パス       | URLの例                            |
    | :---------- | :--------- | :--------------------------------- |
    | localhost   | なし       | http://localhost/mcp               |
    | example.com | pleasanter | https://example.com/pleasanter/mcp |

「API key」には、[Pleasanter MCPを使う](index.md)で控えたAPIキーを入力してください。入力したAPIキーは、OSのキーチェーンに保存されます。

### Visual Studio Codeの動作確認

「新しいチャット エディター」を開きます。

![Visual Studio Code で新しいチャット エディターを開いたところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/0966d13df5f5415aa963a4f4e99955b3.png)

以下のメッセージを入力してください。

``` text
プリザンターのMCPで使えるツールを教えてください。
```

以下のような表示を得られれば、動作確認は完了です。AIの性質上、同じ質問をしても、完全に同じ回答を得られる保証はないことに注意してください。

![チャットで、Pleasanter MCP で使えるツールの一覧が返ってきたところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/53803d3cfa614924862ea790794604ae.png)

## 注意事項

1.  AIが生成する回答には誤りが含まれる可能性があります。回答内容は必ず確認してください。
1.  このマニュアルはプリザンター1.5.3.0リリース時のVisual Studio Codeに基づきます。

## 対応バージョン

| 対応バージョン | 内容                                         |
| :------------- | :------------------------------------------- |
| 1.5.2.0 以降   | 機能追加                                     |
| 1.5.3.0 以降   | レコードの新規作成、レコードの削除機能を追加 |

## 関連情報

-   [Pleasanter MCPを使う](index.md)
