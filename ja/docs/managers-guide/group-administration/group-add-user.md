---
title: 所属するユーザ/組織の追加
category: グループ管理機能
order: '30'
status: ''
parts: ''
urlstring: group-add-user
translationKey: group-add-user
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

グループに所属するユーザまたは組織を追加します。「メンバー」タブでは、グループの管理権限も設定できます。

## 前提条件

この操作は[テナント管理者](../user-administration/user-management-tenant-manager.md)権限またはグループの管理権限が必要です。

## 操作手順

### グループに所属するユーザ/組織の追加

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  対象のグループをクリックします。
1.  「メンバー」タブをクリックします。
1.  画面右の「選択可能なメンバー」でグループに追加するユーザ名もしくは組織名を入力して検索します。[^1]
1.  追加する対象を選択します
1.  「追加」のボタンをクリックします。
1.  「更新」ボタンをクリックします。

[^1]: 検索欄に「%」を入力し、++enter++ を押下すると、登録されているユーザ/組織が全て表示されます。

### グループの管理権限を付与する

1.  管理権限を付与したいメンバーをクリックします。
1.  「管理者」ボタンをクリックします。
1.  メンバー名の隣に(Manager)と表示されます。
1.  「更新」ボタンをクリックします。

### グループの管理権限を外す

1.  管理権限を付与したいメンバーをクリックします。
1.  「一般ユーザ」ボタンをクリックします。
1.  メンバー名の隣にある(Manager)が非表示になります。
1.  「更新」ボタンをクリックします。

## 制限事項

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
