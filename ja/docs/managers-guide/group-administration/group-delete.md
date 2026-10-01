---
title: '削除'
category: グループ管理機能
order: '80'
status: ''
parts: ''
urlstring: group-delete
translationKey: group-delete
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

グループを削除します。削除したグループは[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)に格納されます。

## 前提条件

この操作は[テナント管理者](../user-administration/user-management-tenant-manager.md)権限またはグループの管理権限が必要です。

## グループの削除

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  対象のグループをクリックします。
1.  [削除](../../users-guide/table/record-authoring/edit-records/table-record-delete.md)ボタンをクリックします。

## 制限事項

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [テーブル機能：レコードの削除](../../users-guide/table/record-authoring/edit-records/table-record-delete.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
