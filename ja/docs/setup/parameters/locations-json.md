---
title: Locations.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: locations-json
translationKey: locations-json
shortname: Locations.json
created: 2020-04-21
updated: 2024-09-13
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。 

## 制限事項

[テナントの管理](../../managers-guide/tenant-administration/index.md)で[ダッシュボード](../../users-guide/dashboard/dashboard-add-parts.md)を設定した場合、TopUrlおよびLoginAfterUrlの設定内容は無視されます。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|TopUrl| "/items/123/index" |ロゴをクリックした際や「トップ」をクリックした際に遷移するURL|
| LoginAfterUrl | "/items/456/index" |ログイン後に遷移するURL(ログイン後最初に表示される画面)|
| LoginAfterUrlExcludePrivilegedUsers| true |trueを指定した場合、特権ユーザはLoginAfterUrlで指定したURLおよび[テナントの管理](../../managers-guide/tenant-administration/index.md)で設定した[ダッシュボード](../../users-guide/dashboard/dashboard-add-parts.md)には遷移しません。|

URLの指定は / から記載してください。上記の場合、http://pleasanter.net/items/123/index というプリザンター本体のパス以降を/ から記載しています。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.6.0 以降|LoginAfterUrlExcludePrivilegedUsersを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [テナント管理機能](../../managers-guide/tenant-administration/index.md)
-   [ダッシュボード機能：パーツの追加](../../users-guide/dashboard/dashboard-add-parts.md)
