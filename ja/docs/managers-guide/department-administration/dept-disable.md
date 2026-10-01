---
title: 無効化・有効化
category: 組織管理機能
order: '20'
status: ''
parts: ''
urlstring: dept-disable
translationKey: dept-disable
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

既存の組織を無効化・有効化します。組織が無効になると、組織単位のアクセス制御が無効になります。

## 事前準備

- この操作を実行するユーザは[テナント管理者](../user-administration/user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

### 組織の無効化

1. 「管理」メニューを開き「組織の管理」をクリックします。
1. 対象の組織をクリックします。
1. 「無効」をチェックします。
1. 「更新」ボタンをクリックします。
1. 組織が無効化されます。

### 組織の有効化

1. 「管理」メニューを開き「組織の管理」をクリックします。
1. 対象の組織をクリックします。
1. 「無効」のチェックを外します。
1. 「更新」ボタンをクリックします。
1. 無効だった組織が有効化されます。

## 制限事項

### [Security.json](../../setup/parameters/security-json.md)によるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、組織単位でプリザンターへアクセスを許可する機能があります。該当機能を使用して組織単位のアクセス許可を行っている場合、組織の削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

※[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)