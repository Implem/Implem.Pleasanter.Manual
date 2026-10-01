---
title: 拡張サーバスクリプト
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-server-script
translationKey: extended-server-script
shortname: 拡張サーバスクリプト
created: 2021-07-13
updated: 2025-05-29
---

## 概要

システム全体で使用可能な[サーバスクリプト](../server-script/index.md)を定義します。

## 制限事項

1. 拡張スクリプトのJSONファイルやスクリプトファイルを更新した後は「アプリケーションを再起動」するまで反映しません。

## 拡張サーバスクリプトの設定方法

.¥Pleasanter¥App_Data¥Parameters¥ExtendedServerScripts¥ 配下に以下の内容を含むjsonファイルを作成し、「アプリケーションを再起動」してください。ファイルの拡張子は必ずjsonにしてください。ExtendedServerScripts配下はフォルダで階層化することが可能です。この場合、配下の全てのjsonファイルが設定ファイルとして読み込まれます。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Name|Sample|APIから実行させる際の名前を設定します。|
|Description|"このスクリプトは・・・を実行します"|スクリプトの説明。動作には影響しません。|
|Disabled|false|trueの場合は無効化され動作しません。|
|DeptIdList|[1,2,3]|対象となる組織IDを配列形式で指定します。指定しない場合には省略可能です。|
|GroupIdList|[1,2,3]|対象となるグループIDを配列形式で指定します。指定しない場合には省略可能です。|
|UserIdList|[1,2,3]|対象となるユーザIDを配列形式で指定します。指定しない場合には省略可能です。|
|SiteIdList|[1,2,3]|対象となるサイトのサイトIDを配列形式で指定します。指定しない場合には省略可能です。|
|IdList|[1,2,3]|対象となるレコードのIDを配列形式で指定します。指定しない場合には省略可能です。|
|Controllers|["items"]|対象となるコントローラを配列形式で指定します。指定しない場合には省略可能です。|
|Actions|["index","edit"]|対象となるアクションを配列形式で指定します。指定しない場合には省略可能です。|
|WhenloadingSiteSettings|false|trueの場合、サイト設定読み込み時 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|WhenViewProcessing|false|trueの場合、ビュー処理時 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|WhenloadingRecord|false|trueの場合、レコード読み込み時 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeFormula|false|trueの場合、計算式の前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|AfterFormula|false|trueの場合、計算式の後 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeCreate|false|trueの場合、作成前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|AfterCreate|false|trueの場合、作成後 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeUpdate|false|trueの場合、更新前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|AfterUpdate|false|trueの場合、更新後 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeDelete|false|trueの場合、削除前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|AfterDelete|false|trueの場合、削除後 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeBulkDelete|false|trueの場合、一括削除前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|AfterBulkDelete|false|trueの場合、一括削除後 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeOpeningPage|false|trueの場合、画面表示の前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|BeforeOpeningRow|false|trueの場合、行表示の前 の[条件](../../FAQ/editor/faq-condition-mode-range.md)で実行します。|
|Body|"context.Log('test');"|実行するスクリプトを記述します。|

## スクリプトを外部ファイルから読み込む

jsonファイルと同じディレクトリに、jsonファイルに拡張子.jsを追加したテキストファイルを作成すると、Bodyを外部ファイルから読み込む事が可能です。sample.jsonの外部ファイルのファイル名はsample.json.jsです。

## サンプルコード

下記の例では、サイトID:2で、"BeforeOpeningPage": trueにより画面表示の前にBodyのスクリプトが実行されます。

##### スクリプト

```
{
    "Name": "Sample",
    "SiteIdList": [2],
    "BeforeOpeningPage": true,
    "Body": "// Write an arbitrary script."
}
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.16.0 以降|パラメータにBeforeBulkDeleteおよびAfterBulkDeleteを追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../server-script/index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../FAQ/editor/faq-condition-mode-range.md)