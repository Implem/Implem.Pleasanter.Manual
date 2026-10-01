---
title: 新規作成と編集
category: サーバスクリプト
order: '101'
status: ''
parts: ''
urlstring: server-script-create-run
translationKey: server-script-create-run
shortname: サーバスクリプト：新規作成と編集
created: 2026-01-22
updated: 2026-05-12
---

## 概要

[テーブルの管理](../../../managers-guide/manage-table/index.md)画面の[サーバスクリプト](../index.md)タブで「新規作成」ボタンをクリックすると、[サーバスクリプト](../index.md)画面が表示されます。この画面では、以下の操作を行えます。

1.  サーバスクリプトを新規作成する
1.  作成済みのサーバスクリプトを編集する
1.  作成済みのサーバスクリプトを個別に無効化する

![サーバスクリプト画面。名称やスクリプトなどの設定項目が並ぶ](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/dc6c84eff3e6416694842443d7d13407.png)

| 項目名                                               | 説明                                                                                                                                                                        | 設定方法                         |
| :--------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------- |
| ID                                                   | 各サーバスクリプトへ自動的に割り振られる管理番号                                                                                                                            | ユーザは編集不可                 |
| タイトル                                             | サーバスクリプトのタイトル                                                                                                                                                  | 任意のタイトルを入力             |
| 名称                                                 | サーバスクリプトの名称                                                                                                                                                      | 任意の名称を入力                 |
| スクリプト                                           | サーバスクリプトの内容                                                                                                                                                      | 任意のサーバスクリプトを入力     |
| 無効                                                 | サーバスクリプトを無効にしたい場合チェック                                                                                                                                  | チェックボックスで設定           |
| タイムアウト                                         | サーバスクリプトのタイムアウト時間                                                                                                                                          | タイムアウト時間（ミリ秒）を入力 |
| [関数化](server-script-functionalize.md)      | 無名関数として実行させたい場合にチェック<br>[条件](../../../FAQ/editor/faq-condition-mode-range.md)の「共有」をオンにしたサーバスクリプトでは適用されません                    | チェックボックスで設定           |
| [TryCatch](server-script-try-catch.md)        | 自動的にtry-catch文として変換して実行させたい場合にチェック<br>[条件](../../../FAQ/editor/faq-condition-mode-range.md)の「共有」をオンにしたサーバスクリプトでは適用されません | チェックボックスで設定           |
| [条件](../../../FAQ/editor/faq-condition-mode-range.md) | 実行する条件を選択                                                                                                                                                          | チェックボックスで設定           |

### スクリプト

第2世代[ユーザインターフェースのテーマ](../../../managers-guide/user-administration/user-management-theme.md)を使用している場合は、コードエディタ機能を利用できます。コードエディタ機能は、設定ファイル[General.json](../../../setup/parameters/general.json.md)のパラメータEnableCodeEditorをtrueにすることで利用できます。

![コードエディタ機能を使ったスクリプトの入力欄](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/026e987913094ba0b15461408ba67c57.png)

| コードエディタの機能       | 概要                                             |
| :------------------------- | :----------------------------------------------- |
| シンタックスハイライト     | サーバスクリプトを文法に従って色分け表示します。 |
| コードヒント               | サーバスクリプトの補完入力が有効化されます。     |
| タブキーでのインデント入力 | 適切な量の空白をかんたんに入力できます。         |

### タイムアウト

タイムアウト項目は、既定では画面上に表示されません。設定ファイル[Script.json](../../../setup/parameters/script-json.md)のパラメータServerScriptTimeOutChangeableをtrueにする（有効化する）ことで、画面上に表示されます。

## 対応バージョン

| 対応バージョン | 内容                                                                                                                             |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------- |
| 1.4.12.0 以降  | 無効機能追加<br>[関数化](server-script-functionalize.md)機能追加<br>[TryCatch](server-script-try-catch.md)機能追加 |

## 関連情報

-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：関数化](server-script-functionalize.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [開発者ガイド：サーバスクリプト：TryCatch](server-script-try-catch.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](../../../managers-guide/user-administration/user-management-theme.md)
-   [パラメータ設定：General.json](../../../setup/parameters/general.json.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)
