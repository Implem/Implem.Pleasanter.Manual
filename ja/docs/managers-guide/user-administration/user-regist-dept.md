---
title: 組織に登録
category: ユーザ管理機能
order: '40'
status: ''
parts: ''
urlstring: user-regist-dept
translationKey: user-regist-dept
shortname: ''
created: 2025-06-26
updated: 2025-07-08
---

## 概要

ユーザが所属する組織を選択します。

## 事前準備

-   あらかじめ「組織管理機能：作成・更新」で、所属させたい組織を作成しておきます。
-   この操作を実行するユーザは[テナント管理者](user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

### 所属する組織を登録する

1.  「管理」メニューを開き[ユーザの管理](index.md)をクリックします。
1.  対象のユーザをクリックします。
1.  ユーザ情報の編集画面の[組織](../department-administration/index.md)項目で所属させたい組織を選択します。
1.  「更新」ボタンをクリックします。

### 組織の所属を解除する

どの組織にも所属しないユーザは、[組織](../department-administration/index.md)項目で空欄を選択します。

## 制限事項

-   一人のユーザは1つの組織にしか所属できません。

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、組織単位でプリザンターへアクセスを許可する機能があります。該当機能を使用して組織単位のアクセス許可を行っている場合、組織の削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [ユーザ管理機能：テナント管理者の設定](user-management-tenant-manager.md)
-   [ユーザ管理機能](index.md)
-   [組織管理機能](../department-administration/index.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
