---
title: TryCatch
category: サーバスクリプト
order: '700'
status: ''
parts: ''
urlstring: server-script-try-catch
translationKey: server-script-try-catch
shortname: TryCatch
created: 2025-01-06
updated: 2026-05-12
---

## 概要

[サーバスクリプト](../index.md)で記述したコードを自動的にtry-catch文として変換して実行する機能です。「TryCatch」チェックをオンにすることで、記述したコードをtryブロックに設定し、catchブロックではエラー内容を[logs.LogException](../logs/server-script-logs-log-exception.md)にて出力する処理を設定します。これによりエラー内容をブラウザの管理者ツール上のコンソールに表示するとともにシステムログに記録します。

## 制限事項

1. 「TryCatch」と[関数化](server-script-functionalize.md)を同時にチェックした場合は、無名関数化したうえでtry-catch文へ変換します。
1. [条件](../../../FAQ/editor/faq-condition-mode-range.md)で「共有」のチェックをオンにしたサーバスクリプトでは、「TryCatch」の設定は適用されません。

## 変換イメージ

### 記述したサーバスクリプト

##### JavaScript

```
// siteId：9999は存在しないサイトID
const siteId = 9999;
const sites = items.Get(siteId);
context.Log(sites[0]);  // 配列のインデックス指定でエラーになる
```

### 「TryCatch」チェックONにより変換されて実行するサーバスクリプト

##### JavaScript

```
try {
    // siteId：9999は存在しないサイトID
    const siteId = 9999;
    const sites = items.Get(siteId);
    context.Log(sites[0]);  // 配列のインデックス指定でエラーになる
} catch(e) {
    log.LogException(※サーバスクリプト情報※\n + e.stack)
}
```
※サーバスクリプト情報※は以下の情報を結合した文字列です。  
固定文字列「(Exception):」、サーバスクリプトのID、タイトル、名称  

## 実施例

### 設定内容

![実施例のサーバスクリプトの設定内容](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/3035785a178d4943ac9bd202616a3bed.png)

### 実行結果

![実施例の実行結果](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/894394f018a04461a5fe2c4ade6c5467.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：logs.LogException](../logs/server-script-logs-log-exception.md)
-   [開発者ガイド：サーバスクリプト：関数化](server-script-functionalize.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)