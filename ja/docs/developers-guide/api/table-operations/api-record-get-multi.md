---
title: 複数レコード取得
category: API
order: '1100'
status: ''
parts: ''
urlstring: api-record-get-multi
translationKey: api-record-get-multi
shortname: 複数レコード取得API,レコード取得API
created: 2019-05-02
updated: 2026-07-14
---

## 概要

[API](../basics/api.md)により、指定したサイトIDの複数「レコード」を取得します。[サイト統合](../../../users-guide/table/record-authoring/edit-records/table-site-integration.md)を設定しているテーブルの場合は、統合された各レコードの情報もあわせて取得します。

## 制限事項

-   取得できるレコードの件数は、Api.json の PageSize(デフォルトで 200) が最大となります。200件以上のレコードを取得する場合は、[FAQ：APIで200レコードを超えるデータを取得したい](../../../FAQ/features-for-developers/faq-api-paging.md)を参照してください。
-   単一のレコードを取得する場合は、「[レコード取得API](api-record-get.md)」を使用してください。

## 事前準備

-   [API](../basics/api.md)を使用するためには[APIキー](../basics/api-key.md)を作成する必要があります。
-   ログインしているブラウザのセッションからアクセスする場合には[APIキー](../basics/api-key.md)を指定せずに使用可能です。

## リクエスト

下記のリクエスト形式で、JSONデータを送信します。URLは環境によって異なるため[APIのURL](../basics/api-url.md)を参照の上、適宜変更してください。レコードの[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)条件や「並べ替え」の指定は、「[開発者ガイド：JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)」に指定してください。Viewは省略可能です。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/get|
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

200件以上のレコードを取得する場合は、[FAQ：API で 200 レコードを超えるデータを取得したい](../../../FAQ/features-for-developers/faq-api-paging.md)を参照してください。

##### JSON

```
{
    "StatusCode": 200,
    "Response": {
        "Offset": 0,
        "PageSize": 200,
        "TotalCount": 2,
        "Data": [
            {
                "SiteId": 6,
                "UpdatedTime": "2021-06-11T21:26:34",
                "ResultId": 335,
                "Ver": 2,
                "Title": "Webデータベース開発株式会社",
                "Body": "",
                "Status": 0,
                "Manager": 10,
                "Owner": 10,
                "Locked": false,
                "Comments": "[]",
                "Creator": 10,
                "Updator": 12,
                "CreatedTime": "2021-05-25T16:56:00",
                "ItemTitle": "Webデータベース開発株式会社",
                "ApiVersion": 1.1,
                "ClassHash": {
                    "ClassA": "東京都練馬区",
                    "ClassB": "789-789-789"
                },
                "NumHash": {},
                "DateHash": {},
                "DescriptionHash": {},
                "CheckHash": {},
                "AttachmentsHash": {
                    "AttachmentsA": []
                }
            },
            {
                "SiteId": 6,
                "UpdatedTime": "2021-06-09T21:23:00",
                "ResultId": 336,
                "Ver": 1,
                "Title": "情報共有イノベーション研究所",
                "Body": "",
                "Status": 0,
                "Manager": 11,
                "Owner": 11,
                "Locked": false,
                "Comments": "[]",
                "Creator": 11,
                "Updator": 11,
                "CreatedTime": "2021-05-25T16:56:00",
                "ItemTitle": "情報共有イノベーション研究所",
                "ApiVersion": 1.1,
                "ClassHash": {
                    "ClassA": "東京都新宿区",
                    "ClassB": "333-333-333"
                },
                "NumHash": {},
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
<summary>1. 全レコードを取得する</summary>

指定したサイトのレコード全件を取得します。

##### Python(api_record_get_multi_p1.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

# 指定サイトのレコード全件を取得
def get_records():
    url = f"{BASE_URL}/api/items/{SITE_ID}/get"
    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
    }
    resp = requests.post(url, json=payload)
    resp.raise_for_status()
    data = resp.json()
    return data["Response"]["Data"]

if __name__ == "__main__":
    for row in get_records():
        print(row["Title"], row["ClassHash"]["ClassA"])
```

