---
title: エクスポート
category: 組織管理機能
order: '80'
status: ''
parts: ''
urlstring: dept-export
translationKey: dept-export
shortname: ''
created: 2025-06-25
updated: 2025-07-08
---

## 概要

「組織管理」画面の組織情報をCSVファイルとして出力するための機能です。現在の組織情報を一括で取得することができます。CSVファイルの文字コードにはShift-JISまたはUTF-8が使用できます。

## 手順

1. 「組織管理」画面にて画面下の[エクスポート](../../developers-guide/api/table-operations/api-export.md)ボタンをクリックします。
1. エクスポートダイアログが表示されます。書式、文字コードを選択します。書式は"標準"のみ選択可能です。文字コードはShift-JISまたはUTF-8が選択できます。
1. ファイルがダウンロードされます。エクスポートされる項目については、下記「CSVファイル項目名」を参照ください。

### CSVファイル項目名

|項目名(エクスポートされる列名)|説明|
|:----|:----|
|組織ID|組織ID。一意の番号が自動採番|
|組織コード|組織を管理するためのコード|
|組織名|組織の名称|
|説明|補足説明を記入する欄|
|コメント|組織のコメント欄の内容|
|無効|組織が無効に設定されている場合"1"|
|作成者|組織の作成者|
|更新者|組織の更新者|
|更新日時|組織の更新日時|

## 制限事項

- テーブルの一覧のエクスポートとは異なり、チェックボックスの有/無にかかわらず全件データがエクスポートの対象となります。

### [Security.json](../../setup/parameters/security-json.md)によるアクセス制限について

[Security.json](../../setup/parameters/security-json.md)には、「AllowIpAddresses」と「IpRestrictionExcludeMembers」を併せて設定することにより、組織単位でプリザンターへアクセスを許可する機能があります。該当機能を使用して組織単位のアクセス許可を行っている場合、組織の無効化によって、所属ユーザがプリザンターへアクセスできなくなります。

テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または[Security.json](../../setup/parameters/security-json.md)の再設定等の作業が必要になる可能性があります。

※[Security.json](../../setup/parameters/security-json.md)の「AllowIpAddresses」でIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 関連情報

-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../developers-guide/api/table-operations/api-export.md)
-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
