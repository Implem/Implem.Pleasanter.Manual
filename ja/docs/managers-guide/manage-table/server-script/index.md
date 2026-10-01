---
title: サーバスクリプト
category: 開発者ガイド
order: '3'
status: ''
parts: ''
urlstring: table-management-server-script
translationKey: table-management-server-script
shortname: サーバスクリプト
created: 2020-11-26
updated: 2026-02-10
---

## 概要

[サーバスクリプト](../../../developers-guide/server-script/index.md)機能を使うことで、クライアントサイドで実行される従来の[スクリプト](../scripts/index.md)機能では実現できなかった条件分岐や複雑な計算をシンプルなコードで実現できます。また、クライアントサイドで実行される[スクリプト](../scripts/index.md)機能とは異なり、[サーバスクリプト](../../../developers-guide/server-script/index.md)機能はインポートでのレコード追加・更新やAPIによる操作のタイミングでも実行されます。

このページでは、[テーブルの管理](../index.md)画面の[サーバスクリプト](../../../developers-guide/server-script/index.md)タブの機能を紹介します。[サーバスクリプト](../../../developers-guide/server-script/index.md)の作成方法や編集方法は、[サーバスクリプト：新規作成と編集](../../../developers-guide/server-script/basics/server-script-create-edit.md)を確認してください。

## 前提条件

1.  サイトの管理権限が必要です。

## 操作手順

### 一覧の操作

[テーブルの管理](../index.md)の[サーバスクリプト](../../../developers-guide/server-script/index.md)タブには、開発者が作成・追加したサーバスクリプトの一覧が表示されます。一覧のサーバスクリプトは上から順に読み込まれます。

![テーブルの管理の「サーバスクリプト」タブに並ぶスクリプトの一覧](https://pleasanter.org/files/images/ja/managers-guide/manage-table/server-script/assets/aa771d752f074ce7830523f867bc552c.png)

一覧の左端に表示されたチェックボックスでサーバスクリプトを選択することで、以下の操作を行えます。

|                No                 | ボタン名 | 機能                                                                                                                                                             |
| :-------------------------------: | :------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span class="pl-callout">❶</span> |    上    | 選択したサーバスクリプトを1つ上に移動します。                                                                                                                    |
| <span class="pl-callout">➋</span> |    下    | 選択したサーバスクリプトを1つ下に移動します。                                                                                                                    |
| <span class="pl-callout">❸</span> |  コピー  | 選択したサーバスクリプトを複製します。<br>複製されたサーバスクリプトは一覧の一番下へ追加されます。                                                               |
| <span class="pl-callout">➍</span> |   削除   | 選択したサーバスクリプトを一覧から削除します。<br>削除ボタンをクリックすると、確認ダイアログが表示されます。<br>OKボタンをクリックすると、一覧から削除されます。 |

### 作成・追加済みサーバスクリプトの編集

一覧の各行をクリックすると、作成・追加済みのサーバスクリプトを編集できます。詳細は[サーバスクリプト：新規作成と編集](../../../developers-guide/server-script/basics/server-script-create-edit.md)を確認してください。

### 新規作成

一覧の上に表示される「新規作成」ボタンをクリックすると、サーバスクリプトを新規作成し、一覧へ追加できます。詳細は[サーバスクリプト：新規作成と編集](../../../developers-guide/server-script/basics/server-script-create-edit.md)を確認してください。

### 全て無効化

一覧の上に表示される「全て無効化」チェックボックスを有効化すると、一覧に表示されている全てのサーバスクリプトを無効化できます。

「全て無効化」を有効化しても、各サーバスクリプトの「無効」チェックボックスの状態（一覧の「無効」列で確認できます）は変わりません。

### エラーの詳細を取得する

本機能は開発者向けの機能です。詳細は[FAQ：サーバスクリプトのエラーログを出力したい](../../../FAQ/features-for-developers/faq-server-script-log.md)を確認してください。

## 対応バージョン

| 対応バージョン | 内容                                 |
| :------------- | :----------------------------------- |
| 1.4.14.0 以降  | 「全て無効化」機能を追加             |
| 1.5.1.0 以降   | 「エラーの詳細を取得する」機能を追加 |

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [テーブルの管理：スクリプト](../scripts/index.md)
-   [テーブルの管理](../index.md)
-   [開発者ガイド：サーバスクリプト：新規作成と編集](../../../developers-guide/server-script/basics/server-script-create-edit.md)
-   [FAQ：サーバスクリプトのエラーログを出力したい](../../../FAQ/features-for-developers/faq-server-script-log.md)
