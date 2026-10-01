---
title: 削除
category: 組織管理機能
order: '30'
status: ''
parts: ''
urlstring: dept-delete
translationKey: dept-delete
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

組織を削除します。削除した組織は[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)に格納されます。

## 事前準備

- この操作を実行するユーザは[テナント管理者](../user-administration/user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 組織の削除

1. 「管理」メニューを開き「組織の管理」をクリックします。
1. 対象の組織をクリックします。
1. [削除](../../users-guide/table/record-authoring/edit-records/table-record-delete.md)ボタンをクリックします。

## 制限事項

### [Security.json](../../setup/parameters/security-json.md)によるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、組織単位でプリザンターへアクセスを許可する機能があります。該当機能を使用して組織単位のアクセス許可を行っている場合、組織の削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

※[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [テーブル機能：レコードの削除](../../users-guide/table/record-authoring/edit-records/table-record-delete.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
