---
title: httpClient.Put
icon: material/alpha-m-box
category: サーバスクリプト
order: '65030'
status: ''
parts: ''
urlstring: server-script-http-client-put
translationKey: server-script-http-client-put
shortname: httpClient.Put
created: 2021-11-14
updated: 2023-08-21
---

## 概要

[サーバスクリプト](../index.md)で[httpClient](index.md)を使用してPUTメソッドを発行する際に使用します。

## 構文

```
httpClient.Put();
```

## パラメータ

パラメータはありません。

## 戻り値

string型の戻り値

## 使用例

以下の例では、外部のAPIサーバにPUTメソッドを発行し、結果をログに出力します。

##### JavaScript

```
let data = {
    data1: 'abc',
    data2: '123'
}
httpClient.RequestUri = 'https://servername/api/.....';
httpClient.Content = JSON.stringify(data);
let response = httpClient.Put();
if(httpClient.IsSuccess) {
    context.Log('Success: ' + response);
}else{
    context.Log('Error: (' + httpClient.StatusCode + ')' + response);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：httpClient](index.md)