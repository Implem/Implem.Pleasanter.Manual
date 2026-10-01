---
title: 一括削除
category: 組織管理機能
order: '40'
status: ''
parts: ''
urlstring: dept-bulk-delete
translationKey: dept-bulk-delete
shortname: ''
created: 2023-10-27
updated: 2025-07-08
---

## 概要

組織を一括削除します。削除した組織は[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)に格納されます。

[ごみ箱]: ../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md

## 注意事項

### IPアドレス制限と組織の削除についての注意

[Security.json](../../setup/parameters/security-json.md)のパラメータ「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定すると、IPアドレス制限を実施しつつ、組織単位でプリザンターへのアクセスを許可できます。この機能を使用して組織単位のアクセス許可を行っている場合、組織の削除によって、所属ユーザがプリザンターへアクセスできなくなりますので、注意してください。

[Security.json]: ../../setup/parameters/security-json.md

テナント管理者などの重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更またはSecurity.jsonの再設定などの作業が必要になる可能性があります。

!!! tip
    [Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 前提条件

-   この操作を実行するユーザは[テナント管理者](../user-administration/user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

1.  「管理」メニューを開き「組織の管理」をクリックします。
1.  削除したい組織をチェックします。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックします。
1.  「一括削除」ボタンをクリックします。
1.  削除の可否について確認するポップアップが表示されます。「OK」をクリックします。
1.  画面下に「〇〇件の削除が完了しました。」とメッセージが表示されたら完了です。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [テーブル機能：レコードの一括削除](../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
