---
title: 組織作成
category: API
order: '0'
status: ''
parts: ''
urlstring: api-dept-create
translationKey: api-dept-create
shortname: ''
created: 2022-10-24
updated: 2026-09-08
---

## 概要

APIを使用して新規にレコードを作成することができます。  

## 事前準備

- APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。  
- この機能を実行するための API キーを払い出すユーザにはテナント管理者権限が付与されている必要があります。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/depts/create (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/depts/create

## リクエスト

##### JSON  

```
{
    "ApiVersion": 1.1,
    "ApiKey": "017dRapJ3f5f1Dgsdj95...",
    "DeptCode": "[登録する組織の組織コード]",
    "DeptName": "[登録する組織の名前]",
    "Body": "[登録する組織の説明]"
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

<>

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "Message": "\"登録する組織の組織コード\" を作成しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. JSONファイルを読み込み組織を作成</summary>

JSONファイルに指定された組織情報をPythonプログラムで読み込み、組織を作成します。

##### JSON(api_dept_create.json)

```
[
    { "DeptCode": "DEV001", "DeptName": "開発部", "Body": "開発" },
    { "DeptCode": "DEV002", "DeptName": "営業部", "Body": "営業" },
    { "DeptCode": "DEV003", "DeptName": "総務部", "Body": "総務" }
]
```

##### Python(api_dept_create.py)

```
import json
import requests

# サーバ名、APIキー、JSONファイルパスを指定
BASE_URL = "【サーバー名】"
API_KEY = "【APIキー】"
JSON_PATH = "api_dept_create.json"
# JSONファイル読み込み
with open(JSON_PATH, encoding="utf-8") as f:
    records = json.load(f)
# 各レコードをAPIで登録
for r in records:
    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
        "DeptCode": r["DeptCode"],
        "DeptName": r["DeptName"],
        "Body": r.get("Body", ""),
    }
    res = requests.post(
        f"{BASE_URL}/api/depts/create",
        json=payload,
        headers={"Content-Type": "application/json"},
    )
    print(r["DeptCode"], res.status_code, res.text)

```

##### 実行

```
>python api_dept_create.py
```

##### 実行結果

```
DEV001 200 {"Id":31,"StatusCode":200,"Message":"\" 開発部 \" を作成しました。"}
DEV002 200 {"Id":32,"StatusCode":200,"Message":"\" 営業部 \" を作成しました。"}
DEV003 200 {"Id":33,"StatusCode":200,"Message":"\" 総務部 \" を作成しました。"}
```
</details>

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)