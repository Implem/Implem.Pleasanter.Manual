---
title: インクルード
category: サーバスクリプト
order: '1500'
status: ''
parts: ''
urlstring: server-script-include
translationKey: server-script-include
shortname: インクルード
created: 2021-10-17
updated: 2025-01-30
---

## 概要

[拡張サーバスクリプト](../../extended-features/extended-server-script.md)などの[サーバスクリプト](../index.md)の共通コードをインクルードする機能です。//Include命令を[サーバスクリプト](../index.md)の任意の位置に記述して使用します。共通関数などを定義しておくことで、コードの一元管理が可能になります。

## 使用例

下記の例では Name が "ServerScriptName" の[拡張サーバスクリプト](../../extended-features/extended-server-script.md)を読み込み // Include を記述した位置に挿入します。
※事前に Name が "ServerScriptName" の[拡張サーバスクリプト](../../extended-features/extended-server-script.md)のファイル(JSON)を配置しておく必要があります。

```
//Include: ServerScriptName
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.37.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：拡張機能：拡張サーバスクリプト](../../extended-features/extended-server-script.md)
-   [開発者ガイド：サーバスクリプト](../index.md)