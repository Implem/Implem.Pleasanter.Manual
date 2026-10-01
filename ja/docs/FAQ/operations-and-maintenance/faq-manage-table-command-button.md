---
title: サーバスクリプト設定後にアプリケーションエラーとなり、テーブルが開けない
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-manage-table-command-button
translationKey: faq-manage-table-command-button
shortname: ''
created: 2022-06-17
updated: 2024-07-01
---

## 回答

[テーブルの管理](../../managers-guide/manage-table/index.md)を開いて[サーバスクリプト](../../developers-guide/server-script/index.md)を修正してください。

---

## 概要

プリザンターでサーバスクリプトなどを設定した際に、「アプリケーションで問題が発生しました。」と表示されテーブルが開けなくなる事があります。このような状態から回復する方法について記載します。

![「アプリケーションで問題が発生しました。」と表示された画面](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/a2230d68f5774758b3d0475a81bce3e0.png)

## 新バージョンでの回復方法

バージョン 1.2.16.0 以降では、アプリケーションエラーが発生した際に[テーブルの管理](../../managers-guide/manage-table/index.md)ボタンが表示され、テーブルの管理画面に移動できます。

### エラーの原因が把握できている場合

サーバスクリプトに構文エラーがある場合には、それを取り除き画面下部の更新ボタンをクリックします。

### エラーの原因が把握できていない場合

サイト設定を変更履歴から元に戻すことができますので、変更履歴タブを開いて元に戻す履歴にチェックを入れ「復元」ボタンをクリックします。テーブルの設定がエラー発生前の内容に戻ります。

## 旧バージョンでの回復方法

バージョン 1.2.16.0 より前のバージョンでは、アプリケーションエラーが発生した際に[テーブルの管理](../../managers-guide/manage-table/index.md)ボタンが表示されませんので、以下の手順によりテーブルの管理画面を開きます。

1. 対象のテーブルのURLを調べます。テーブルを開かずにマウスオーバーすることでブラウザの左下などでURLを確認することができます。
1. 確認したURLの末尾の/indexを除いたURLをブラウザのアドレスバーに直接入力します。URLが「 https://servername/items/2/index 」の場合「 https://servername/items/2 」を入力します。

## 関連項目

-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)