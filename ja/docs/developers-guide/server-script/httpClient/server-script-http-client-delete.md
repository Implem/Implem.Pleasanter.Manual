---
title: httpClient.Delete
icon: material/alpha-m-box
category: サーバスクリプト
order: '65040'
status: ''
parts: ''
urlstring: server-script-http-client-delete
translationKey: server-script-http-client-delete
shortname: httpClient.Delete
created: 2021-11-14
updated: 2023-08-21
---

## 概要

[サーバスクリプト](../index.md)で[httpClient](index.md)を使用してDELETEメソッドを発行する際に使用します。

## 構文

```
httpClient.Delete();
```

## パラメータ

パラメータはありません。

## 戻り値

string型の戻り値

## 使用例

以下の例では、外部のAPIサーバにDELETEメソッドを発行し、結果をログに出力します。

##### JavaScript

```
httpClient.RequestUri = 'https://servername/api/.....';
let response = httpClient.Delete();
if(httpClient.IsSuccess) {
    context.Log('Success: ' + response);
}else{
    context.Log('Error: (' + httpClient.StatusCode + ')' + response);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：httpClient](index.md)