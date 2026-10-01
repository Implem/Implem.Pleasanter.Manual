---
title: レコード削除
category: API
order: '1500'
status: ''
parts: ''
urlstring: api-record-delete
translationKey: api-record-delete
shortname: ''
created: 2019-05-02
updated: 2026-07-14
---

## 概要

APIを使用してレコードを削除することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記の形式のjsonデータを送信してください。  

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{レコードID}/delete (※1)|

(※1){サーバ名}、{レコードID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{レコードID}/delete  

##### JSON

```
{
     "ApiVersion": 1.1,
     "ApiKey": "Asfas63dsf1A0faA567A..."
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9995,
    "Message": "\" {レコードのタイトル名} \" を削除しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. レコードIDを指定して削除する</summary>

状況が’910’のレコードを取得、取得できたIDでレコードを削除します。

##### Python(api_record_delete_p1.py)

```python
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# サーバ名、APIキー
BASE_URL = "【サーバ名】"  # 例: http://server
API_KEY = "【APIキー】"

# 検索開始サイトID
START_SITE_ID = 【サイトID】

# 対象サイト名と削除対象ステータス
TARGET_SITE_NAME = "【サイト名】"
TARGET_STATUS = '["910"]'

# セッション共通化
session = requests.Session()
session.headers.update({"Content-Type": "application/json"})

# JSON POST リクエスト共通関数
def post_json(url: str, payload: dict) -> dict:
    r = session.post(url, data=json.dumps(payload))
    if not r.ok:
        raise RuntimeError(f"HTTP {r.status_code} {url}\n{r.text}")
    return r.json()

# 1) サイト名から SiteId を取得
getclosest_url = f"{BASE_URL}/api/items/{START_SITE_ID}/getclosestsiteid"
closest_payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "FindSiteNames": [TARGET_SITE_NAME],
}

closest_res = post_json(getclosest_url, closest_payload)
data_list = closest_res.get("Data", [])
if not data_list:
    print(f"{TARGET_SITE_NAME} サイト情報取得失敗")
    raise SystemExit()

site_id = data_list[0].get("SiteId")

if not isinstance(site_id, int) or site_id <= 0:
    print(f"{TARGET_SITE_NAME} サイトID不正: {site_id}")
    raise SystemExit()

print(f"対象サイトID取得成功: {site_id}")

# 2) Status=910 のレコード取得（複数取得）
get_url = f"{BASE_URL}/api/items/{site_id}/get"
get_payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "View": {
        "ColumnFilterHash": {
            "Status": TARGET_STATUS,
        }
    },
}

get_res = post_json(get_url, get_payload)

rows = []
if isinstance(get_res, dict):
    rows = (get_res.get("Response", {}) or {}).get("Data", []) or []
elif isinstance(get_res, list):
    rows = get_res

if not rows:
    print("削除対象データなし")
    raise SystemExit()

# 3) 取得したレコードを 1件ずつ削除
for row in rows:
    record_id = row.get("ResultId") or row.get("Id")
    if not record_id:
        continue

    delete_url = f"{BASE_URL}/api/items/{record_id}/delete"
    delete_payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
    }

    try:
        post_json(delete_url, delete_payload)
        print(f"削除成功：Id={record_id}")
    except Exception as e:
        print(f"削除失敗：Id={record_id}")
        print(e)
```

##### 実行

```
>python api_record_delete_p1.py
```

##### 実行結果

```
削除成功：Id=9001
削除成功：Id=9002
削除成功：Id=9003
削除成功：Id=9004
・・・・
```
</details>

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2019年10月よりAPIの仕様が一部変更となりました。**
- 分類, 数値, 日付, 説明, チェック項目はjsonにそのまま記載する方法から「～Hash」の中に記載する方法へ変更されました。

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。