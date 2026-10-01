---
title: レコード一括削除
category: API
order: '1600'
status: ''
parts: ''
urlstring: api-table-bulk-delete
translationKey: api-table-bulk-delete
shortname: ''
created: 2020-10-08
updated: 2026-07-14
---

## 概要

APIを使用してレコードを一括削除します。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## 注意事項  

当機能はレコードの情報を削除する機能です。
削除レコードや削除条件項目に細心の注意を払って操作してください。  
この操作においては以下の手順を踏み、削除を行うことをおすすめ致します。

(1)[削除予定のレコード取得](api-record-get-multi.md)  

(2)取得レコードから削除レコードや削除項目を転記し、一括削除APIのリクエストを作成  
    ([view項目を使用する場合はこちらを確認](../../json-data-layout/api-view/index.md))  

(3)PhysicalDeleteオプションをチェック(trueにした場合は記録また期限付きテーブルの_deletedと_historyテーブルからも削除記録が消去され、復元ができなくなります)  

## リクエスト

下記の形式のjsonデータを送信してください。  

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/pleasanter/api/items/{サイトID}/bulkdelete (※1)|

(※1)「http://{サーバー名}/pleasanter」 の部分は、適宜、ご使用の環境に合わせて編集し、「{サイトID}」は削除するレコードが登録されているサイトのIDに置き換えてください。   
(pleasanter.netの場合はhttps://pleasanter.net/fs/api/items/{サイトID}/bulkdelete)

### 設定値

設定値には[スクリプトの$p.apiBulkDelete](../../script/script-api/script-api-bulk-delete.md) および [サーバスクリプトのitems.BulkDelete](../../server-script/items/server-script-items-bulk-delete.md) も指定できます。

|パラメータ名|型|必須|概要|
|:--|:--|:--|:--|
|ApiVersion|decimal||APIのバージョン。|
|ApiKey|string|※1|事前に作成したAPIキー。|
|View|object||一括削除するレコードの条件を指定する場合記述する。詳細は後述。|
|Selected|object||削除するレコードのIDを指定する場合、配列形式で記述。|
|All|bool||テーブルのすべてのレコードを一括削除する場合true。|
|PhysicalDelete|bool||レコード削除と同時に変更履歴およびごみ箱から削除する場合はtrue。|

※1：APIキーはAPIでは指定必須。スクリプト、サーバスクリプトは任意指定で、指定した場合はAPIキーのユーザの権限で処理を実行。

### View

|パラメータ名|型|必須|概要|
|:--|:--|:--|:--|
|ColumnFilterHash|object||一括削除するレコードの条件。詳細は [JSONデータレイアウト：View](../../json-data-layout/api-view/index.md) を参照。|

## 使用例

### 1. 項目の条件で絞ってレコードを物理削除する場合

View: {ColumnFilterHashの記述} を設定する。  
PhysicalDelete: true を設定する。

#### JSON

```
{
    ApiVersion: 1.1,
    ApiKey: "XXXXX...",
    View: {
        ColumnFilterHash: {
            Status: "[100,910]"
        }
    },
    PhysicalDelete: true
}
```

### 2. 複数レコードを選択して削除する場合（レコードIDが135,376のレコードを削除）

Selected: [対象のID] を設定する。

#### JSON

```
{
    ApiVersion: 1.1,
    ApiKey: "XXXXX...",
    Selected: [
        135,
        376
    ]
}
```

### 3. 対象テーブルの全レコードを削除する場合

All: true を設定する。

#### JSON

```
{
    ApiVersion: 1.1,
    ApiKey: "XXXXX...",
    All: true
}
```

## レスポンス

下記の形式のjsonデータが返却されます。

### 返却値

|パラメータ名|型|必須|概要|
|:--|:--|:--|:--|
|Id|long|○|一括削除対象の記録また期限付きテーブルのID。|
|StatusCode|int|○|実行結果のステータスコード。|
|Message|string|○|実行結果のメッセージ。|

## 実行結果例

### 1. サイトIDが46010のテーブルに登録されているレコードを一括削除（ごみ箱に移動）した場合

#### JSON

```
{
    Id: 46010,
    StatusCode: 200,
    Message: "サンプルテーブル: 3 件 一括削除しました。"
}
```

### 2. サイトIDが46010のテーブルに登録されているレコードを物理削除した場合

#### JSON

```
{
    Id: 46010,
    StatusCode: 200,
    Message: "2 件 物理削除しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. 削除対象レコードを取得してからIDを指定して一括削除します。</summary>

削除対象のレコードを取得（当サンプルではStatus=910）し、そのIDをbulkdeleteのリクエストに設定し削除します。

##### Python(api_record_bulkdelete_p1.py)

```python
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# サーバ名、APIキー
BASE_URL = (
    "【URL】"
)
API_KEY = "【APIキー】"

# 検索開始サイトID
START_SITE_ID = 【サイトID】

# 対象サイト名と削除対象ステータス
TARGET_SITE_NAME = "案件管理"
TARGET_STATUS = '["910"]'  # 保留(910)

# 物理削除（履歴/ゴミ箱も含めて削除）したい場合は True
PHYSICAL_DELETE = False

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

# 2) Status=910 のレコード取得（削除対象の確認用）
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

# 3) 取得したレコードIDをまとめて bulkdelete（Selected指定）
record_ids = []
for row in rows:
    rid = row.get("ResultId") or row.get("Id")
    if isinstance(rid, int) and rid > 0:
        record_ids.append(rid)

# 念のため重複排除
record_ids = sorted(set(record_ids))

if not record_ids:
    print("削除対象IDが取得できませんでした")
    raise SystemExit()

bulkdelete_url = f"{BASE_URL}/api/items/{site_id}/bulkdelete"
bulkdelete_payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "Selected": record_ids,  # ← ID配列を指定して一括削除
    "PhysicalDelete": PHYSICAL_DELETE,
}

