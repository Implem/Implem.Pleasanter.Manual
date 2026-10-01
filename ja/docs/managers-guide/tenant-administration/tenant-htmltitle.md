---
title: HTMLタイトル
category: テナント管理機能
order: '200'
status: ''
parts: ''
urlstring: tenant-htmltitle
translationKey: tenant-htmltitle
shortname: HTMLタイトル
created: 2024-04-04
updated: 2024-04-11
---

## 概要

ブラウザのタブ等に表示するHTMLタイトルを設定する機能です。トップ画面の表示、サイト（フォルダ、テーブル、Wiki、ダッシュボード）の表示、各レコードの編集画面の表示の3種類に対してそれぞれ表示内容を設定できます。

## 制限事項

1.  ログイン画面のHTMLタイトルは変更できません。ログイン画面では製品名※1が表示されます。
1.  各種管理機能（[テナント](index.md)、[システムログ](../system-log-administration/index.md)、[組織](../department-administration/index.md)、[グループ](../group-administration/index.md)、[ユーザ](../manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)）はトップ画面の設定内容で表示されます。

## 前提条件

1.  設定を行うには[テナント管理者](../user-administration/user-management-tenant-manager.md)権限が必要です。

## 設定内容

任意の文字列の他、以下キーワードを設定できます。文字列が長くなるとタブ表示で見切れるので適宜調整してください。

| 設定            | 説明                     |
| :-------------- | :----------------------- |
| \[ProductName\] | 製品名[^1]を表示         |
| \[TenantTitle\] | テナントのタイトルを表示 |
| \[SiteTitle\]   | サイトのタイトルを表示   |
| \[RecordTitle\] | レコードのタイトルを表示 |

[^1]: `Implem.Pleasanter\App_Data\Displays`配下にある「ProductName.json」で設定した文字列

### 設定イメージ

![HTMLタイトルを設定するテナントの管理画面](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/7b2d9f0bf8254d2ba7a3b8e403ed2263.png)

### 表示結果

=== "トップ画面"

    ![設定したHTMLタイトルが表示されたトップ画面](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/32fc1cec2f554d49873ac4c42c860943.png)

=== "サイト"

    ![設定したHTMLタイトルが表示されたサイトの画面](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/49fe26856b794d2aa330c2d20461d7a0.png)

=== "レコード"

    ![設定したHTMLタイトルが表示されたレコードの画面](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/58aac3edd62449f5963ffa2ac7b7baab.png)

## 関連情報

-   [テナント管理機能](index.md)
-   [システムログ管理機能](../system-log-administration/index.md)
-   [組織管理機能](../department-administration/index.md)
-   [グループ管理機能](../group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
