---
title: '作成・更新'
category: グループ管理機能
order: '10'
status: ''
parts: ''
urlstring: group-new-edit
translationKey: group-new-edit
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

グループを作成・更新します。

## グループの作成

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  「新規作成」ボタンをクリックします。
1.  下表の必要事項を入力します。

    | 項目名     | 説明                 | 設定                         |
    | :--------- | :------------------- | :--------------------------- |
    | グループID | 対象グループのID     | 一意の番号が自動採番         |
    | バージョン | 変更履歴の番号       | 更新時に自動でカウントアップ |
    | グループ名 | グループの名称       | 任意のグループ名を設定       |
    | 説明       | 補足説明を記入する欄 | 任意の文章を記載             |

1.  「作成」ボタンをクリックします。

## グループの更新

1.  「管理」メニューを開き「グループの管理」をクリックします。
1.  更新したいグループをクリックします。
1.  任意の項目を修正します。
1.  「更新」ボタンをクリックします。

## 制限事項

### [Security.json](../../setup/parameters/security-json.md)によるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、グループ単位でプリザンターへアクセスを許可する機能があります。該当機能を使用してグループ単位のアクセス許可を行っている場合、グループの削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

※[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