try:
    bulk_res = post_json(bulkdelete_url, bulkdelete_payload)
    # bulkdeleteのレスポンス例: { Id: <siteId>, StatusCode: 200, Message: "..." }
    print("bulkdelete 実行結果:", bulk_res)
except Exception as e:
    print("bulkdelete 失敗")
    print(e)
```

##### 実行

```
>python api_record_bulkdelete_p1.py
```

##### 実行結果

```
対象サイトID取得成功: 9999
bulkdelete 実行結果: {'Id': 9999, 'StatusCode': 200, 'Message': '案件管理: 5 件 一括削除しました。'}
```
</details>

<details markdown="1">
<summary>2. 削除対象のレコードをフィルタし一括削除します。</summary>

削除対象のレコードをフィルタ（当サンプルではStatus=910）しbulkdeleteを実行します。

##### Python(api_record_bulkdelete_p2.py)

```python
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# サーバ名、APIキー
BASE_URL = "【URL】"
API_KEY = "【APIキー】"

# 検索開始サイトID
START_SITE_ID = 6429

# 対象サイト名と削除対象ステータス
TARGET_SITE_NAME = "案件管理"
TARGET_STATUS = '["910"]'  # 保留(910)

# 物理削除する場合は True（復元不可）
PHYSICAL_DELETE = False

# セッション共通化
session = requests.Session()
session.headers.update({"Content-Type": "application/json"})

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

# 2) View 条件を指定して bulkdelete
bulkdelete_url = f"{BASE_URL}/api/items/{site_id}/bulkdelete"
bulkdelete_payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "View": {"ColumnFilterHash": {"Status": TARGET_STATUS}},
    "PhysicalDelete": PHYSICAL_DELETE,
}

try:
    res = post_json(bulkdelete_url, bulkdelete_payload)
    print("bulkdelete 実行結果:", res)
except Exception as e:
    print("bulkdelete 失敗")
    print(e)
```

##### 実行

```
>python api_record_bulkdelete_p2.py
```

##### 実行結果

```
対象サイトID取得成功: 9999
bulkdelete 実行結果: {'Id': 9999, 'StatusCode': 200, 'Message': '案件管理: 5 件 一括削除しました。'}
```
</details>

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)
