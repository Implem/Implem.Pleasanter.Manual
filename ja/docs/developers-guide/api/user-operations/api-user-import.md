---
title: インポート
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-user-import
translationKey: api-user-import
shortname: ''
created: 2023-10-25
updated: 2023-10-25
---

## 概要

APIを使用してユーザ情報をインポートします。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、CSVデータとJSONパラメータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |multipart/form-data|  
|文字コード|UTF-8|
|URL|http://{サーバー名}/api/users/import (※1)|
|Body|下記「Bodyに指定する項目」を参照のこと|

(※1){サーバー名}の部分は、適宜、環境に合わせて編集してください。  

### Bodyに指定する項目

|項目名|値|
|:--|:--|  
|parameters|下記「APIパラメータ」の内容をJSON形式の文字列で指定|
|file|登録するCSVファイルのバイナリデータ|

### APIパラメータ

|項目名|設定例|備考|
|:--|:--|:--|  
|ApiVersion|1.1|APIバージョン|
|ApiKey|3da0fa3a7R61faf821...|取得したAPIキー|
|Encoding|Shift-JIS|CSVファイルのエンコーディング。"UTF-8"または"Shift-JIS"を指定|

## 実行例のサンプル

### PowerShell（version6.0 以降）のサンプル

##### PowerShell

```
$uri = 'http://servername/api/users/import'
$filePath = "./sample.csv"
$form = @{
    parameters = ConvertTo-Json @{
        ApiVersion = 1.1;
        ApiKey = "4d84b4773a58bbc3c4...";
        Encoding = "UTF-8";
    };
    file = Get-Item -Path $filePath;
}
Invoke-WebRequest -Uri $uri -Method Post -Form $form
```

### Pythonのサンプル

##### Python

```
import requests
import json

url = "https://servername/api/users/import"
filePath = "./sample.csv"
data = {
    "parameters": json.dumps({
        "ApiVersion" : 1.1,
        "ApiKey" : "4d84b4773a58bbc3c4...",
        "Encoding" : "UTF-8"
    })            
}
files = {
    "file":("sample.csv", open(filePath,"rb"), "text/csv")
}
response = requests.post(url, data, files=files)
print(response.content.decode())
```

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
  "Id":0,
  "StatusCode":200,
  "Message":"50 件追加し、12 件更新しました。"
}
```

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)
