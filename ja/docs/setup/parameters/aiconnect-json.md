---
title: AiConnect.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: aiconnect-json
shortname: AiConnect.json
created: 2026-08-24
updated: 2026-09-08
---

## 注意事項

パラメータ変更時は「[パラメータ変更時の確認事項](parameter-edit.md)」を確認してください。

## 設定値

### トップレベルパラメータ

| パラメータ名 | 設定例 | 説明 |
| :-- | :-- | :-- |
| ProviderEndpoints| { "Dify": "https\://dify.example.com/v1", "OpenAi": "https\://api.openai.com/v1" } | 連携方式ごとの接続先URLです。連携設定のテンプレートのEndpointに表示され、Endpointが空欄の場合はこのパラメータの値が使用されます。Endpointに不正な形式の値を入力した場合は、ProviderEndpointsの値へは切り替わらず、連携時にエラーとなります。|
| AllowInsecureLoopbackEndpoint | false| ループバックアドレス（localhost、127.0.0.1、[::1]）へのHTTP接続を許可するかどうかを指定します。既定値はfalseです。 |
|Rag|下記参照|RAG機能の設定のうち、連携方式ごとの接続先URL以外の設定を行います。|

### RAG以下のパラメータ

| パラメータ名 | 設定例 | 説明 |
| :-- | :-- | :-- |
| Enabled | true | 「RAG連携」全体の有効・無効を切り替えます。|
| DeleteEnabled| true| 削除連携の有効・無効を切り替えます。|
| FormatTemplate| ["# [Title]", "", "[Body]"]| 連携設定を新規作成するとき、「連携フォーマット」欄へ表示する初期値です。文字列の配列で指定します。各要素は改行で連結されます。既定値は下記「本パラメータの既定値」を参照してください。この値を変更しても、既に登録済みのAI連携設定の「連携フォーマット」は変更されません。|
| OutputFilePath| C:\\Pleasanter\\AiConnect| 連携文書（.mdファイル）の出力先となるルートフォルダを指定します。相対パスを指定した場合、プリザンターの実行フォルダが基準になります。このフォルダ配下にテナントID、サイトIDを名前とするサブフォルダが作成されます。このフォルダに対してプリザンターの実行ユーザの書き込み権限が必要です。書き込みできない場合、連携文書の出力に失敗し、連携先への登録も行われません。レコードの内容を含むデータが格納されるためアクセス権を適切に設定してください。 |
| LogSucceeded| true| 連携先への登録が成功したときに、その旨をシステムログへ出力するかどうかを指定します。大量のレコードを連携する際、システムログ出力が過多となってしまうのを防ぎます。|
| SyncRetryCount        | 2| 連携先への登録が通信エラーで失敗したときに、再試行する回数の上限です。0を指定した場合、再試行しません。また、連携方式がOpenAIで、連携設定のEndpointとProviderEndpointsのOpenAiが共に設定されていない場合は、通信を行わず設定エラーとなり、再試行しません。|
| IndexCheckMaxAttempts | 10| 連携方式が「OpenAI」の場合に、登録状態の確認を行う回数の上限です。0を指定した場合、登録確認しません。|
| DeleteRetryCount      | 2| 連携先の文書の削除が通信エラーで失敗したときや、サーバ上の「.md」ファイルの削除が一時的に失敗したときに再試行する回数の上限です。0を指定した場合、削除を再試行しません。|
|RetryAfterMaxSeconds|60|連携先がレート制限（HTTPステータス429）を返したときに、応答のRetry-Afterに従って待機する秒数の上限です。既定値は60です|

## 本パラメータファイルの既定値

```json
{
    "ProviderEndpoints": {
        "Dify": "",
        "OpenAi": ""
    },
    "AllowInsecureLoopbackEndpoint": false,
    "Rag": {
        "Enabled": false,
        "DeleteEnabled": false,
        "FormatTemplate": [
            "# [Title]",
            "",
            "| 項目 | 値 |",
            "|------|----|",
            "| 状況 | [Status] |",
            "| 管理者 | [Manager] |",
            "| 担当者 | [Owner] |",
            "| 作成者 | [Creator] |",
            "| 更新者 | [Updator] |",
            "| 更新日時 | [UpdatedTime] |",
            "",
            "## 内容",
            "",
            "[Body]",
            "",
            "## コメント",
            "",
            "[Comments]",
            "",
            "---",
            "",
            "URL: {Url}",
            ""
        ],
        "OutputFilePath": null,
        "LogSucceeded": true,
        "SyncRetryCount": 2,
        "IndexCheckMaxAttempts": 10,
        "DeleteRetryCount": 2,
        "RetryAfterMaxSeconds": 60
    }
}
```

## 対応バージョン

| 対応バージョン | 内容                 |
| -------------- | -------------------- |
| 1.5.8.0 以降   | AiConnect.jsonを追加 |
