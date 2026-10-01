---
title: AD連携前に登録したローカルユーザはAD認証の対象になりますか
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-local-user-ad-sync-authentication
translationKey: faq-local-user-ad-sync-authentication
shortname: ''
created: 2026-03-17
updated: 2026-03-17
---

## 回答

AD（Active Directory）連携前に登録したローカルユーザは、AD認証の対象となります。

---

## 概要

[AD連携](../../setup/additional/authn-authz/active-directory.md)時は、通常、設定ファイル[Authentication.json](../../setup/parameters/authentication-json.md)のパラメータ"Provider"の値をLDAPに設定します。これによりADで設定したパスワードによるログインが可能となります。

何らかの理由によりAD側のパスワードを使用できない場合は、設定ファイル[Authentication.json](../../setup/parameters/authentication-json.md)のパラメータ"Provider"の値を"LDAP+Local"に設定してください。
これによりローカルユーザのパスワードでログインが可能となります。
W"#"
ユーザのレコードは1つのため、どちらのパスワードでログインしても、ログイン後の権限など、ユーザとしての動作に違いはありません。

## 関連情報

-   [プリザンターとActive Directoryを連携する ― AD連携](../../setup/additional/authn-authz/active-directory.md)
-   [パラメータ設定：Authentication.json](../../setup/parameters/authentication-json.md)
