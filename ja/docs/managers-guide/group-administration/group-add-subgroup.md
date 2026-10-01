---
title: 子グループの追加
category: グループ管理機能
order: '50'
status: ''
parts: ''
urlstring: group-add-subgroup
translationKey: group-add-subgroup
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

既存のグループを子グループとして追加します。追加された子グループは、親グループのアクセス権を継承します。

## 事前準備

-   子グループを追加するには、グループが必要です。あらかじめ、子グループとして追加したいグループを作成しておきます。
-   この操作はテナント管理者権限またはグループの管理権限が必要です。

## 操作手順

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  対象のグループをクリックします。
1.  [子グループ](../../users-guide/hands-on/basics/basic-operations-group-child.md)タブをクリックします。
1.  画面右の「選択可能なグループ」で追加したいグループを検索します。[^1]
1.  「更新」ボタンをクリックします。  

[^1]: 検索欄に「%」を入力し、++enter++ を押下すると、登録されているグループが全て表示されます。

## 制限事項

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [子グループ追加](../../users-guide/hands-on/basics/basic-operations-group-child.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
