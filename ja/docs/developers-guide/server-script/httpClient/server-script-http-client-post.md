---
title: httpClient.Post
icon: material/alpha-m-box
category: サーバスクリプト
order: '65020'
status: ''
parts: ''
urlstring: server-script-http-client-post
translationKey: server-script-http-client-post
shortname: httpClient.Post
created: 2021-11-14
updated: 2023-08-21
---

## 概要

[サーバスクリプト](../index.md)で[httpClient](index.md)を使用してPOSTメソッドを発行する際に使用します。

## 構文

```
httpClient.Post();
```

## パラメータ

パラメータはありません。

## 戻り値

string型の戻り値

## 使用例

以下の例では、外部のAPIサーバにPOSTメソッドを発行し、結果をログに出力します。

##### JavaScript

MediaType: application/json の例
```
let data = {
    data1: 'abc',
    data2: '123'
}
httpClient.RequestUri = 'https://servername/api/.....';
httpClient.Content = JSON.stringify(data);
let response = httpClient.Post();
if(httpClient.IsSuccess) {
    context.Log('Success: ' + response);
}else{
    context.Log('Error: (' + httpClient.StatusCode + ')' + response);
}
```

MediaType: application/x-www-form-urlencoded の例
```
let data = {
    data1: 'abc',
    data2: '123'
}
httpClient.RequestUri = 'https://servername/api/.....';
httpClient.MediaType = 'application/x-www-form-urlencoded';
httpClient.Content = createParameters(data);
let response = httpClient.Post();
if(httpClient.IsSuccess) {
    context.Log('Success: ' + response);
}else{
    context.Log('Error: (' + httpClient.StatusCode + ')' + response);
}
//オブジェクトをURLエンコードしたパラメータ形式に変換する関数
function createParameters(obj) {
    let result =[];
    for(var key in obj) {
        result.push(encodeURIComponent(key) + '=' +encodeURIComponent(obj[key]));
    }
    return result.join('&');
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：httpClient](index.md)

