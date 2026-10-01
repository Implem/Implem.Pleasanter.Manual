---
title: Pleasanter MCPを使う
category: Pleasanter MCP
order: '100'
status: ''
parts: ''
urlstring: pleasanter-mcp
translationKey: pleasanter-mcp
shortname: Pleasanter MCPを使う,Pleasanter MCP
created: 2026-02-25
updated: 2026-09-08
---

## 概要

### Pleasanter MCPとは

Pleasanter MCPは、プリザンターに統合されたModel Context Protocol（MCP）サーバ機能です。

![Pleasanter MCP の位置づけを示した図](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/d6590a7beada42eda98d20493fa8c4ec.png)

Pleasanter MCPを利用することで、ユーザはプリザンターのUIやAPIを使うことなく、プリザンター内のデータをよりスマートに利活用できるようになります。たとえば、社内SEに依頼するときのような自然なことばで、AIエージェントやコードエディタに対して、複雑なタスクを依頼できます。

![Pleasanter MCP を使うと、自然なことばでプリザンターのデータを扱えることを示した図](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/cad776ea9db0450db660ec28b2809ca3.png)

### Pleasanter MCPでできること

プリザンター1.5.8.0リリース時点で、Pleasanter MCPは以下の機能をサポートしています。

1. サイト情報の取得
1. サイトテンプレートの一覧取得
1. サイトテンプレートを用いたサイトの新規作成
1. レコードの新規作成・取得・更新・削除
1. ビューの新規作成・取得・更新・コピー・削除
1. ユーザ情報の取得
1. レコードに関連するメールを送信

上記の機能は、Pleasanter MCP内の抽象的な概念である「ツール」を通して提供されます。Pleasanter MCPを利用する際、ユーザがツールの存在を意識する必要はありませんが、Pleasanter MCPでできることはツールの機能により決まります。

プリザンター1.5.8.0リリース時点で利用できるツールは以下の通りです[^1][^2][^3]。

<figure>
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
            <td rowspan="6">レコード操作系</td>
            <td>GetItems</td>
            <td>サイト内のレコード一覧を取得</td>
        </tr>
        <tr>
            <td>AddItem</td>
            <td>レコードの新規作成</td>
        </tr>
        <tr>
            <td>GetItem</td>
            <td>単一レコードの詳細を取得</td>
        </tr>
        <tr>
            <td>UpdateItem</td>
            <td>レコードを更新</td>
        </tr>
        <tr>
            <td>CreateItemJson</td>
            <td>更新用JSONを生成（日本語→コード変換）</td>
        </tr>
        <tr>
            <td>DeleteItem</td>
            <td>レコードを削除</td>
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
            <td>サイトテンプレートを用いたサイトの新規作成</td>
            <td>AddSiteByTemplate</td>
            <td>サイトテンプレートを用いて指定フォルダ内へサイトを新規作成</td>
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
            <td rowspan="7">ビュー操作系</td>
            <td>CreateViewJson</td>
            <td>検索条件のView JSONを作成</td>
        </tr>
        <tr>
            <td>AddView</td>
            <td>サイトにビューを新規作成</td>
        </tr>
        <tr>
            <td>GetView</td>
            <td>ビュー設定を取得</td>
        </tr>
        <tr>
            <td>GetViewIdByViewName</td>
            <td>ビュー名からビューIDを検索</td>
        </tr>
        <tr>
            <td>UpdateView</td>
            <td>ビューを更新</td>
        </tr>
        <tr>
            <td>CopyView</td>
            <td>ビューをコピー</td>
        </tr>
        <tr>
            <td>DeleteView</td>
            <td>ビューを削除</td>
        </tr>
        <tr>
            <td>メール送信系</td>
            <td>SendEmail</td>
            <td>レコードに関連するメールを送信<br>（添付ファイル未対応）</td>
        </tr>
    </tbody>
</table>
</figure>

[^1]: AddItemツールとDeleteItemツールは、プリザンター1.5.3.0以降で利用できます。
[^2]: CreateItemJsonツールはプリザンター1.5.3.0以降でツール名を変更しています（旧ツール名：CreateUpdateItemJson）。
[^3]: GetSiteTemplatesツールとAddSiteByTemplateツールはプリザンター1.5.8.0以降で利用できます。

