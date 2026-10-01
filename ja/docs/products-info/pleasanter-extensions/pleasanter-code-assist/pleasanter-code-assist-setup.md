---
title: セットアップ、事前準備
category: Pleasanter Code Assist
order: '2000'
status: ''
parts: ''
urlstring: pleasanter-code-assist-setup
translationKey: pleasanter-code-assist-setup
shortname: Pleasanter Code Assist,セットアップ手順
created: 2025-02-17
updated: 2026-03-12
---

## 概要

Pleasanter Code Assistのセットアップおよび事前準備を説明します。

## 手順概要

1. Visual Studio Codeのインストール
1. 拡張機能[Pleasanter Code Assist](pleasanter-code-assist-create-workfolder.md)のインストール
1. 作業フォルダ作成
1. サーバ接続情報ファイル作成

## 1. Visual Studio Codeのインストール

ご利用のクライアント端末にVisual Studio Codeをインストールします。Visual Studio Codeはこちらからダウンロードしてください。
https://code.visualstudio.com/Download
インストール方法は以下公式サイトを確認してください。
https://code.visualstudio.com/docs/setup/setup-overview

## 2. 拡張機能[Pleasanter Code Assist](pleasanter-code-assist-create-workfolder.md)のインストール

1. Visual Studio Codeを起動します。
1. 左側ペインのビューバーより拡張機能アイコンをクリックし、拡張機能サイドバーを開きます。
1. [Pleasanter Code Assist](pleasanter-code-assist-create-workfolder.md)を検索します。
1. 検索結果で、インストール ボタンをクリックします。
![拡張機能サイドバーでPleasanter Code Assistを検索した結果](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/f0310d47db25499d8a607fe5433ebac7.png)
1. 以下のようなダイアログが表示した場合は「Trust Publisher & Install」ボタン（日本語表示の場合は「発行元を信頼＆インストール」ボタン）をクリックします。
![「Trust Publisher & Install」ボタンが表示されたダイアログ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/7bbb081d535a42d68a9483a6f82d2b74.png)

## 3. 作業フォルダ作成

作業フォルダ作成用のコマンドを実行して作業フォルダを作成します。手順は以下のページを参照してください。
[Pleasanter Code Assist：コマンドによる作業フォルダ作成](pleasanter-code-assist-create-workfolder.md)
手動で作成する場合は、ご利用の端末の任意のフォルダを「基準フォルダ」とし、その配下に下図の通りの構成でフォルダを作成します。「基準フォルダ」は任意の名称で作成してください。下図では「sampleRoot」が基準フォルダです。
![基準フォルダ「sampleRoot」配下に作るフォルダ構成の図](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/c0db8a29038d4df788c64525033e7b6f.png)

|フォルダ名|説明|
|---|---|
|基準フォルダ（上図ではsampleRoot）|Pleasanter Code Assistを利用する際の基準となるフォルダ。場所、名称は任意。基準フォルダは複数作成することができます。|
|connectionSetting|サーバ接続情報ファイルを格納|
|extensions|拡張スクリプト、拡張サーバスクリプト、拡張SQL、拡張スタイルの各フォルダをまとめる|
|　scripts|拡張スクリプトの定義ファイル、ソースコードファイルを格納|
|　serverscripts|拡張サーバスクリプトの定義ファイル、ソースコードファイルを格納|
|　sqls|拡張SQLの定義ファイル、ソースコードファイルを格納|
|　styles|拡張スタイルの定義ファイル、ソースコードファイルを格納|
|sites|HTML、スクリプト、サーバスクリプト、スタイルの各フォルダをまとめる|
|　htmls|HTMLのソースコードを格納|
|　scripts|スクリプトのソースコードを格納|
|　serverscripts|サーバスクリプトのソースコードを格納|
|　styles|スタイルのソースコードを格納|

Pleasanter Code Assist 1.3.0以降では、scriptsやserverscriptsなどのフォルダ内にサブフォルダを作成し、作成したスクリプトを整理・分類して保存できます。

## 4. サーバ接続情報ファイル作成

connectionSettingsフォルダにサーバ接続情報ファイルを作成します。あらかじめ[APIキー](../../../developers-guide/api/basics/api-key.md)を作成してください。

### ファイル名

任意です。拡張子は".json"です。ファイルは複数作成することができます。
![connectionSettingsフォルダに作成したサーバ接続情報ファイル](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/db423fb2197249fb8b35c868a292aef9.png)

### 設定値

|パラメータ名|設定例|説明|
|---|---|---|
|apiKey|xxxxx...|対象テーブルに対してサイトの管理権限をもつユーザで作成したAPIキーを設定します|
|url|https://servername|プリザンターのルートURLを設定します|

``` json title="設定例" linenums="1"
{
    "apiKey":"xxxxx...",
    "url":"https://servername"
}
```

### プロキシサーバ経由で接続する

プロキシサーバ経由で接続する場合はバージョンによって設定方法が異なりますのでご注意ください。

#### Ver1.2.0以降

Visual Studio Code のデフォルト設定である http.proxy 、http.proxyAuthorizationを設定してください。

#### Ver1.1.0まで

<details markdown="1">
<summary>詳細を見る</summary>
サーバ接続情報ファイルに追加のパラメータを設定してください。

|パラメータ名|設定例|説明|
|---|---|---|
|proxy|JSON|プロキシサーバ経由で接続する場合に設定します。プロキシサーバ未使用時は設定不要です[^1]|
|protocol|https|プロキシサーバへ接続するプロトコルを設定します。httpまたはhttpsを設定します[^1]|
|host|proxy.servername|プロキシサーバのサーバ名を設定します[^1]|
|port|8080|プロキシサーバの接続ポートを設定します[^1]|

``` json title="設定例" linenums="1"
{
    "apiKey":"xxxxx...",
    "url":"https://servername",
    "proxy":{
        "protocol":"https",
        "host":"proxy.servername",
        "port":"8080"
    }
}
```
</details>

[^1]: proxyパラメータは、バージョン1.2.0以降では無効です。

## 関連情報

-   [Pleasanter Code Assist：コマンドによる作業フォルダ作成](pleasanter-code-assist-create-workfolder.md)
-   [開発者ガイド：API：APIキーの作成](../../../developers-guide/api/basics/api-key.md)
