---
title: 無効化・有効化
category: グループ管理機能
order: '70'
status: ''
parts: ''
urlstring: group-disable
translationKey: group-disable
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

既存のグループを無効化・有効化します。グループが無効になると、グループ単位のアクセス制御が無効になります。

## 操作手順

この操作はテナント管理者権限またはグループの管理権限が必要です。

### 無効化する

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  対象のグループをクリックします。
1.  「無効」をチェックします。
1.  「更新」ボタンをクリックします。
1.  グループが無効化されます。

## 有効化する

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  対象のグループをクリックします。
1.  「無効」のチェックを外します。
1.  「更新」ボタンをクリックします。
1.  無効だったグループが有効化されます。

## 制限事項

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
