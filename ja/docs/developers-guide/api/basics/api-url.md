---
title: APIのURL
category: API
order: '10'
status: ''
parts: ''
urlstring: api-url
translationKey: api-url
shortname: APIのURL
created: 2021-06-13
updated: 2023-10-25
---

## 概要

[API](api.md)を操作する際に指定するURLについて説明します。URLは環境によってサーバ名やパスが異なりますので、サンプルコードを適宜読み替えて実行してください。

## 詳細情報

[API](api.md)のURLは下記の形式で記述します。  
※{パス}は環境により省略される場合があります。

##### URL

```
http://{サーバー名}/{パス}/api/{コントローラー名}/{ID}/{メソッド名}
```

## URLの例

下記は各環境におけるURLの例です。サーバ名やパスはセットアップの状況によっては異なる場合があります。実際に利用しているURLを確認して適宜変更してください。

|No|環境|サーバ名|パス|URLの例|
|:----|:----|:----|:----|:----|
|1|Community Edition  Enterprise Edition|localhost|なし|http\://localhost/api/items/100/get|
|2|Pleasanter.net|pleasanter.net|fs|https\://pleasanter.net/fs/api/items/100/get|

## 関連情報

-   [開発者ガイド：API](api.md)