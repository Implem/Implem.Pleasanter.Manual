---
title: httpClient.Patch
icon: material/alpha-m-box
category: サーバスクリプト
order: '65030'
status: ''
parts: ''
urlstring: server-script-http-client-patch
translationKey: server-script-http-client-patch
shortname: httpClient.Patch
created: 2023-12-07
updated: 2023-12-13
---

## 概要

[サーバスクリプト](../index.md)で[httpClient](index.md)を使用してPATCHメソッドを発行する際に使用します。

## 構文

```
httpClient.Patch();
```

## パラメータ

パラメータはありません。

## 戻り値

string型の戻り値

## 使用例

以下の例では、外部のAPIサーバにPATCHメソッドを発行し、結果をログに出力します。

##### JavaScript

```
let data = {
    data1: 'abc',
    data2: '123'
}
httpClient.RequestUri = 'https://servername/api/.....';
httpClient.Content = JSON.stringify(data);
let response = httpClient.Patch();
if (httpClient.IsSuccess) {
    context.Log('Success: ' + response);
} else {
    context.Log('Error: (' + httpClient.StatusCode + ')' + response);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：httpClient](index.md)