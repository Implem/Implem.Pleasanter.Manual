---
title: グループ管理機能
category: グループ管理機能
order: '100'
status: ''
parts: ''
urlstring: group
translationKey: group
shortname: グループ
created: 2019-04-30
updated: 2025-07-08
---

## 概要

グループは、[ユーザ](../manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)または[組織](../department-administration/index.md)をまとめてグループ単位でのアクセス制御を可能にする仕組みです。一人のユーザおよび組織は複数のグループに所属できます。

## グループ管理

グループ名や所属メンバーなどのグループ情報を管理できます。

![グループの管理の一覧画面](https://pleasanter.org/files/images/ja/managers-guide/group-administration/assets/a11ed225ce6e4199b338393ae25eeb4c.png)

### グループ管理の設定方法

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  下表の必要事項を入力します。

    | 項目名                 | 説明                                 | 設定方法                                     |
    | :--------------------- | :----------------------------------- | :------------------------------------------- |
    | グループID             | システムで使用するID                 | システムにより自動で入力                     |
    | バージョン             | システムで使用するバージョン番号     | システムにより自動で入力                     |
    | グループ名             | グループ名称                         | 任意のグループ名を入力                       |
    | 説明                   | グループの説明                       | 任意の説明を入力                             |
    | 無効                   | グループの有効・無効の設定           | グループを無効する場合はチェック             |
    | LDAP同期               | LDAP同期で作成されたグループ         | システムにより自動で入力                     |
    | 新バージョンとして保存 | バージョンをカウントアップするか指定 | バージョンをカウントアップする場合はチェック |

1.  「更新」ボタンをクリックします。

## グループ機能の利用方法

グループは様々な機能を備えています。詳細は下記をご参照ください。

[グループ管理機能：作成・更新](group-new-edit.md)
[グループ管理機能：所属するユーザ/組織の追加](group-add-user.md)
[グループ管理機能：所属するユーザ/組織の削除](group-delete-user.md)
[グループ管理機能：子グループの追加](group-add-subgroup.md)
[グループ管理機能：子グループの削除](group-delete-subgroup.md)
[グループ管理機能：削除](group-delete.md)
[グループ管理機能：一括削除](group-bulk-delete.md)
[グループ管理機能：ごみ箱から復元](group-restore.md)
[グループ管理機能：ごみ箱から削除](group-physical-delete.md)
[グループ管理機能：無効化・有効化](group-disable.md)
[グループ管理機能：インポート](group-import.md)
[グループ管理機能：エクスポート](group-export.md)

### グループに所属するユーザ/組織の検索

以下の操作でグループに所属するユーザ/組織を指定してグループを検索できます。この操作は[テナント管理者](../user-administration/user-management-tenant-manager.md)権限またはグループの管理権限が必要です。

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  [フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)の[組織](../department-administration/index.md)または[ユーザ](../manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の入力項目に検索する文字列を入力し、エンターキーを押します。組織またはユーザ検索時の入力文字列はそれぞれ以下の項目を検索対象とします。

    | 項目名 | 検索対象                                |
    | :----- | :-------------------------------------- |
    | 組織   | 組織名 / 組織コード / 説明              |
    | ユーザ | ログインID / 名前 / ユーザコード / 説明 |

1.  検索結果がグループ一覧に表示されます。
1.  検索結果から対象のグループをクリックします。
1.  「メンバー」タブをクリックします。

### グループによるアクセス制御

グループ単位で、サイトやレコードに対するアクセスを許可できます。詳しくは[サイトのアクセス制御](../manage-table/site-access-control/index.md)または[レコードのアクセス制御](../../users-guide/access-control/table-record-access-control.md)をご覧ください。

### ユーザ毎のグループ管理許可権限

ユーザ毎にグループの管理許可権限とグループの作成許可権限を設定可能です。マニュアルの「ユーザ管理機能：作成」 を参照して設定ください。

## 制限事項

### [Security.json](../../setup/parameters/security-json.md)によるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

※[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [グループ管理機能：作成・更新](group-new-edit.md)
-   [グループ管理機能：変更履歴の閲覧](group-change-history.md)
-   [グループ管理機能：所属するユーザ/組織の追加](group-add-user.md)
-   [グループ管理機能：所属するユーザ/組織の削除](group-delete-user.md)
-   [グループ管理機能：子グループの追加](group-add-subgroup.md)
-   [グループ管理機能：子グループの削除](group-delete-subgroup.md)
-   [グループ管理機能：無効化・有効化](group-disable.md)
-   [グループ管理機能：削除](group-delete.md)
-   [グループ管理機能：一括削除](group-bulk-delete.md)
-   [グループ管理機能：ごみ箱から復元](group-restore.md)
-   [グループ管理機能：ごみ箱から削除](group-physical-delete.md)
-   [グループ管理機能：インポート](group-import.md)
-   [グループ管理機能：エクスポート](group-export.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [組織管理機能](../department-administration/index.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [サイトのアクセス制御](../manage-table/site-access-control/index.md)
-   [レコードのアクセス制御（レコードの編集）](../../users-guide/access-control/table-record-access-control.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
