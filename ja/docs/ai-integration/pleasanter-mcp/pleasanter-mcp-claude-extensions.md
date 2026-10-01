---
title: Pleasanter MCPをClaude Desktopで使う（拡張機能）
category: Pleasanter MCP
order: '200'
status: ''
parts: ''
urlstring: pleasanter-mcp-claude-extensions
translationKey: pleasanter-mcp-claude-extensions
shortname: Pleasanter MCPをClaude Desktopで使う（拡張機能）
created: 2026-02-25
updated: 2026-09-08
---

## 概要

Claude Desktopの拡張機能として提供されるPleasanter MCPを使用する方法を解説します。

### 確認事項

1.  以下の手順を実施する前に、[Pleasanter MCPを使う](index.md)の手順が完了していることを確認してください。
1.  拡張機能を利用できない場合は、[Pleasanter MCPをClaude Desktopで使う（設定ファイル）](pleasanter-mcp-claude-config.md)の手順を確認してください。

### Node.jsのインストール

以下のURLからNode.jsをダウンロードし、画面の指示に従ってインストールしてください。

https://nodejs.org/ja/download

![Node.js のダウンロードページ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/097a296d54bd4165b5e5c795f6a1d3ab.png)

### Claude Desktopのインストール

以下のURLからClaude Desktopをダウンロードし、画面の指示に従ってインストールしてください。

``` text
https://claude.com/ja-jp/download
```

![Claude Desktop のダウンロードページ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/496ea87c966740518c3434b715df270d.png)

初回ログイン時、メールアドレスを入力すると認証コードが届きます。認証コードを入力すると、Claude Desktopの利用を開始できます。

### PleasanterMCP拡張機能のダウンロード

以下のURLを開き、「PleasanterMCP.mcpb」をクリックし、ダウンロードしてください。

``` text
https://github.com/Implem/Pleasanter-MCP/releases/tag/v1.0.0
```

![PleasanterMCP.mcpb を配布しているページ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/c3566ef7a9dc450c82005538690b6c2c.png)

### Claude Desktopの設定

Claude Desktopの設定画面を開いてください。

![Claude Desktop の設定画面](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/28b1f6b2218645dfa677359243ca0031.png)

「拡張機能」を選択し、「詳細設定」ボタンをクリックしてください。

![Claude Desktop の設定画面の「拡張機能」。「詳細設定」ボタンがある](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/82bf816e047044d2a90e4ef80a5bbcb9.png)

「拡張機能をインストール」ボタンをクリックしてください。

![「拡張機能をインストール」ボタンがある画面](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/d1e28d91704b41c0ad06dcd4d0c29499.png)

ダウンロードした「PleasanterMCP.mcpb」を選択し、「プレビュー」ボタンをクリックしてください。

![ファイル選択ダイアログで PleasanterMCP.mcpb を選んだところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/93981189cbbb48888d5743ca244c7e99.png)

「インストール」ボタンをクリックしてください。

![拡張機能のプレビュー。「インストール」ボタンがある](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/2cc05bb4a75941e1aac7bf846576c2ba.png)

「→インストール」をクリックしてください。

![「→インストール」が表示されたところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/746cacc2746d4653b790b32faf32e72e.png)

Pleasanter MCPエンドポイントURLとAPIキーを設定し「保存」ボタンをクリックしてください。

![Pleasanter MCP の設定画面。エンドポイントURLとAPIキーを入力し「保存」ボタンがある](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/38a0d6d1e7ce4fa593c9cd687e4a9593.png)

Pleasanter MCPエンドポイントURLには、以下のようなURLを設定してください。

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

スイッチをクリックして「有効」に切り替え、「設定」ボタンをクリックしてください。

![拡張機能の一覧。スイッチを「有効」に切り替え、「設定」ボタンがある](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/223fd5f16ea34b6ebaa85de47cb5d6ba.png)

Pleasanter MCPで利用できる「ツール」の一覧が表示されます。一覧ではツールがアルファベット昇順で表示されます。

![Pleasanter MCP で使えるツールの一覧。アルファベット昇順で並んでいる](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/4a2213f7d15b4b84a18f14d856b244ec.png)

一覧の右上に表示されるドロップダウンメニューでは、すべてのツールの利用権限を一括設定できます。ツール毎に権限を設定したい場合は、各ツール名の右側に表示されているボタンで設定してください。

|                     アイコン                     | 選択肢       | 意味                                               |
| :----------------------------------------------: | :----------- | :------------------------------------------------- |
| ![「常に許可」のアイコン](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/4ac43886fe7b40cbbd95bc106e5c31b0.png) | 常に許可     | すべてのツールの利用を常に承認します。             |
| ![「承認が必要」のアイコン](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/d5c0d85bd1d347deb65860e48e6070ac.png) | 承認が必要   | すべてのツールの初回利用時にユーザ承認を求めます。 |
| ![「ブロック済み」のアイコン](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/5a79ff86740a4df6853a565288cd9f8b.png) | ブロック済み | すべてのツールの利用をブロックします。             |
| ![「カスタム」のアイコン](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/e9adabdd38944785a33374d0b3c1e0a9.png) | カスタム     | ツールごとに異なる権限設定を適用します。           |

デフォルトでは、すべてのツールについて「承認が必要」が設定されています。

### Claude Desktopの終了

拡張機能の設定が済んだら、変更を反映するためにClaude Desktopを完全に終了します。Claude Desktopを完全に終了するには、タスクトレイから「終了」を選択する必要があります。

![タスクトレイの Claude Desktop のメニュー。「終了」が選べる](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/f167470a54f74f38988cc9bf001f9a41.png)

### Claude Desktopの動作確認

Claude Desktopを起動し、新規チャットを開いて（++ctrl+shift+o++）、以下のメッセージを入力してください。

``` text
プリザンターのMCPで使えるツールを教えてください。
```

以下のように表示されれば、初期設定は完了です。AIの性質上、同じ質問をしても、同じ回答を得られる保証はないことに注意してください。

![Claude Desktop のチャットで、Pleasanter MCP を使った回答が返ってきたところ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/3fb04a5328f54a73b0a5f0c14886c50a.png)

### Claudeのプランに関する補足情報

Pleasanter MCPは「Free Claude」（無料）プランでも利用可能です。各プランにはClaude Desktopの開発元であるAnthropic社が定める使用量制限があり、使用量が上限に達すると以下のようなメッセージが表示されます。

![使用量が上限に達したときに表示されるメッセージ](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/8cb6778c45954154879daedc9f70b330.png)

このような場合には、①表示された時間まで待つ、②エクストラ使用量オプション（有料）を有効化する、③契約プランを見直すなどすることで再度操作できるようになります。

詳細については、Claude Desktopのヘルプを参照してください。

![Claude Desktop の使用量に関する画面](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/e313eadb59f64b6c8317aa02a012f177.png)

## 注意事項

1. AIが生成する回答には誤りが含まれる可能性があります。回答内容は必ず確認してください。
1. このマニュアルはプリザンター1.5.3.0リリース時のClaude Desktop（Claude for Windows）に基づきます。
1. Claude Desktopは頻繁にバージョンアップされており、画面の一部が変更されることがあります。適宜読み替えをお願いいたします。

## 対応バージョン

| 対応バージョン | 内容                                         |
| :------------- | :------------------------------------------- |
| 1.5.2.0 以降   | 機能追加                                     |
| 1.5.3.0 以降   | レコードの新規作成、レコードの削除機能を追加 |

## 関連情報

-   [Pleasanter MCPを使う](index.md)