##### 実行

```
>python api_record_get_multi_p1.py
```

##### 実行結果

```
サンプル案件E 改善要望
サンプル案件D 問い合わせ
サンプル案件C 障害
サンプル案件B 改善要望
サンプル案件A 問い合わせ
```

</details>
<details markdown="1">
<summary>2. 日付範囲でレコードを取得する</summary>

日付範囲を指定し対象のレコードを取得します。

##### Python(api_record_get_multi_p2.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

# 日付範囲を指定しレコードを取得する
def get_by_date(start, end):
    url = f"{BASE_URL}/api/items/{SITE_ID}/get"

    view = {
        "ColumnFilterHash": {
            "DateA": f'["{start} 00:00:00,{end} 23:59:59"]'
        },
        "ColumnSorterHash": {"DateA": "asc"},
    }

    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
        "View": view,
    }

    resp = requests.post(url, json=payload)
    resp.raise_for_status()
    data = resp.json()
    return data["Response"]["Data"]

if __name__ == "__main__":
    # 日付範囲 2025/01/01〜2025/01/13 で取得
    data = get_by_date("2025/01/01", "2025/01/13")
    for row in data:
        print(row["Title"], row["ClassHash"]["ClassA"], row["DateHash"]["DateA"])
```

##### 実行

```
>python api_record_get_multi_p2.py
```

##### 実行結果

```
サンプル案件A 問い合わせ 2025-01-10T00:00:00
サンプル案件B 改善要望 2025-01-11T00:00:00
サンプル案件C 障害 2025-01-12T00:00:00
```
</details>
<details markdown="1">
<summary>3. ステータスで絞り込む</summary>

ステータスを指定しレコードを取得します。ステータスは表示名で取得します。

##### Python(api_record_get_multi_p3.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

# ステータスを指定しレコードを取得する（ステータスは表示名で取得する）
def get_by_status(status_codes):
    url = f"{BASE_URL}/api/items/{SITE_ID}/get"

    view = {
        "ColumnFilterHash": {"Status": f"{status_codes}"},
        "ColumnSorterHash": {"DateA": "asc"},
        "ApiColumnKeyDisplayType": "ColumnName",
        "ApiColumnValueDisplayType": "DisplayValue",
        "ApiDataType": "KeyValues",
    }

    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
        "View": view,
    }

    resp = requests.post(url, json=payload)
    resp.raise_for_status()
    data = resp.json()
    return data["Response"]["Data"]

if __name__ == "__main__":
    # ステータス100 or 200を取得
    data = get_by_status('["100","200"]')
    for row in data:
        print(row["Title"], row["ClassA"], row["Status"])
```

##### 実行

```
>python api_record_get_multi_p3.py
```

##### 実行結果

```
サンプル案件A 問い合わせ 進行中
サンプル案件B 改善要望 未着手
サンプル案件C 障害 進行中
```

</details>
<details markdown="1">
<summary>4. 特定の文字列を検索（部分一致）しレコードを取得する</summary>

特定の文字列を検索（部分一致）しレコードを取得します。

##### Python(api_record_get_multi_p4.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

# 特定の文字列を検索（部分一致）しレコードを取得する
def get_by_text(text):
    url = f"{BASE_URL}/api/items/{SITE_ID}/get"

    view = {
        "ColumnFilterHash": {"DescriptionA": f"{text}"},
        "ColumnSorterHash": {"DateA": "asc"},
        "ColumnFilterSearchTypes": {"DescriptionA": "PartialMatch"},
    }

    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
        "View": view,
    }

    resp = requests.post(url, json=payload)
    resp.raise_for_status()
    data = resp.json()
    return data["Response"]["Data"]

if __name__ == "__main__":
    # 「リリース」という文字列で検索
    data = get_by_text("リリース")
    for row in data:
        print(
            row["Title"],
            row["ClassHash"]["ClassA"],
            row["DescriptionHash"]["DescriptionA"],
        )
