---
title: Permissions.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: permissions-json
translationKey: permissions-json
shortname: Permissions.json
created: 2019-04-30
updated: 2026-05-25
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|CheckManagePermission|true|「権限の管理」権限を有するユーザが存在するかチェックする場合はtrueを設定。|
|General|31|既定の一般利用者のアクセス権を指定。31は書き込み権限。|
|Manager|511|既定の管理者のアクセス権を指定。511は管理者権限。|
|Pattern|json配列|アクセス権のパターンを設定。|
|ReadOnly|1|読取専用のアクセス権。|
|ReadWrite|31|書き込みのアクセス権。|
|Leader|255|リーダーのアクセス権。|
|Manager|511|管理者のアクセス権。|
|PageSize|100|アクセス権設定対象一覧に表示するリストの最大件数。|

設定可能なアクセス権の数字は、下記のソースコードのenum Typesに記載されている数値の論理和。  
https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Libraries/Security/Permissions.cs
