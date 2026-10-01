---
title: コードの共有
category: サーバスクリプト
order: '1400'
status: ''
parts: ''
urlstring: server-script-shared
translationKey: server-script-shared
shortname: コードの共有
created: 2021-10-18
updated: 2026-05-12
---

## 概要

[サーバスクリプト](../index.md)のコードを共有化する機能です。[サーバスクリプト](../index.md)の条件にある共有のチェックをオンにすることで、その他のサーバスクリプトの先頭にコードが読み込まれます。

## 制限事項

1. 実行時は、各サーバスクリプトの[TryCatch](server-script-try-catch.md)、[関数化](server-script-functionalize.md)の設定に従って実行コードが生成され、共有コードがその先頭へ差し込まれます。
1. 「共有」のチェックをオンにしたサーバスクリプトに、[TryCatch](server-script-try-catch.md)、[関数化](server-script-functionalize.md)、//debug//（[サーバスクリプトのデバッグ](server-script-debug.md)を参照）の設定は適用されません。
1. 「共有」のチェックをオンにしたサーバスクリプトで[TryCatch](server-script-try-catch.md)や[関数化](server-script-functionalize.md)を設定したい場合は、コードに直接try-catch句や無名関数化の記述をしてください。ただしブロックスコープとなるため呼び出す側のサーバスクリプトで参照できなくなる恐れがありますので、十分に検証を行ってください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.37.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：TryCatch](server-script-try-catch.md)
-   [開発者ガイド：サーバスクリプト：関数化](server-script-functionalize.md)
-   [開発者ガイド：サーバスクリプト：デバッグ](server-script-debug.md)