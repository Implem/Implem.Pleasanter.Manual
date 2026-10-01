---
title: ユーザ招待
category: ユーザ管理機能
order: '20'
status: ''
parts: ''
urlstring: user-invite
translationKey: user-invite
shortname: ユーザ招待
created: 2019-08-06
updated: 2026-06-15
---

## 概要

ユーザ招待機能は、ユーザへ招待メールを送付し承認する仕組みです。承認されたユーザはプリザンターを利用できます。

**このページに記載された内容はオープンソース版での操作となります。pleasanter.netをご利用の場合は招待方法が異なります。以下のPleasanterダウンロードセンターから「Pleasanter.netスタートガイド」をダウンロードしていただき「ユーザの招待」の項目を確認してください。**  

-   ダウンロードセンター  
    [https://pleasanter.org/dlcenter](https://pleasanter.org/dlcenter)

## 事前準備

1.  [特権ユーザ](user-management-privileged-users.md)のみユーザ承認が可能です。[[パラメータ設定：Security.json](../../setup/parameters/security-json.md)]を参考にして[特権ユーザ](user-management-privileged-users.md)を設定します。
1.  [[パラメータ設定：Registration.json](../../setup/parameters/registration-json.md)]を参考にしてパラメータ設定をします。  

## ユーザの招待

任意のユーザへ招待メールを送信します。

1.  「管理」メニューを開き「ユーザ招待」をクリックします。
1.  「新規作成」ボタンをクリックします。
1.  「メールアドレス」欄に招待したいユーザのメールアドレスを入力します。
1.  「招待」ボタンをクリックします。
1.  指定したメールアドレスへ招待メールが送信されます。

## 招待されたユーザの承認依頼

招待されたユーザは必要情報を入力し、承認者へ承認依頼メールを送信します。

1.  招待メールの本文に記載されているリンクをクリックし、Webサイトにアクセスします。
1.  「名前」、「パスワード」等の必要情報を入力します。
1.  「承認依頼」ボタンをクリックします。
1.  承認依頼メールが送信されます。

 承認依頼メールは、[Registration.jsonの設定](../../setup/parameters/registration-json.md)で設定したメールアドレスに送信されます。

## ユーザの承認

承認者は、招待されたユーザからの承認依頼を承認します。

1.  承認依頼メールの本文に記載されているリンクをクリックし、Webサイトにアクセスします。
1.  「承認」ボタンをクリックします。
1.  承認依頼中のユーザへ承認メールが送信されます。

[特権ユーザ](user-management-privileged-users.md)以外は承認ボタンが非表示となります。

## プリザンターへのログイン

招待されたユーザがプリザンターへログインします。

1.  承認メールの本文に記載されているリンクをクリックします。
1.  プリザンターのログイン画面が表示されます。
1.  メールアドレスと先ほど設定したパスワードでログインします。
1.  プリザンターのTOP画面が表示されます。

## 関連情報

-   [ユーザ管理機能：特権ユーザの設定](user-management-privileged-users.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
-   [パラメータ設定：Registration.json](../../setup/parameters/registration-json.md)
