---
title: httpClient
icon: material/alpha-o-box
category: サーバスクリプト
order: '65000'
status: ''
parts: ''
urlstring: server-script-http-client
translationKey: server-script-http-client
shortname: httpClient
created: 2021-11-14
updated: 2025-09-09
---

## 概要

[サーバスクリプト](../index.md)で外部のサービスと接続するためのHTTPクライアントを利用する際に使用します。

## プロパティ

|No|Name|Get|Set|Type|Description|
|:----|:----|:----|:----|:----|:----|
|1|RequestUri|○|○|string|接続先のURI|
|2|Content|○|○|string|送信するデータ|
|3|Encoding|○|○|string|エンコーディング(既定値は "utf-8")|
|4|MediaType|○|○|string|メディアの種類(既定値は "application/json")|
|5|RequestHeaders|○||Dictionary<string,string>|リクエストヘッダ。詳細は下記参照。|
|6|ResponseHeaders|○||Dictionary<string,IList<string>>|レスポンスヘッダ。詳細は下記参照。|
|7|IsSuccess|○||bool|直前に発行したリクエストが成功したか否かを取得。StatusCodeが200～299の範囲にある場合にTrueを返します|
|8|StatusCode|○||int|直前に発行したリクエストに対する応答メッセージのステータスコード|
|9|TimeOut|○|○|int|HTTPリクエストのタイムアウト時間をミリ秒で指定。<br>[Script.json](../../../setup/parameters/script-json.md) に記載された "ServerScriptHttpClientTimeOutMin" ～ "ServerScriptHttpClientTimeOutMax" の範囲で設定可能。<br>(既定値は、[Script.json](../../../setup/parameters/script-json.md) の "ServerScriptHttpClientTimeOut" に設定された値)|
|10|IsTimeOut|○||bool|直前に発行したリクエストがタイムアウトで中断したか否かを取得。タイムアウトした場合にTrueを返します。|

### RequestHeadersプロパティの使用例

下記の様に、RequestHeadersプロパティの Add メソッドを使用することで、任意のリクエストヘッダを追加できます。

```javascript
httpClient.RequestHeaders.Add({ヘッダ名}, {値});
```

#### AuthorizationヘッダでBasic認証を行う場合

```javascript
let base64 = utilities.ConvertToBase64String('userName:password');
httpClient.RequestHeaders.Add("Authorization", "Basic " + base64);
httpClient.RequestUri= "https://servername/api/.....";
let result = httpClient.Get();
```
※文字列をBase64に変換するには、[utilities.ConvertToBase64String](../utilities/server-script-utilities-convert-to-base64-string.md)メソッドが利用可能です。

また、続けて別のヘッダを設定して送信する場合は、Clearメソッドでヘッダの内容をリセットしてください。
```javascript
httpClient.RequestHeaders.Clear();
httpClient.RequestHeaders.Add("Authorization", "Bearer " + "X2kKRHGI495Y.......");
```

### ResponseHeadersプロパティの使用例

下記のように外部APIにアクセスした際、ResponseHeadersプロパティの Item.get メソッドを使用することで、任意のレスポンスヘッダのプロパティ値を取得することができます。

``` javascript
httpClient.ResponseHeaders.Item.get({レスポンスヘッダのプロパティ名})
```

#### Access-Control-Allow-Originプロパティの値をレスポンスヘッダから取得したい場合

``` javascript
// 外部APIに接続
httpClient.RequestUri="https://savername/api/......";
let response = httpClient.Get();

// レスポンスヘッダを取得
var value = httpClient.ResponseHeaders.Item.get("Access-Control-Allow-Origin");
context.Log(value[0]);
```

また、続けて送信しレスポンスヘッダのプロパティ値を取得する場合は、Clearメソッドであらかじめヘッダの内容をリセットしてください。
```javascript
httpClient.RequestUri="https://savername/api/....../123/...";
let response = httpClient.Get();
var value = httpClient.ResponseHeaders.Item.get("Access-Control-Allow-Origin");
context.Log(value[0]);
// 続けて送信する前にResponseHeadersをクリア
httpClient.ResponseHeaders.Clear();
httpClient.RequestUri="https://savername/api/....../456/...";
response = httpClient.Get();
```

### TimeOutプロパティの使用例

下記の例では、リクエストを送信する前に TimeOut プロパティに値を設定することで、リクエストのタイムアウト時間を変更できます。

```javascript
httpClient.RequestUri= "https://servername/api/.....";
httpClient.TimeOut = 300000;
let result = httpClient.Get();
```

### IsTimeOutプロパティの使用例

下記の例では、リクエストが失敗した場合に失敗した理由がタイムアウトかどうかを判定し、タイムアウトだった場合は再度HttpClientGetを実行します。

```javascript
let response = httpClient.Get();
if (!httpClient.IsSuccess) {  //リクエストに失敗した
    if (httpClient.IsTimeOut) {  //タイムアウトによる中断だった
        response = httpClient.Get();  //リトライ
    }
}
```

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|[Delete](server-script-http-client-delete.md)|DELETEメソッドを発行し結果を受け取ります。|
|2|[Get](server-script-http-client-get.md)|GETメソッドを発行し結果を受け取ります。|
|3|[Patch](server-script-http-client-patch.md)|PATCHメソッドを発行し結果を受け取ります。|
|4|[Post](server-script-http-client-post.md)|POSTメソッドを発行し結果を受け取ります。|
|5|[Put](server-script-http-client-put.md)|PUTメソッドを発行し結果を受け取ります。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.16.0以降|HttpClientを追加|
|1.3.9.0以降|RequestHeadersを追加|
|1.3.50.0以降|HttpClientのPatchメソッドを追加|
|1.4.8.0以降|ResponseHeadersを追加|
|1.4.19.0以降|TImeOutを追加|
|1.4.20.0以降|IsTImeOutを追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)
-   [開発者ガイド：サーバスクリプト：utilities.ConvertToBase64String](../utilities/server-script-utilities-convert-to-base64-string.md)
-   [開発者ガイド：サーバスクリプト：httpClient.Get](server-script-http-client-get.md)
-   [開発者ガイド：サーバスクリプト：httpClient.Post](server-script-http-client-post.md)
-   [開発者ガイド：サーバスクリプト：httpClient.Put](server-script-http-client-put.md)
-   [開発者ガイド：サーバスクリプト：httpClient.Delete](server-script-http-client-delete.md)
-   [開発者ガイド：サーバスクリプト：httpClient.Patch](server-script-http-client-patch.md)