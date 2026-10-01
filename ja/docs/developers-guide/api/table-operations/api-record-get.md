---
title: 単一レコード取得
category: API
order: '1000'
status: ''
parts: ''
urlstring: api-record-get
translationKey: api-record-get
shortname: レコード取得API
created: 2019-05-02
updated: 2026-07-14
---

## 概要

[API](../basics/api.md)により、指定したIDの「レコード」を取得します。

## 制限事項

-   複数のレコードを一括で取得する場合は、[複数レコード取得API](api-record-get-multi.md)を使用してください。

## 事前準備

-   [API](../basics/api.md)を使用するためには[APIキー](../basics/api-key.md)を作成する必要があります。
-   ログインしているブラウザのセッションからアクセスする場合には[APIキー](../basics/api-key.md)を指定せずに使用可能です。

## リクエスト

下記のリクエスト形式で、JSONデータを送信します。URLは環境によって異なるため[APIのURL](../basics/api-url.md)を参照の上、適宜変更してください。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/{パス}/api/{コントローラ名}/{レコードID}/get|
|Body|以下のjsonデータを参考のこと|

### JSON  

```
{
     "ApiVersion": 1.1,
     "ApiKey": "63Kfk0ds3d4S2DBsa32..."
}
```

## レスポンス

下記の形式のJSONデータが返却されます。Response部分のデータのレイアウトは[JSONデータレイアウト：Item](../../json-data-layout/api-item.md)を参照してください。

##### JSON

``` 
{
    "StatusCode": 200,
    "Response": {
        "Data": [
            {
                "SiteId": 7,
                "UpdatedTime": "2021-06-12T11:26:26",
                "IssueId": 340,
                "Ver": 2,
                "Title": "AI技術の検証",
                "Body": "プロジェクトマネジメントにおけるリスクの早期発見を目的としたAI技術の検証を行いたいとの依頼がありました。\r\n今期は進捗管理のデータや電子メールのデータ等を活用し問題が発生しやすいプロジェクトの共通点を発見するための技術検証を行います。\r\nまずはプロジェクトを具体化するための要件定義フェーズを商談化します。",
                "StartTime": "1899-12-30T00:00:00",
                "CompletionTime": "2021-06-18T00:00:00",
                "WorkValue": 0.0,
                "ProgressRate": 0.0,
                "Status": 100,
                "Manager": 17,
                "Owner": 17,
                "Locked": false,
                "Comments": "[]",
                "Creator": 17,
                "Updator": 2,
                "CreatedTime": "2021-05-25T16:56:00",
                "ItemTitle": "AI技術の検証",
                "ApiVersion": 1.1,
                "ClassHash": {
                    "ClassA": "338",
                    "ClassB": "コンサルティング",
                    "ClassC": "90%"
                },
                "NumHash": {
                    "NumA": 1500000.0,
                    "NumB": 1180000.0,
                    "NumC": 320000.0,
                    "NumD": 21.3
                },
                "DateHash": {},
                "DescriptionHash": {},
                "CheckHash": {},
                "AttachmentsHash": {
                    "AttachmentsA": []
                }
            }
        ]
    }
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。  

<details markdown="1">
<summary>1. レコードIDを指定しCSVを出力</summary>

任意のレコードを取得し、CSVファイルを出力します。

##### Python(api_record_get.py)

```
import requests
import csv

# サーバ名、APIキー、レコードID、CSVファイル名を指定
BASE_URL = "【サーバー名】"
API_KEY = "【APIキー】"
RECORD_ID = 【レコードID】
CSV_PATH = "api_record_get.csv"

# 単一レコード取得APIでレコード情報を1件取得する関数
def get_record(base_url: str, record_id: int, api_key: str) -> dict:
    url = f"{base_url}/api/items/{record_id}/get"

    payload = {
        "ApiVersion": 1.1,
        "ApiKey": api_key,
    }

    headers = {"Content-Type": "application/json"}

    res = requests.post(url, json=payload, headers=headers)
    res.raise_for_status()

    data = res.json()

    # レコード本体は Response.Data[0] に入っている
    item_list = data.get("Response", {}).get("Data", [])
    if not item_list:
        raise ValueError("レコードが取得できませんでした。")

    return item_list[0]

def write_record_to_csv(record: dict, csv_path: str):
    row = {
        "会社名": record.get("Title"),
        "会社概要": record.get("Body"),
        "設立日": record.get("DateHash", {}).get("DateC"),
        "業種": record.get("ClassHash", {}).get("ClassF"),
    }

    fieldnames = list(row.keys())

    # UTF-8 (BOM付き)
    with open(csv_path, "w", newline="", encoding="utf-8-sig") as f:
        writer = csv.DictWriter(f, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerow(row)

if __name__ == "__main__":
    record = get_record(BASE_URL, RECORD_ID, API_KEY)
    write_record_to_csv(record, CSV_PATH)
    print(f"レコード {RECORD_ID} を {CSV_PATH} に出力しました。")

```

##### 実行

```
>python api_record_get.py
```

##### 実行結果

```
レコード {レコードID} を api_record_get.csv に出力しました。
```
</details>

## 関連情報

-   [開発者ガイド：API](../basics/api.md)
-   [開発者ガイド：API：テーブル操作：複数レコード取得](api-record-get-multi.md)
-   [開発者ガイド：API：APIキーの作成](../basics/api-key.md)
-   [開発者ガイド：API：APIのURL](../basics/api-url.md)
-   [開発者ガイド：JSONデータレイアウト：Item](../../json-data-layout/api-item.md)