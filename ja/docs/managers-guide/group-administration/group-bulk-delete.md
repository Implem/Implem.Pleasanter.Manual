---
title: 一括削除
category: グループ管理機能
order: '90'
status: ''
parts: ''
urlstring: group-bulk-delete
translationKey: group-bulk-delete
shortname: ''
created: 2023-10-27
updated: 2025-07-08
---

## 概要

グループを一括削除します。削除したグループは[ごみ箱](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)に格納されます。

## 事前準備

-   この操作を実行するユーザは[テナント管理者](../user-administration/user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 操作手順

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  削除したいグループをチェックします。チェック欄は各レコードの左端列です。また、全てを選択したい場合はヘッダ行のチェック欄にチェックします。
1.  [一括削除](../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)ボタンをクリックします。
1.  削除の可否について確認するポップアップが表示されます。「OK」をクリックします。
1.  画面下に「〇〇件の削除が完了しました。」とメッセージが表示されます。

## 制限事項

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [テーブル機能：レコードをごみ箱から削除](../../users-guide/table/record-authoring/edit-records/table-record-physical-delete.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [テーブル機能：レコードの一括削除](../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
