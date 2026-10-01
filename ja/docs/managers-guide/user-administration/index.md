---
title: ユーザ管理機能
category: ユーザ管理機能
order: '100'
status: ''
parts: ''
urlstring: user
translationKey: user
shortname: ユーザ,ユーザ管理,ユーザの管理
created: 2019-04-30
updated: 2026-03-22
---

## 概要

氏名やログインIDなどのユーザ情報管理できます。ここに登録されたユーザがプリザンターを使用できます。ユーザが利用するメールアドレスは複数件、登録することができます。

## 前提条件

1.  ユーザの管理機能を使用するには、テナント管理者または特権ユーザである必要があります。
1.  ナビゲーションメニューの「管理」－「ユーザの管理」は、ログインユーザがテナント管理者または特権ユーザで、パラメータファイル[Service.json](../../setup/parameters/service-json.md)のShowProfilesがtrueの場合に表示されます。

## ユーザ管理

![ユーザの管理の一覧画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/44d220abc8b24a468ad332d0a970dea4.png)

### ユーザ管理の設定方法

1.  「管理」メニューを開き「ユーザの管理」をクリックします。

### ユーザ機能の利用方法

ユーザは様々な機能を備えています。詳細は下記を参照してください。

-   [ユーザ管理機能：作成・更新](user-new-edit.md)
-   [ユーザ管理機能：ユーザ招待](user-invite.md)
-   [ユーザ管理機能：メールアドレスの追加](user-mailaddress.md)
-   [ユーザ管理機能：組織に登録](user-regist-dept.md)
-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [ユーザ管理機能：特権ユーザの設定](user-management-privileged-users.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](user-management-theme.md)
-   [ユーザ管理機能：多言語対応](user-multi-language.md)
-   [ユーザ管理機能：パスワードリセット](user-password-reset.md)
-   [ユーザ管理機能：認証](user-authentication.md)
-   [ユーザ管理機能：スイッチユーザ](user-switch.md)
-   [ユーザ管理機能：削除](user-delete.md)
-   [ユーザ管理機能：一括削除](user-bulk-delete.md)
-   [ユーザ管理機能：ごみ箱から復元](user-restore.md)
-   [ユーザ管理機能：ごみ箱から削除](user-physical-delete.md)
-   [ユーザ管理機能：インポート](user-import.md)
-   [ユーザ管理機能：エクスポート](user-export.md)

## ユーザ種別

ユーザには複数の種類があり、種類別に操作できる権限が異なります。

### 管理権限

|                                    | 一般ユーザ | テナント管理ユーザ | 特権ユーザ |
| :--------------------------------- | :--------: | :----------------: | :--------: |
| サイトの作成                       |     〇     |         〇         |     〇     |
| ユーザの管理                       |     ×      |         〇         |     〇     |
| 組織の管理                         |     ×      |         〇         |     〇     |
| グループの管理                     |     ×      |         〇         |     〇     |
| アクセス権のないサイトへのアクセス |     ×      |         ×          |     〇     |

### テナント管理ユーザとは

組織、グループ、ユーザの管理が可能なユーザです。詳細は以下を参照してください。

-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)

### 特権ユーザとは

アクセス権に関わらず、組織、グループ、ユーザの管理およびすべてのサイト、レコードへの操作が可能なユーザです。詳細は以下を参照してください。

-   [ユーザ管理機能：特権ユーザの設定](user-management-privileged-users.md)

### Pleasanter.netのユーザについて

-   Pleasanter.netのフリープラン、ライトプラン、スタンダードプランでは一部機能が利用可能です。詳しくは[FAQ：Pleasanter.netのユーザ管理で利用可能な機能について](../../FAQ/pleasanter.net/faq-pleasanter-net-user.md)を参照してください。
-   [Pleasanter.net専用環境](https://pleasanter.net/Home/Dedicated)では「ユーザ管理」機能をお使いいただけます。

## 関連情報

-   [パラメータ設定：Service.json](../../setup/parameters/service-json.md)
-   [ユーザ管理機能：作成・更新](user-new-edit.md)
-   [ユーザ管理機能：ユーザ招待](user-invite.md)
-   [ユーザ管理機能：メールアドレスの追加](user-mailaddress.md)
-   [ユーザ管理機能：組織に登録](user-regist-dept.md)
-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [ユーザ管理機能：特権ユーザの設定](user-management-privileged-users.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](user-management-theme.md)
-   [ユーザ管理機能：多言語対応](user-multi-language.md)
-   [ユーザ管理機能：パスワードリセット](user-password-reset.md)
-   [ユーザ管理機能：認証](user-authentication.md)
-   [ユーザ管理機能：スイッチユーザ](user-switch.md)
-   [ユーザ管理機能：削除](user-delete.md)
-   [ユーザ管理機能：一括削除](user-bulk-delete.md)
-   [ユーザ管理機能：ごみ箱から復元](user-restore.md)
-   [ユーザ管理機能：ごみ箱から削除](user-physical-delete.md)
-   [ユーザ管理機能：インポート](user-import.md)
-   [ユーザ管理機能：エクスポート](user-export.md)
-   [FAQ：Pleasanter.netのユーザ管理で利用可能な機能について](../../FAQ/pleasanter.net/faq-pleasanter-net-user.md)
-   [Pleasanter.net専用環境](https://pleasanter.net/Home/Dedicated)
