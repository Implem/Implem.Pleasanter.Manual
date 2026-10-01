---
title: OpenAIに連携する
category: RAG連携
order: '300'
status: ''
parts: ''
urlstring: rag-connect-openai
shortname: RAG連携：OpenAIに連携する
created: 2026-08-25
updated: 2026-09-08
---

## 概要

[RAG連携](rag-connect.md)機能を使い、指定したテーブルのレコードを[OpenAI Platform](https://platform.openai.com/)へ連携する手順を説明します。

## 注意事項

1.  検証環境と本番環境で異なるストレージとAPIキーを指定してください。同じストレージとAPIキーを共用すると、一方の環境における同期操作により、もう一方の環境の文書が削除される場合があります。
1.  連携設定で指定するAPIキーは、サイトの設定情報の一部として平文で保存されます。画面上はマスクした文字列（\*\*\*\*\*\***）を表示しますが、保存値そのものは平文です。エクスポートしたサイトパッケージには平文で記載されますので、サイトパッケージの取り扱いには注意してください。
1.  OpenAIでは無料で使用できるストレージ容量に制限があります。課金を避けたい場合は、不要なファイルを削除する必要があります。
1.  連携設定のEndpointと[AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータProviderEndpoints.OpenAiが未設定の場合、エラーとなります。ただし[AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータAllowInsecureLoopbackEndpointをtrueに設定した場合に限り、ループバックアドレスへのHTTP接続だけが許可されます。ループバック以外のホストへのHTTP接続は、AllowInsecureLoopbackEndpointがtrueでも拒否されます。この検査は保存時には行われず、連携の実行時に行われます。

## 制限事項

1.  マークダウンファイルはレコードを更新したユーザの権限で出力されます。そのユーザに閲覧権限のない項目の値は空文字列で出力されます。
1.  登録状態の確認で連携先から空の応答、不正なJSON、状態のない応答、未知の状態が返されたときは、一時的な確認失敗として既定では10回まで再確認します（この回数は[AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータRag.IndexCheckMaxAttemptsで変更できます）。10回確認しても連携先から正しい応答を得られない場合は、ジョブが失敗します。この場合、連携文書の再送は行いません。再送が行われるのは、連携先が「失敗」または「取り消し」を返した場合だけです。

## 前提条件

1.  設定を変更するには「サイトの管理」権限が必要です。
1.  [AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータEnabledをtrueに設定してください。
1.  [AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータOutputFilePathに、連携文書の出力先フォルダを設定してください。未設定の場合、同期を実行するとエラーメッセージが表示されます。

## 操作手順

1.  [テーブルの管理：AI連携](../../managers-guide/manage-table/ai-connect/index.md)で「AI連携設定」を新規作成してください。
1.  「AI連携」ダイアログが開きます。下記を参考に各項目を設定してください。

    ![「AI連携」ダイアログ](https://pleasanter.org/files/images/ja/ai-integration/rag-integration/assets/60db159e9dd04f4f90f51524ab2a8098.png)

    | 項目             | 必須 | 説明                                                                                                     |
    | :--------------- | :--: | :------------------------------------------------------------------------------------------------------- |
    | ID               | —    | 設定不要です。<br>連携先を識別する番号です。自動で採番され変更できません。<br>新規作成時は表示されません。|
    | タイトル         | ○    | サイト管理者が連携先を識別するための名前を指定してください。|
    | 連携フォーマット | ○    | 下記「連携フォーマット」を参考に、マークダウンファイルの書式を指定してください。<br>初期値は[AiConnect.json](../../setup/parameters/aiconnect-json.md)のパラメータFormatTemplateです。|
    | 連携方式         | —    | 「OpenAI」を選択してください。|
    | 連携設定         | [^1]    | 下記「連携設定」を参考に、必要な情報をJSON形式で指定してください。 |
    | 無効             | —    | オンにすると、連携を行いません。|

1.  新規作成時は「追加」ボタンを、既存の設定を編集する場合は「変更」ボタンをクリックしてください。
1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

[^1]: 必須です。ただし、連携方式で「Dify」または「OpenAI」を選択した場合のみ表示されます。

## 連携フォーマット

-   プリザンターの[リマインダー](../../managers-guide/manage-table/reminders/table-management-reminder.md)や[通知](../../managers-guide/manage-table/notifications/table-management-notification-messagebody.md)の本文で利用できる記法と同じ記法を使用します。
-   角括弧（ [ と ] ）と波括弧（ { と } ）で囲んだ文字列は、以下の規則で置換されます。

    | 記法          | 内容                                                             |
    | :------------ | :--------------------------------------------------------------- |
    | [「[カラム名](../../developers-guide/dev-column-name.md)」]  |当該カラムの表示値に置換されます。<br>例：[Title]、[Status]、[Owner]、[Body] |
    | {Url}         | レコードの編集画面の絶対URLに置換されます。                        |
    | {LoginId}     | 操作者のログインIDに置換されます。|
    | {UserName}    | 操作者のユーザ名に置換されます。|
    | {MailAddress} | 操作者のメールアドレスに置換されます。|

    ```markdown title="連携フォーマットの設定例"
    # [Title]
    
    状況: [Status]
    
    URL: {Url}
    ```

## 連携設定

「連携方式」で「OpenAI」を選択すると、以下のテンプレートが「連携設定」欄に表示されます。

##### 連携設定の初期状態

```json
{
    "Endpoint": "",
    "VectorStoreId": "",
    "ApiKey": ""
}
```

| パラメータ          | 説明                                                                    |
| :------------ | :---------------------------------------------------------------------- |
| Endpoint      | OpenAIのAPIエンドポイントです。例：https\://api.openai.com/v1 |
| VectorStoreId| OpenAIのストレージIDです                                                |
| ApiKey        | OpenAIで発行したAPIキーです                                  |

各パラメータの設定値は、以下の手順で取得してください。詳細は[OpenAI API Platform Documentation](https://developers.openai.com/api/docs)を参照してください。

1.  APIエンドポイント（Endpoint）

    OpenAI PlatformのAPIエンドポイントは以下のとおりです（バージョン1.5.8.0のリリース時点）。  

    ```text
    https://api.openai.com/v1
    ```

1.  ストレージID（VectorStoreId）

    1.  [OpenAI Platform](https://platform.openai.com/)へログインしてください。
    1.  ダッシュボード左側のメニューでStorageまたはVector Storageを選択してください。
    1.  ベクトルストアが一覧表示されます。対象のベクトルストアを選択するか、新規作成してください。
    1.  画面上に表示される「vs_」から始まる文字列がベクトルストアIDです。

1.  APIキー（ApiKey）

    1.  [OpenAI Platform](https://platform.openai.com/)へログインしてください。
    1.  ダッシュボード左側のメニューでAPI Keysを選択してください。
    1.  APIキーの一覧が表示されます。対象のAPIキーを選択するか、新規作成してください。
    1.  画面に表示される「sk_」から始まる文字列がAPIキーです。

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.8.0 以降| 機能追加|
