---
title: 認証
category: 操作ガイド（応用編）
order: '90'
status: ''
parts: ''
urlstring: advanced-operations-authentication
translationKey: advanced-operations-authentication
shortname: 認証
created: 2023-09-12
updated: 2026-04-14
---

## 概要

プリザンターにログインする際の認証機能は以下の通りです。[パラメータ設定：Authentication.json](../../../setup/parameters/authentication-json.md)および[パラメータ設定：Security.json](../../../setup/parameters/security-json.md)で設定します。

1.  ローカル認証
1.  [LDAP認証](../../../setup/additional/authn-authz/active-directory.md)
1.  [SAML認証](../../../setup/additional/authn-authz/saml.md)
1.  [パスキー認証](../../../setup/additional/authn-authz/passkey.md)
1.  二段階認証
    -   [メールによる二段階認証](../../../setup/additional/authn-authz/secondary-authentication.md)
    -   [TOTPによる二段階認証](../../../setup/additional/authn-authz/totp-authentication.md)

## ローカル認証

[ユーザの管理](../../../managers-guide/user-administration/index.md)で登録したユーザ情報のログインID、パスワードで認証を行います。

## LDAP認証

ログインID、パスワードを用いてActive Directory等のLDAPサーバで認証を行います。LDAPサーバがActive Directoryの場合は[統合Windows認証](../../../setup/additional/authn-authz/active-directory-sso.md)によるシングルサインオンも設定可能です。

## SAML認証

SAML認証を行います。SAML認証設定時は専用ボタン（「SSOログイン」ボタン）が表示します。

![「SSOログイン」ボタンが表示されたログイン画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/6c74941681cb44bcbad2df6f33f397ca.png)

## パスキー認証

パスワードを用いない認証方式です。デバイスの生体認証（指紋・顔認証など）またはハードウェアキーを使用してログインします。パスキーはデバイスに紐付けられ、フィッシング耐性があります。パスキー認証設定時は、「パスキーでログイン」ボタンが表示します。

![「パスキーでログイン」ボタンが表示されたログイン画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/698387624bee44daa181126bea4e26ad.png)

次の二段階認証が有効な環境では、以下の挙動となります。

1.  パスキー認証でログインした場合、二段階認証画面は表示されません。
1.  ID、パスワードでログインした場合、二段階認証画面が表示されます。

## 二段階認証

上記3つの認証処理と確認コードの入力の二段階の認証方式です。上記3ついずれかの認証後に確認コード入力ダイアログが表示します。

### 認証方式がメールの場合

メール送信された確認コードを入力することでログイン処理が完了します。

![メールで届いた確認コードを入力するダイアログ](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/d1062d843cae43c68a937d16bb5cb49a.png)

### 認証方式がTOTPの場合

初回ログイン時には、QRコードが表示されます。TOTP認証に対応した認証アプリでQRコードを読み取ることで、ログインに必要な確認コードを取得できます。認証アプリに表示される確認コードを入力することで、ログイン処理が完了します。

![TOTPの初回ログインで表示されるQRコードの画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/786f24f8758841479a3ca67081b0bc78.png)

## 関連情報

-   [プリザンターとActive Directoryを連携する ― AD連携](../../../setup/additional/authn-authz/active-directory.md)
-   [SAML認証を利用する](../../../setup/additional/authn-authz/saml.md)
-   [パスキー認証を利用する](../../../setup/additional/authn-authz/passkey.md)
-   [メールによる二段階認証を利用する](../../../setup/additional/authn-authz/secondary-authentication.md)
-   [TOTP（Time-based One-Time Password）による二段階認証を利用する](../../../setup/additional/authn-authz/totp-authentication.md)
-   [ユーザ管理機能](../../../managers-guide/user-administration/index.md)
-   [統合Windows認証によるシングルサインオンを利用する](../../../setup/additional/authn-authz/active-directory-sso.md)
