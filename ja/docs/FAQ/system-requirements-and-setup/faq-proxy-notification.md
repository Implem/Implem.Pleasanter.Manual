---
title: プリザンターからの通知などの通信にプロキシを設定したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-proxy-notification
translationKey: faq-proxy-notification
shortname: ''
created: 2025-01-30
updated: 2025-03-21
---

## 回答

システム環境変数を設定し、サーバを再起動してください。

---

## 概要

システム環境変数を設定し、サーバを再起動することで可能となります。

## 制限事項

1.  この設定はバージョン1.4.0.0以降で使用可能です。
1.  この設定はWindowsの場合必要に応じて行います。LinuxやmacOSの場合は不要です。

## 操作手順

1.  スタートメニューから「システム環境変数の編集」を開いてください。

1.  「詳細設定」タブの「環境変数」から環境変数の設定を開きます。

    ![システムのプロパティの詳細設定タブ。「環境変数」ボタンがある](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/8b201c8dbbf343f691712622d9990a5a.png)

1.  「新規」をクリックします。

    ![環境変数の画面。システム環境変数の「新規」ボタンがある](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/67f46cadea25434a9bf03f7a643b07db.png)

1.  以下の通りにシステム環境変数を2つ設定します。

    ![新しいシステム変数の入力画面。HTTP_PROXY を設定する](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/481f5fdf5c9d4798bb6ce3751bbef2f4.png)
    ![新しいシステム変数の入力画面。HTTPS_PROXY を設定する](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/abef5573e2ed403aaec2cedd8ce198ed.png)

    | 変数        | 値                      | 説明                                                      |
    | :---------- | :---------------------- | :-------------------------------------------------------- |
    | HTTP_PROXY  | http://proxyserver:port | http://<プロキシサーバのURL>:<プロキシサーバのポート番号> |
    | HTTPS_PROXY | http://proxyserver:port | http://<プロキシサーバのURL>:<プロキシサーバのポート番号> |

     プロトコルは利用環境に合わせて変更してください。

1.  設定が完了したことを確認し、「OK」をクリックします。

    ![システム環境変数に2つの変数が追加されたことを確認する画面](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/94e5b8e50c7f42448df871baf31a3979.png)

1.  「OK」をクリックします。

    ![システムのプロパティを「OK」で閉じるところ](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/e156388f5b8e4da0938804efd505fd73.png)

1.  サーバを再起動します。
