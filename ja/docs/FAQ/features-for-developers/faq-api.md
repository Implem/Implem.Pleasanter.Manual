---
title: API実行でエラーになる
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-api
translationKey: faq-api
shortname: API
created: 2020-09-04
updated: 2024-04-29
---

## 回答

API実行時にエラーになる場合には、「URL」、「メソッド」、「リクエスト」でPOSTするパラメータの内容を確認してください。

---

## 概要

API実行時にエラーが発生する場合は、エラーの内容に応じてそれぞれの内容をチェックしてください。

## 1. URL

以下のようなエラーが表示される場合は、APIのURL（ホスト名やサブディレクトリの有無）が正しくない可能性があります。  

```
The resource you are looking for has been removed, had its name changed, or is temporarily unavailable.
```

```
HTTP Error 404.0 - Not Found  
探しているリソースは削除されたか、名前が変更されたか、または一時的に使用不可能になっています。  
```
※エラーメッセージはサーバにより異なります。  

指定するURLは環境により異なります。以下の例は、それぞれの環境でitems情報取得APIのURLです。  

### オンプレミス環境での使用  

http://192.168.1.100/api/items/999/get  
※192.168.1.100 の部分はサーバのIPアドレス等に置き換えてください。  

### クラウド - Pleasanter.netでの使用  

https://pleasanter.net/fs/api/items/999/get  

### クラウド - デモ環境での使用  

https://demo.pleasanter.org/api/items/999/get  

オンプレミス環境の場合、プリザンターを配置したパスによりURLが異なります。  
上記は、ユーザーマニュアルに沿ってインストールした場合のURLとなりますので、上記URLで動作を保証するものではございません。正しく動作しない場合は、システム管理者にお問い合わせください。  

## 2. HTTPメソッド  

プリザンターのAPIはHTTPメソッドにPOSTを使用します。  

以下のようなエラーが表示される場合は、HTTPメソッドが異なる可能性があります。  

```
403 Forbidden
```

```
 "Message": "要求されたリソースは、http メソッド 'GET' をサポートしていません。"
```

※エラーメッセージはサーバにより異なります。  

## 3. リクエスト 

プリザンターのAPIはJSON形式での記述となります。  
構文が誤っている場合、正しいリクエストとして認識されず以下のようなエラーが表示されます。  

 ```
 {"Id":0,"StatusCode":401,"Message":"認証できませんでした。"}
 ```

上記のエラーが発生する場合、  

-   JSON構文が正しくない  
-   APIキーが正しくない  

どちらかの可能性が高いので確認してください。  

JSON構文については「JSON構文チェッカー」などのサービスをご利用ください。  