### Pleasanter MCP はじめてのMCPガイド

各部門における活用提案などは、以下のPDFドキュメントを参照してください。  
[Pleasanter MCP はじめてのMCPガイド](https://pleasanter.org/downloads/pleasanter-mcp-guide.pdf)（PDF形式：1.25MB）  
[![「Pleasanter MCP はじめてのMCPガイド」の表紙](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/ef6f69b85f5d4b34b9973027cd6e77e2.png)](https://pleasanter.org/downloads/pleasanter-mcp-guide.pdf)

## Pleasanter MCPのセットアップ

ユーザマニュアルでは、AIエージェントのClaude DesktopとPleasanter MCPを接続する方法に加え、コードエディタのVisual Studio CodeとPleasanter MCPを接続する方法を説明します。Claude Desktopについては、拡張機能を使う方法に加え、より汎用的な設定ファイルを使う方法を説明します。セットアップ方法の詳細は、以下の各ページを確認してください。

1. [Pleasanter MCPをClaude Desktopで使う（拡張機能）](pleasanter-mcp-claude-extensions.md)
1. [Pleasanter MCPをClaude Desktopで使う（設定ファイル）](pleasanter-mcp-claude-config.md)
1. [Pleasanter MCPをVisual Studio Codeで使う](pleasanter-mcp-vscode.md)

どのパターンを選んだ場合でも、以下のプリザンターの設定は必須です。

## プリザンターの設定

プリザンターでは設定ファイルの編集と、APIキーの発行が必要です。

### Pleasanter MCPの有効化

Pleasanter MCPを利用するには、設定ファイル[McpServer.json](../../setup/parameters/mcpserver-json.md)のパラメータEnabledをtrueに設定し、プリザンターを再起動してください。

``` json title="McpServer.json" linenums="1" hl_lines="2"
{
    "Enabled": true,
        ： 中略
}
```

Enabled以外のパラメータについては、[McpServer.json](../../setup/parameters/mcpserver-json.md)のマニュアルを確認してください。

### APIキーの発行

以下の手順で、APIキーを発行してください。<span class="pl-attention">APIキーが漏洩すると外部プログラムからのアクセスが可能となります。APIキーは他者に知られないよう、厳重に管理してください。</span>

1.  Pleasanter MCPを利用するユーザでプリザンターへログインしてください。
1.  ナビゲーションメニューで「[ユーザ](../../managers-guide/user-administration/index.md)」を選択してください。
1.  「API設定」をクリックしてください。
1.  「作成」ボタンをクリックしてください。
1.  表示されたAPIキーを控えてください。

![発行された API キーが表示された画面](https://pleasanter.org/files/images/ja/ai-integration/pleasanter-mcp/assets/f817c80e487e4f61ac1f9d95ecb4be1c.png)

## 対応バージョン

| 対応バージョン | 内容                                                                           |
| :------------- | :----------------------------------------------------------------------------- |
| 1.5.2.0 以降   | 機能追加                                                                       |
| 1.5.3.0 以降   | レコードの新規作成、レコードの削除機能を追加                                   |
| 1.5.8.0 以降   | サイトテンプレートの情報取得、サイトテンプレートを用いたサイトの新規作成を追加 |

## 関連情報

-   [Pleasanter MCP はじめてのMCPガイド](https://pleasanter.org/downloads/pleasanter-mcp-guide.pdf)
-   [Pleasanter MCPをClaude Desktopで使う（拡張機能）](pleasanter-mcp-claude-extensions.md)
-   [Pleasanter MCPをClaude Desktopで使う（設定ファイル）](pleasanter-mcp-claude-config.md)
-   [Pleasanter MCPをVisual Studio Codeで使う](pleasanter-mcp-vscode.md)
-   [Pleasanter MCPをその他のAIエージェントで使う](pleasanter-mcp-other-agents.md)
-   [Pleasanter MCPを運用する](pleasanter-mcp-maintenance.md)
-   [パラメータ設定：McpServer.json](../../setup/parameters/mcpserver-json.md)
