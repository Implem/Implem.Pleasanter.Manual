---
title: 組織管理機能
category: 組織管理機能
order: '100'
status: ''
parts: ''
urlstring: dept
translationKey: dept
shortname: 組織
created: 2019-04-30
updated: 2025-07-08
---

## 概要

組織では、ユーザの所属する組織を作成できます。一人のユーザは1つの組織にしか所属できません。

## 組織管理

組織名や組織コードなどの組織情報を管理できます。

![組織の管理の一覧画面](https://pleasanter.org/files/images/ja/managers-guide/department-administration/assets/a26cebf2727e426ea3e9aff3d58d8d32.png)

## 組織管理の設定方法

1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  「組織の管理」をクリックしてください。
1.  下表の必要事項を入力してください。

    | 項目名                 | 説明                                 | 設定                                         |
    | :--------------------- | :----------------------------------- | :------------------------------------------- |
    | 組織ID                 | 対象組織のID                         | 一意の番号が自動採番                         |
    | バージョン             | 変更履歴の番号                       | 更新時に自動でカウントアップ                 |
    | 組織コード             | 組織を管理するためのコード           | 任意のコードを設定                           |
    | 組織名                 | 組織の名称                           | 任意の組織名を設定                           |
    | 説明                   | 補足説明を記入する欄                 | 任意の文章を記載                             |
    | 無効                   | 組織の有効・無効の設定               | 組織を無効する場合はチェック                 |
    | 新バージョンとして保存 | バージョンをカウントアップするか指定 | バージョンをカウントアップする場合はチェック |

1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

## 組織管理機能の利用方法

組織管理は様々な機能を備えています。詳細は下記を参照してください。

-   [組織管理機能：作成・更新](dept-new-edit.md)
-   [組織管理機能：無効化・有効化](dept-disable.md)
-   [組織管理機能：削除](dept-delete.md)
-   [組織管理機能：一括削除](dept-bulk-delete.md)
-   [組織管理機能：ごみ箱から復元](dept-restore.md)
-   [組織管理機能：ごみ箱から削除](dept-physical-delete.md)
-   [組織管理機能：インポート](dept-import.md)
-   [組織管理機能：エクスポート](dept-export.md)

### ユーザを組織に登録する

ユーザを組織に登録・登録解除するには、「ユーザ管理機能」で組織を選択します。詳しくは[ユーザ管理：組織に登録](../user-administration/user-regist-dept.md)をご覧ください。

## 制限事項

### Security.jsonによるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、組織単位でプリザンターへアクセスを許可する機能があります。該当機能を使用して組織単位のアクセス許可を行っている場合、組織の削除/無効化/所属するユーザの削除によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

!!! tip
    [Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [組織管理機能：作成・更新](dept-new-edit.md)
-   [組織管理機能：無効化・有効化](dept-disable.md)
-   [組織管理機能：削除](dept-delete.md)
-   [組織管理機能：一括削除](dept-bulk-delete.md)
-   [組織管理機能：ごみ箱から復元](dept-restore.md)
-   [組織管理機能：ごみ箱から削除](dept-physical-delete.md)
-   [組織管理機能：インポート](dept-import.md)
-   [組織管理機能：エクスポート](dept-export.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
