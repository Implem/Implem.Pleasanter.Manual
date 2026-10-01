---
title: 定期実行
category: 操作ガイド（応用編）
order: '0'
status: ''
parts: ''
urlstring: advanced-operations-task
translationKey: advanced-operations-task
shortname: 定期実行
created: 2023-12-11
updated: 2024-12-19
---

## 概要

プリザンターでは[リマインダー](advanced-operations-notification.md)、[LDAP同期](../../../setup/additional/authn-authz/active-directory-sync-script.md)の他「システムログの削除」、「テンポラリファイルの削除」、「ごみ箱のレコード削除」などを定時で実行することができます。また、様々な業務要件に合わせ作成した[サーバスクリプト](../../../developers-guide/server-script/index.md)を定期実行する[バックグラウンドサーバスクリプト](../../../managers-guide/tenant-administration/background-server-script.md)機能があります。

## 1．リマインダー

[リマインダー](advanced-operations-notification.md)は、期日が過ぎたレコード、または指定範囲内で期日が近付いたレコードに対して指定した時刻・周期でリマインド通知する機能です。

詳しくはこちらを参照してください。  
[応用編：通知、リマインダー](advanced-operations-notification.md)

## 2．LDAP同期

[LDAP認証](../../../setup/additional/authn-authz/active-directory.md)（ログインID、パスワードを用いてActive Directory等のLDAPサーバで認証を行う）の設定を用いて、毎日定時刻にLDAPサーバのユーザ情報をプリザンターに同期する機能です。パラメータファイルの設定に応じて、LDAPサーバ上のユーザ情報を取込む際の検索条件の指定や、取込結果に応じてプリザンター側のユーザの無効化／有効化を自動設定する機能があります。

## 3．システムログの削除

あらかじめ指定した保存期間を過ぎたシステムログを毎日定時刻に削除する機能です。保存期間は[SysLog.json](../../../setup/parameters/sys-log-json.md)の"RetentionPeriod"で指定します。

## 4．テンポラリファイルの削除

あらかじめ指定した保存期間を過ぎたテンポラリファイル（App_Data\Temp配下およびApp_Data\Histories配下のファイル）を毎日定時刻に削除する機能です。保存期間は[General.json](../../../setup/parameters/general.json.md)の"DeleteTempOldThan"および"DeleteHistoriesOldThan"で指定します。

## 5．ごみ箱のレコード削除

あらかじめ指定した保存期間を過ぎた[ごみ箱](../../table/record-authoring/edit-records/table-record-physical-delete.md)内のレコードを毎日定時刻に削除する機能です。保存期間は[BackgroundService.json](../../../setup/parameters/background-service-json.md)の"DeleteTrashBoxRetentionPeriod"で指定します。

## 6．バックグラウンドサーバスクリプト

任意のサーバスクリプトを指定した周期で実行する機能です。毎時、毎日、毎週、毎月など様々なタイミングで実行するバッチ処理をプリザンターだけで実現することが可能です。

詳しくはこちらを参照してください。  
[テナント管理機能：バックグラウンドサーバスクリプト](../../../managers-guide/tenant-administration/background-server-script.md)

![バックグラウンドサーバスクリプトの設定画面](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/0eba613366534409a7bfb43e86bd15ab.png)

![バックグラウンドサーバスクリプトの設定画面（続き）](https://pleasanter.org/files/images/ja/users-guide/hands-on/advanced/assets/5045e44399ce4022b629b79a82a5c3ff.png)

## 関連項目

-   [応用編：通知、リマインダー](advanced-operations-notification.md)
-   [プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）](../../../setup/additional/authn-authz/active-directory-sync-script.md)
-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [テナント管理機能：バックグラウンドサーバスクリプト](../../../managers-guide/tenant-administration/background-server-script.md)
-   [プリザンターとActive Directoryを連携する ― AD連携](../../../setup/additional/authn-authz/active-directory.md)
-   [パラメータ設定：SysLog.json](../../../setup/parameters/sys-log-json.md)
-   [パラメータ設定：General.json](../../../setup/parameters/general.json.md)
-   [テーブル機能：レコードをごみ箱から削除](../../table/record-authoring/edit-records/table-record-physical-delete.md)
-   [パラメータ設定：BackgroundService.json](../../../setup/parameters/background-service-json.md)
