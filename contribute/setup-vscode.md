# Visual Studio Codeのセットアップ

プリザンターユーザマニュアルでは、マニュアルデータの編集にVisual Studio Codeを使用します。

> [!note]
> **WSL で作業する場合**は、Windows 側に入れた Visual Studio Code から拡張機能「WSL」で接続し、WSL 側のディレクトリを開きます。拡張機能は**接続先（WSL 側）にも入れる**必要があります。

PowerShellを起動し、下記コマンドを実行してください。

``` ps1
winget install --id Microsoft.VisualStudioCode -e --source winget
```

> [!note]
> Visual Studio Codeのセットアップ時、PowerShellなどから`code`コマンドで実行できるように設定しておくと便利です。

## 拡張機能のセットアップ

Visual Studio Codeを使用する場合、以下の拡張機能をインストールすることで、マニュアル執筆の手間を軽減できます。

ショートカットキーCtrl＋Shift＋Xを押下し、以下の拡張機能名を入力して、インストールしてください。

| 拡張機能名                                        | 概要                                                                                       |
| :------------------------------------------------ | :----------------------------------------------------------------------------------------- |
| [Japanese Language Pack for Visual Studio Code][] | Visual Studio Codeのユーザインターフェイスを日本語化します。                               |
| [EditorConfig][]                                  | インデント、文字エンコーディング形式、改行コードなどをプロジェクト推奨値に自動設定します。 |
| [markdownlint][]                                  | Markdownのマークアップを検証したり、自動修正したりします。                                 |
| [Markdown Table][]                                | プリザンターユーザマニュアルで多用されるテーブルの作成・整形を支援します。                 |
| [YAML][]                                          | 設定ファイルの編集を支援します。                                                           |

[Japanese Language Pack for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ja
[EditorConfig]: https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig
[markdownlint]: https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint
[Markdown Table]: https://marketplace.visualstudio.com/items?itemName=TakumiI.markdowntable
[YAML]: https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml

> [!warning]
> 名前がよく似た別の拡張機能をインストールしないように注意してください。完全な名前で検索し、間違いがないことを確認してください。

## Visual Studio Codeでプロジェクトディレクトリを開く

プロジェクトディレクトリへ移動し、`code .`と実行すると、Visual Studio Codeでプロジェクトディレクトリを開けます。WSL のシェルで実行すれば、WSL に接続した状態で開きます。

``` ps1
cd Implem.Pleasanter.Manual
code .
```
