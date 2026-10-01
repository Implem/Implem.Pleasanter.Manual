---
title: 関数化
category: サーバスクリプト
order: '600'
status: ''
parts: ''
urlstring: server-script-functionalize
translationKey: server-script-functionalize
shortname: 関数化
created: 2025-01-06
updated: 2026-05-12
---

## 概要

[サーバスクリプト](../index.md)で記述したコードを自動的に無名関数化する機能です。無名関数化することで、コード上で「return;」と記述した箇所でサーバスクリプトを中断できるようになります。

## 制限事項

1. [TryCatch](server-script-try-catch.md)と「関数化」を同時にチェックした場合は、無名関数化したうえでtry-catch文へ変換します。
1. 「関数化」チェックOFFで「return;」を記述するとアプリケーションエラーとなります。（エラー内容は SyntaxError: Illegal return statement です）
1. [条件](../../../FAQ/editor/faq-condition-mode-range.md)で「共有」をオンにしたサーバスクリプトでは「関数化」の設定は適用されません。

## 実施例

### 設定内容

##### JavaScript

```
// 先行の処理
context.Log('先行の処理');
// 数値Aと数値Bの大小チェック
if (model.NumA > model.NumB) {
    context.Log('数値Bには数値Aより大きい値を入力してください。');
    return;
}
// 後続の処理
context.Log('後続の処理');
```

### 「関数化」チェックONにより変換されて実行するサーバスクリプト

##### JavaScript

```
(() => {
    // 先行の処理
    context.Log('先行の処理');
    // 数値Aと数値Bの大小チェック
    if (model.NumA > model.NumB) {
        context.Log('数値Bには数値Aより大きい値を入力してください。');
        return;
    }
    // 後続の処理
    context.Log('後続の処理');
})();
```

### 実行結果

#### 数値A：10、数値B：100の場合

![数値A：10、数値B：100の場合の実行結果](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/b3b057606afd47cf8fd05f7c051dd2f7.png)

#### 数値A：101、数値B：100の場合

![数値A：101、数値B：100の場合の実行結果](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/7a95e43310f64a61a95bccaa34e9cd54.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：TryCatch](server-script-try-catch.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)