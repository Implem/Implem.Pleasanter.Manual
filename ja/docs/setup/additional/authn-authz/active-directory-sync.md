---
title: プリザンターにActive Directoryのユーザ情報を同期する
category: 追加設定：認証
order: '200'
status: ''
parts: ''
urlstring: active-directory-sync
translationKey: active-directory-sync
shortname: LDAP同期
created: 2019-04-29
updated: 2025-03-13
---

## 概要

ActiveDirectoryなどのLDAPサーバとの同期処理を自動実行する方法を説明します。ご利用環境が以下に当てはまる場合に本手順で[LDAP同期](active-directory-sync-script.md)機能の定期実行を設定してください。

-   ご利用のプリザンターのバージョン1.3.19以降である

## 制限事項

1. プリザンターのバージョン1.3.19以降、ldap同期処理を自動実行する手順が変更になりました。ご利用環境が以下に当てはまる場合は「プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）」を確認してください。  

    -   ご利用のプリザンターのバージョンが1.3.18以前である  
    -   統合Windows認証を有効とした環境である（バージョン問わず）

2. 本手順の設定をしたまま、「プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）」の手順で設定するとLDAP同期処理が二重起動し、設定内容によってはログインできなくなる可能性があります。

## 操作手順

[Authentication.json](../../parameters/authentication-json.md)および[BackgroundService.json](../../parameters/background-service-json.md)のパラメータ設定値を変更してください。なお、パラメータ変更時はマニュアル[パラメータ変更時の確認事項](../../parameters/parameter-edit.md)を確認してください。

#### Authentication.json

LdapParameters配下のパラメータを設定してください。

#### BackgroundService.json

マニュアル「[パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)」を参照し、BackgroundService.jsonファイル内の設定を下記の設定値に変更してください。

|項目|設定例|説明|
|:--|:--|:--|
|SyncByLdap|true|LDAP同期の自動実行を有効化|
|SyncByLdapTime|["01:00"]|LDAP同期を自動実行する時間|

## 関連情報

-   [プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）](active-directory-sync-script.md)
-   [パラメータ設定：Authentication.json](../../parameters/authentication-json.md)
-   [パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)
-   [パラメータ設定：パラメータ変更時の確認事項](../../parameters/parameter-edit.md)
