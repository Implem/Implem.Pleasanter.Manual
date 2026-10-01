---
title: サーバスクリプトのエラーログを出力したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-server-script-log
translationKey: faq-server-script-log
shortname: FAQ：サーバスクリプトのエラーログを出力したい
created: 2021-02-22
updated: 2026-02-10
---

## 回答

複数の方法があるため、エラーログの取得目的に応じて使い分けてください。

---

## 概要

[サーバスクリプト](../../developers-guide/server-script/index.md)でエラーが発生すると、コマンドボタンエリアの上にエラーメッセージが表示され、エラーの内容は[システムログ](../../managers-guide/system-log-administration/index.md)に記録されます。しかし、[システムログ](../../managers-guide/system-log-administration/index.md)は特権ユーザでないと閲覧することができません。

プリザンターは特権ユーザでないユーザがエラーの内容を確認する方法を複数用意しています。エラーログの取得目的に応じて使い分けてください。

### 1. 予見可能なエラー（例外）をログ出力する 

try-catchとログ出力メソッドを使用します。この場合、以下で説明する「エラーの詳細を取得する」は無視されます。

#### ログ出力メソッド

ログの出力先別に、以下のログ出力メソッドを使い分けてください。

|出力先|メソッド|
|:--|:--|
|以下の一方または両方<br><br>・開発者ツールのコンソール<br>・システムログ|[logs.LogException](../../developers-guide/server-script/logs/server-script-logs-log-exception.md)|
|・開発者ツールのコンソール|[context.Log](../../developers-guide/server-script/context/server-script-context-log.md)|

#### サンプルコード

```js
try {
    context.Log('処理開始');
    const myItems = items.Get('aaaa');  // 引数に文字列を渡す
    const myItem = myItems[0];    // myItemsがnullなのに配列要素を指定→エラー
    context.Log(myItem.Title);
    context.Log('処理終了');
} catch(e) {
    context.Log('エラー発生');
    // エラーログ出力
    context.Log(e.stack);    
}
```

#### TryCatch

[サーバスクリプト](../../developers-guide/server-script/index.md)画面の[TryCatch](../../developers-guide/server-script/basics/server-script-try-catch.md)を有効化すると、記述したコードをtryブロックに設定し、catchブロックではエラー内容を[logs.LogException](../../developers-guide/server-script/logs/server-script-logs-log-exception.md)にて出力する処理を設定します。これによりエラー内容をブラウザの管理者ツール上のコンソールに表示するとともにシステムログに記録します。

#### ログ出力サンプル

出力されたログはブラウザの開発者ツールのConsoleに、以下のように出力されます。  
開発者ツールは、Chromeなど代表的なブラウザでF12キーを押下したときに表示される画面です。

![ブラウザの開発者ツールのConsoleにログが出力されている状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/80e03a972d0148b88a4b509ed136dc9a.png)

### 2. 予見不可能なエラーをログ出力する

[テーブルの管理](../../managers-guide/manage-table/index.md)画面の[サーバスクリプト](../../developers-guide/server-script/index.md)タブにある「エラーの詳細を取得する」を有効化してください。

エラー発生時に「開発者ツール」の「コンソール」画面から[サーバスクリプトのデバッグ](../../developers-guide/server-script/basics/server-script-debug.md)に役立つ情報を得られます。本機能は、無効化されていない全てのサーバスクリプトが対象となります。

#### サンプルコード

以下のサンプルコードは上記サンプルコードの3行目～5行目と同じです。  

```js
const myItems = items.Get('aaaa');  // 引数に文字列を渡す
const myItem = myItems[0];    // myItemsがnullなのに配列要素を指定→エラー
context.Log(myItem.Title);
```

条件に「作成後」を設定し、レコードを新規作成すると、以下のように表示されます。

![レコードの新規作成時にエラーの内容がConsoleに出力された状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/53dff3adfb584aac8f0c6b6d4d87d2fc.png)

サーバスクリプトの[条件](../../developers-guide/server-script/basics/server-script-conditions.md)として、「サイト設定の読み込み時」「ビュー処理時」「レコード読み込み時」などを指定した場合は、エラーページ（/errors/serverscripterror）へのリダイレクトが発生します。このような場合はコンソールにエラーの詳細は出力されません。

「エラーの詳細を取得する」を有効化した場合、try-catch文で補足した例外は出力されません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.1.0 以降|「エラーの詳細を取得する」の実装に合わせて更新|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [システムログ管理機能](../../managers-guide/system-log-administration/index.md)
-   [開発者ガイド：サーバスクリプト：logs.LogException](../../developers-guide/server-script/logs/server-script-logs-log-exception.md)
-   [開発者ガイド：サーバスクリプト：context.Log](../../developers-guide/server-script/context/server-script-context-log.md)
-   [開発者ガイド：サーバスクリプト：TryCatch](../../developers-guide/server-script/basics/server-script-try-catch.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [開発者ガイド：サーバスクリプト：デバッグ](../../developers-guide/server-script/basics/server-script-debug.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../editor/faq-condition-mode-range.md)