---
title: デバッグ
category: サーバスクリプト
order: '500'
status: ''
parts: ''
urlstring: server-script-debug
translationKey: server-script-debug
shortname: サーバスクリプトのデバッグ
created: 2021-11-02
updated: 2026-05-12
---

## 概要

Visual Studio Codeを使用して[サーバスクリプト](../index.md)のラインデバッグを行う方法を説明します。

## 制限事項

1. デバッグ中はデバッガに接続するまでスクリプトが途中で停止しテーブルを利用できません。本番環境では使用しないでください。
1. サーバスクリプトの種類によってデバッグできない場合があります。

    |コードの種類|本手順によるデバッグの可否|
    |:---|:---|
    |「テーブルの管理：サーバスクリプト」|可能|
    |「テナント管理機能：バックグラウンドサーバスクリプト」|不可能|
    |[ExtendedServerScriptsフォルダ配下の拡張サーバスクリプト](../../extended-features/extended-server-script.md)|可能|
    |[Pleasanter Code Assistで追加した拡張サーバスクリプト](../../../products-info/pleasanter-extensions/pleasanter-code-assist/pleasanter-code-assist-how-to-use-extensions.md)|不可能|

1. [条件](../../../FAQ/editor/faq-condition-mode-range.md)で「共有」のチェックをオンにしたサーバスクリプトでは、本ページの方法でデバッグを行うことはできません。

## 前提条件

1. プリザンターが稼働するサーバのポート9222が開いている必要があります。
1. デバッグを行うPCにVisual Studio Codeがインストールされている必要があります。

## 操作手順

1. 任意の作業用フォルダを作成します。※ここではworkフォルダとします。
1. 上記フォルダ内に.vscodeフォルダを作成します。
1. 上記.vscodeフォルダ内にlaunch.jsonを作成します。
1. Visual Studio Codeを起動し、workフォルダを開きます。※Visual Studio Codeでworkフォルダを開くと、左側のEXPLORERは以下のようになります。
![workフォルダを開いたVisual Studio CodeのEXPLORER](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/024f47dd871a44b8a2ef1f345b43ef1d.png)
1. launch.jsonのaddressをサーバのアドレスに変更します。
1. ブラウザでプリザンターにアクセスしデバッグする[サーバスクリプト](../index.md)の内容の先頭行に、//debug// を記述し保存します。
1. デバッグする[テーブル](../../../users-guide/table/index.md)を開きます。サーバスクリプトがデバッグモードで待機状態となり画面の応答が無い状態になります。
1. Visual Studio Codeで Run → Start Debugging と操作します。
1. Visual Studio Code上にソースコードが読み込まれラインデバッグが可能となります。

## launch.json

デバッグするプリザンターが動作する環境への接続情報です。addressは適宜変更する必要があります。ローカルPC上にプリザンターがある場合にはlocalhostを指定します。

##### JSON

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach to ClearScript V8 on port 9222",
            "type": "node",
            "request": "attach",
            "protocol": "inspector",
            "address": "192.168.1.101",
            "port": 9222
        }
    ]
}
```

## デバッグするスクリプトの例

先頭に //debug// を記述することで、このスクリプトが動作するタイミングで待機状態となります。デバッグ時以外は //debug// を除去してください。下のサーバスクリプト例では、context.Log()メソッドによりブラウザの開発者ツールのコンソールにログ出力されます。

##### JavaScript

```
//debug//
if (context.UserId === 1) {
    context.Log('User ID is 1');
} else {
    context.Log('User ID is not 1');
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [ExtendedServerScriptsフォルダ配下の拡張サーバスクリプト](../../extended-features/extended-server-script.md)
-   [Pleasanter Code Assistで追加した拡張サーバスクリプト](../../../products-info/pleasanter-extensions/pleasanter-code-assist/pleasanter-code-assist-how-to-use-extensions.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [テーブル機能](../../../users-guide/table/index.md)