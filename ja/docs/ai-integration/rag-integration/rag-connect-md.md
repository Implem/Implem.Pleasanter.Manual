---
title: マークダウンファイルを出力する
category: RAG連携
order: '100'
status: ''
parts: ''
urlstring: rag-connect-md
shortname: RAG連携：マークダウンファイルを出力する
created: 2026-08-25
updated: 2026-09-08
---

## 概要

[RAG連携](rag-connect.md)機能を使い、指定したテーブルのレコードをマークダウンファイルとして書き出す手順を説明します。

## 制限事項

1. マークダウンファイルはレコードを更新したユーザの権限で出力されます。そのユーザに閲覧権限のない項目の値は空文字列で出力されます。

## 前提条件

1. 設定を変更するには「サイトの管理」権限が必要です。
1. [AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータEnabledをtrueに設定してください。
1. [AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータOutputFilePathに、連携文書の出力先フォルダを設定してください。未設定の状態で更新・同期を実行するとエラーメッセージが表示されます。

## 操作手順

1. [テーブルの管理：AI連携](../../managers-guide/manage-table/ai-connect/index.md)で「AI連携設定」を新規作成してください。
1. 「AI連携」ダイアログが開きます。下記を参考に各項目を設定してください。

   ![「AI連携」ダイアログ](https://pleasanter.org/files/images/ja/ai-integration/rag-integration/assets/2af05e15da0b4afda296977f449477f8.png)

   | 項目             | 必須 | 説明                                                                                                     |
   | :--------------- | :--: | :------------------------------------------------------------------------------------------------------- |
   | ID               | —    | 設定不要です。<br>連携先を識別する番号です。自動で採番され変更できません。<br>新規作成時は表示されません。|
   | タイトル         | ○    | サイト管理者が連携先を識別するための名前を指定してください。|
   | 連携フォーマット | ○    | 下記「連携フォーマット」を参考に、マークダウンファイルの書式を指定してください。<br>初期値は[AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータFormatTemplateです。|
   | 連携方式         | —    | 「mdファイル」を選択してください。|
   | 無効             | —    | 連携を無効化するときのみ、オンにしてください。|

1. 新規作成時は「追加」ボタンを、既存の設定を編集する場合は「変更」ボタンをクリックしてください。
1. コマンドボタンエリアの「更新」ボタンをクリックしてください。

## 連携フォーマット

-   プリザンターの[リマインダー](../../managers-guide/manage-table/reminders/table-management-reminder.md)や[通知](../../managers-guide/manage-table/notifications/table-management-notification-messagebody.md)の本文で利用できる記法と同じ記法を使用します。
-   角括弧（ [ と ] ）と波括弧（ { と } ）で囲んだ文字列は、以下の規則で置換されます。

    | 記法          | 内容                                                             |
    | :------------ | :--------------------------------------------------------------- |
    | [カラム名]  |当該カラムの表示値に置換されます。<br>例：[Title]、[Status]、[Owner]、[Body] |
    | {Url}         | レコードの編集画面の絶対URLに置換されます。                        |
    | {LoginId}     | 操作者のログインIDに置換されます。|
    | {UserName}    | 操作者のユーザ名に置換されます。|
    | {MailAddress} | 操作者のメールアドレスに置換されます。|

##### 連携フォーマットの設定例

```markdown
# [Title]

## レコード情報

| ID        | バージョン  | 開始         | 完了             |
| :-------- | :--------- | :---------- | :--------------- |
| [IssueId] | [Ver]      | [StartTime] | [CompletionTime] |

## WBS分類

- 作業工程：[ClassA]
- 作業内容：[ClassB]
- 機能分類：[ClassC]

## 作業内容

[Body]

## 状況

### [Status]

## 進捗管理

- 作業量：[WorkValue]
- 進捗率：[ProgressRate]
- 残作業量：[RemainingWorkValue]

---

管理者：[Manager]／担当者：[Owner]
```

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.8.0 以降| 機能追加|
