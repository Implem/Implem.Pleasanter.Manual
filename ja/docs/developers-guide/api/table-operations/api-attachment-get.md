---
title: 添付ファイル取得
category: API
order: '1700'
status: ''
parts: ''
urlstring: api-attachment-get
translationKey: api-attachment-get
shortname: 添付ファイル取得API
created: 2019-12-16
updated: 2026-01-26
---

## 概要

添付ファイル項目に添付したファイルや、内容や説明項目およびコメントに貼り付けた画像ファイルの情報を取得するAPIです。

## 制限事項

1. このAPIではファイルの情報を取得します。実際のファイルを取得するためには変換処理（Base64デコード）を行ってください。変換処理は以下のFAQを参照してください。  
[FAQ：サンプルコード：添付ファイルをダウンロードする](../../../FAQ/features-for-developers/faq-download-attachment.md)

## 事前準備

1. APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/binaries/{Guid}/get(※1)|
|Body|以下のjsonデータを参考のこと|

(※1)
{サーバ名}、{Guid}の部分は、適宜、環境に合わせて編集してください。  
pleasanter.netの場合は以下の形式になります。  
https\://pleasanter.net/fs/api/binaries/{Guid}/get  

(※2)
添付ファイルのあるGuidを含むレコード情報が取得したい場合は以下のリンク先に従って取得してください。  
[API機能：単一レコード取得](api-record-get.md)  

## リクエスト

##### JSON  

```
{
     "ApiVersion": 1.1,
     "ApiKey": "234S567dStfghjkA..."
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

|取得項目|説明|
|:--|:--|
|Id|取得したBinariesテーブルのレコードのIDが格納されます。|
|StatusCode|完了時のステータスコードが格納されます。正常終了時は200です。|
|Message|完了時のメッセージが格納されます。|
|ReferenceId|ファイルが紐づいているレコードのIDが格納されます。|
|BinaryType|添付ファイルの場合Attachments、画像の場合Imagesが格納されます。|
|Base64|Base64にエンコードされたファイルの内容が格納されます。実際のファイルを取得するにはこの値をBase64デコードしてください。|
|Guid|ファイルのGUIDが格納されます。|
|FileName|ファイル名が格納されます。|
|Extension|拡張子が格納されます。|
|Size|ファイルサイズがバイト単位で格納されます。|
|ContentType|ファイルのMimeTypeが格納されます。|
|Creator|ファイル作成者のユーザIDが格納されます。|
|Updator|ファイル更新者のユーザIDが格納されます。|
|CreatedTime|ファイル作成日時が格納されます。|
|UpdatedTime|ファイル更新日時が格納されます。|

##### JSON  

```
{
    "Id": 123,
    "StatusCode": 200,
    "Message": "Test用ファイルを取得しました。",
    "Response": {
        "ReferenceId": 30,
        "BinaryType": "Attachments",
        "Base64": "dGVzdA==...",
        "Guid": "5E23245...",
        "FileName": "テスト用ファイル",
        "Extension": ".txt",
        "Size": 54,
        "ContentType": "text/plain",
        "Creator": 1,
        "Updator": 1,
        "CreatedTime": "2023/08/16 12:00:00",
        "UpdatedTime": "2023/08/17 12:00:00"
    }
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. 任意のテーブルに保存された添付ファイルをまとめて取得する</summary>

任意のテーブルのレコードに添付されたファイルをまとめて取得します。取得対象はViewで絞り、添付ファイルが存在したらIDごとのフォルダを作成し格納します。

##### Python(api_binaries_p1.py)

```
# Base64エンコード/デコードライブラリ
import base64

# 正規表現のためのライブラリ
import re

# ファイルパス操作のためのライブラリ
from pathlib import Path

# HTTPリクエスト用ライブラリ
import requests

# 設定
BASE_URI = "【URL】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】
API_VERSION = 1.1

# 取得対象とする添付ファイル項目
ATTACHMENT_ITEM = "AttachmentsA"
# 取得先ディレクトリ
OUT_DIR = Path(r"C:\work\download")

# ファイル名として使用できない文字を置換し、安全な名前に変換する
safe = lambda s: re.sub(r'[\\/:*?"<>|\x00-\x1F]', "_", str(s or "")).strip()

# 検索条件(Status が 100 のレコードに絞る)
VIEW = {
    "ColumnFilterHash": {
        "Status": '["100"]',
    }
}

post = lambda s, url, payload: (lambda r: (r.raise_for_status(), r.json())[1])(
    s.post(
        url, json=payload, headers={"Content-Type": "application/json; charset=utf-8"}
    )
)

# メイン処理
OUT_DIR.mkdir(parents=True, exist_ok=True)

# 結果集計用変数
record_count = 0  # 取得レコード数
records_with_attachments = 0  # 添付ありレコード数
seen_files = 0  # 添付ファイル総数
downloaded_files = 0  # 実際にDLした数

with requests.Session() as s:
    # レコード取得
    items = (
        post(
            s,
            f"{BASE_URI}/api/items/{SITE_ID}/get",
            {"ApiVersion": API_VERSION, "ApiKey": API_KEY, "View": VIEW},
        )
        .get("Response", {})
        .get("Data", [])
    )

    record_count = len(items)

    for rec in items:
        rec_id = rec.get("ResultId") or rec.get("IssueId")
        atts = (rec.get("AttachmentsHash") or {}).get(ATTACHMENT_ITEM) or []
        if not rec_id or not atts:
            continue  # 添付なし → フォルダ作らない

        records_with_attachments += 1
        rec_dir = OUT_DIR / str(rec_id)
        rec_dir.mkdir(parents=True, exist_ok=True)

        # 添付ファイル取得ループ
        for a in atts:
            guid, name = a.get("Guid"), a.get("Name")
            if not guid or not name:
                continue

            seen_files += 1
            b64 = (
                post(
                    s,
                    f"{BASE_URI}/api/binaries/{guid}/get",
                    {"ApiVersion": API_VERSION, "ApiKey": API_KEY},
                )
                .get("Response", {})
                .get("Base64")
            )

            if not b64:
                continue
            # ファイル保存
            (rec_dir / safe(name)).write_bytes(base64.b64decode(b64))
            downloaded_files += 1

# 処理結果出力
print("=== Download Result ===")
print(f"SiteId                : {SITE_ID}")
print(f"Attachment Item       : {ATTACHMENT_ITEM}")
print(f"Records (matched)     : {record_count}")
print(f"Records with files    : {records_with_attachments}")
print(f"Attachments found     : {seen_files}")
print(f"Attachments downloaded: {downloaded_files}")
print(f"Output directory      : {OUT_DIR}")

```

##### 実行

```
>python api_binaries_p1.py
```

##### 実行結果

```
=== Download Result ===
SiteId                : 6412
Attachment Item       : AttachmentsA
Records (matched)     : 1
Records with files    : 0
Attachments found     : 0
Attachments downloaded: 0
Output directory      : C:\work\download
```
</details>

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。