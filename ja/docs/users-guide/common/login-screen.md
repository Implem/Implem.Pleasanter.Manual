---
title: ログイン画面
category: 共通機能
order: '0'
status: ''
parts: ''
urlstring: login-screen
translationKey: login-screen
shortname: ''
created: 2025-09-25
updated: 2025-10-24
---

## 概要

ログイン画面は、プリザンターにアクセスしたときに表示される画面です。「ログインID」と「パスワード」をプリザンターへ送信することで、アクセスが登録済みのユーザによるものであることを証明します。「ログイン情報を記憶」はログインID、パスワード、二段階認証の確認コードを記憶する機能ではありません。

![ログインIDとパスワードを入力するログイン画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/a11e5b5e762145efb1245df5c679a5bb.png)

### ログイン情報を記憶

「ログイン情報を記憶」をオンにすると、ログインセッションを管理するCookie情報が保持され、いったんブラウザを終了させても、その後のブラウザ起動によりログインが継続されます。

Cookie情報の保持期間は、[Session.json](../../setup/parameters/session-json.md)のRetentionPeriodで設定できます。

## 操作手順

ローカル認証によるログインを行います。

1. ログインIDとパスワードを入力してください。
1. 必要に応じて「ログイン情報を記憶」をオンにしてください。
1. ログインボタンをクリックしてください。

ローカル認証以外の認証方式については、[応用編：認証](../hands-on/advanced/advanced-operations-authentication.md)をご覧ください。
