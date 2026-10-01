---
title: 作成・更新
category: 組織管理機能
order: '10'
status: ''
parts: ''
urlstring: dept-new-edit
translationKey: dept-new-edit
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

ユーザの所属する組織を作成できます。

## 事前準備

- この操作を実行するユーザは[テナント管理者](../user-administration/user-management-tenant-manager.md)権限を有効にしておく必要があります。

## 組織の作成

1. 「管理」メニューを開き「組織の管理」をクリックします。
2. 「新規作成」ボタンをクリックします。
3. 下表の必要事項を入力します。

|項目名|説明|設定|
|:---|:---|:---|
|組織ID|対象組織のID|一意の番号が自動採番|
|バージョン|変更履歴の番号|更新時に自動でカウントアップ|
|組織コード|組織を管理するためのコード|任意のコードを設定|
|組織名|組織の名称|任意の組織名を設定|
|説明|補足説明を記入する欄|任意の文章を記載|

4. 「作成」ボタンをクリックします。

## 組織の更新

1. 「管理」メニューを開き「組織の管理」をクリックします。
1. 更新したい組織をクリックします。
1. 任意の項目を修正します。
1. 「更新」ボタンをクリックします。

## 制限事項

### [Security.json](../../setup/parameters/security-json.md)によるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、組織単位でプリザンターへアクセスを許可する機能があります。該当機能を使用して組織単位のアクセス許可を行っている場合、組織の削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

※[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)