```

##### 実行

```
>python api_record_get_multi_p4.py
```

##### 実行結果

```
サンプル案件B 改善要望 次期リリース候補
サンプル案件E 改善要望 仕様確定しリリース済
```

</details>
<details markdown="1">
<summary>5. 特定の項目だけ取得する</summary>

任意の項目のみを指定しレコードを取得します。

##### Python(api_record_get_multi_p5.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

# 特定の項目だけを指定し取得する
def get_selected_columns():
    url = f"{BASE_URL}/api/items/{SITE_ID}/get"

    view = {
        "ApiDataType": "KeyValues",
        "GridColumns": ["Title", "Status", "DateA", "NumA"],
    }

    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
        "View": view,
    }

    resp = requests.post(url, json=payload)
    resp.raise_for_status()
    data = resp.json()
    return data["Response"]["Data"]

if __name__ == "__main__":
    records = get_selected_columns()

    # --- コンソール出力例 ---
    for rec in records:
        print(rec["案件名"], rec["状況"], rec["登録日"], rec["見積工数"])
```

##### 実行

```
>python api_record_get_multi_p5.py
```

##### 実行結果

```
サンプル案件E 完了 2025/01/20 10.0
サンプル案件D 完了 2025/01/15 2.0
サンプル案件C 進行中 2025/01/12 4.0
サンプル案件B 未着手 2025/01/11 16.0
サンプル案件A 進行中 2025/01/10 8.0
```

</details>
<details markdown="1">
<summary>6. 200件を超えるレコードを取得する</summary>

200件を超えるレコードを取得します。

##### Python(api_record_get_multi_p6.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

# 指定サイトの200件を超えるレコード全件を取得
def fetch_all_records():
    url = f"{BASE_URL}/api/items/{SITE_ID}/get"

    offset = 0
    all_rows = []

    while True:
        # Offsetを指定してページを進める
        payload = {
            "ApiVersion": 1.1,
            "ApiKey": API_KEY,
            "Offset": offset,
        }

        res = requests.post(
            url, json=payload, headers={"Content-Type": "application/json"}
        )
        res.raise_for_status()
        data = res.json()

        response = data["Response"]
        rows = response["Data"]
        total = response["TotalCount"]  # 全件数
        page_size = response[
            "PageSize"
        ]  # 1回の取得上限（Api.json の PageSize、デフォルト200）
        current_offset = response["Offset"]

        # 今回分を追加
        all_rows.extend(rows)

        print(f"Offset={current_offset}, 取得件数={len(rows)}, 全件={total}")

        # (開始位置 + 一度に取得できる件数) > 全件 になったら末尾まで取得済み
        if current_offset + page_size >= total:
            break

        # 次ページの開始位置に Offset を進める
        offset = current_offset + page_size
    return all_rows

if __name__ == "__main__":
    records = fetch_all_records()
    print(f"最終的な取得件数: {len(records)} 件")

    for r in records:
        print(r["Title"], r["ClassHash"]["ClassA"])
```

##### 実行

```
>python api_record_get_multi_p6.py
```

##### 実行結果

```
Offset=0, 取得件数=200, 全件=350
Offset=200, 取得件数=150, 全件=350
最終的な取得件数: 350 件
サンプル案件A 問い合わせ
サンプル案件B 改善要望
サンプル案件C 障害
サンプル案件D 問い合わせ
サンプル案件E 改善要望
サンプル案件A 問い合わせ
・・・・・
```

</details>

## 関連情報

-   [開発者ガイド：API](../basics/api.md)
-   [テーブル機能：サイト統合](../../../users-guide/table/record-authoring/edit-records/table-site-integration.md)
-   [開発者ガイド：API：APIキーの作成](../basics/api-key.md)
-   [開発者ガイド：API：APIのURL](../basics/api-url.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [開発者ガイド：JSONデータレイアウト：Item](../../json-data-layout/api-item.md)
-   [FAQ：API で 200 レコードを超えるデータを取得したい](../../../FAQ/features-for-developers/faq-api-paging.md)
