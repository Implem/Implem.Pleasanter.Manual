---
title: メール送信
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-mail
translationKey: api-mail
shortname: メール送信API
created: 2020-10-06
updated: 2026-08-12
---

## 概要

「メール送信API」を使用してメールの送信をすることができます。  

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。  

## リクエスト

下記のリクエスト形式で、JSONデータを送信します。

| 設定項目     | 値                                                               |
| :----------- | :--------------------------------------------------------------- |
| HTTPメソッド | POST                                                             |
| Content-Type | application/json                                                 |
| 文字コード   | UTF-8                                                            |
| URL          | http://{サーバ名}/api/items/{レコードID}/OutgoingMails/Send [^1] |
| Body         | 以下のJSONデータを参考のこと                                     |

[^1]:
    {サーバ名}、{レコードID}の部分は、適宜、環境に合わせて編集してください。
    Pleasanter.netの場合は以下の形式になります。

    ``` text
    https://pleasanter.net/fs/api/items/{レコードID}/OutgoingMails/Send  
    ```

### JSONデータの必須項目

| 項目        | 必須 | 備考                                                                                                                                             |
| :---------- | :--- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| ApiVersion  | 〇   |                                                                                                                                                  |
| ApiKey      | 〇   |                                                                                                                                                  |
| From        | -    |                                                                                                                                                  |
| To          | -    |                                                                                                                                                  |
| Cc          | -    |                                                                                                                                                  |
| Bcc         | -    |                                                                                                                                                  |
| Title       | 〇   |                                                                                                                                                  |
| Body        | -    |                                                                                                                                                  |
| Attachments | -    | 以下のプロパティを設定してください。<br>Name : ファイル名<br>Base64 : 添付ファイルをBase64エンコードした文字列<br>ContentType : コンテンツタイプ |

``` json title="リクエストサンプル" linenums="1" hl_lines="4"
{
     "ApiVersion": 1.1,
     "ApiKey": "[設定したAPIキー]",
     "From": "[Mail.jsonのFixedFrom値]",
     "To": "[受信側メールアドレス]",
     "Cc": "[受信側Ccメールアドレス]",
     "Bcc": "[受信側Bccメールアドレス]",
     "Title": "メール送信APIのテストです",
     "Body": "メール送信APIのテストでメールを送信します。",
     "Attachments": [
         {
             "Name": "sample1.txt",
             "Base64": "c2FtcGxlMS50eHQ=...",
             "ContentType": "text/plain"
         },
         {
             "Name": "sample2.txt",
             "Base64": "c2FtcGxlMi50eHQ=...",
             "ContentType": "text/plain"
         }
     ]
}
```

FixedFrom値については、[Mail.json](../../../setup/parameters/mail-json.md)を参照してください 。

## レスポンス

下記の形式のJSONデータが返却され、メールが送信されます。

``` json title="レスポンスサンプル" linenums="1"
{
    "Id": <レコードID>,
    "StatusCode": 200,
    "Message": "メールを送信しました。"
}
```

## 参考（PostmanによるHTTPリクエスト送信）

content-typeはHeadersから設定しています。

![Postmanでメール送信のHTTPリクエストを送信する画面](https://pleasanter.org/files/images/ja/developers-guide/api/mail/assets/3ca1574784524b0e8012bc35a91aefe4.png)

## エラー時の確認事項

-   [API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
-   [FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 対応バージョン

| 対応バージョン | 内容              |
| :------------- | :---------------- |
| 1.2.4.0 以降   | Attachmentsを追加 |

## 関連情報

-   [開発者ガイド：API：APIキーの作成](../basics/api-key.md)
-   [パラメータ設定：Mail.json](../../../setup/parameters/mail-json.md)
-   [FAQ：API実行でエラーになる](../../../FAQ/features-for-developers/faq-api.md)
-   [FAQ：変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)
