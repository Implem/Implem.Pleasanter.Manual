---
title: レコード一括作成・更新
category: API
order: '1400'
status: ''
parts: ''
urlstring: api-record-bulkupsert
translationKey: api-record-bulkupsert
shortname: ''
created: 2024-06-27
updated: 2026-09-09
---

## 概要

APIを使用して複数レコードを一括作成または一括更新します。

-   指定したキー項目に一致するレコードがある場合：該当レコードを更新
-   一致するレコードがない場合：新規作成(※1)
-   指定したキー項目の値がNULLの場合：レコードを新規作成
-   キー項目が無い場合：全てのレコードを新規作成

このAPIでは、処理が正常に終了した時に[通知](../../../users-guide/hands-on/advanced/advanced-operations-notification.md)できます。通知するには、通知タイミングの"インポート後"を有効にしておきます。

※1 KeyNotFoundCreateパラメータがfalseの場合は新規作成されません。

## 注意事項

1. レコード単位で処理をおこない途中がエラーが発生した場合は以降の処理は中止されます。

## 制限事項

1. 対象の[サイト](../../../users-guide/site/index.md)に「作成」および「更新」権限が必要です。
1. [Wiki](../../../users-guide/wiki/index.md)では使用できません。
1. パラメータ[General.json](../../../setup/parameters/general.json.md)の「BulkUpsertMax」で設定した値を超えたレコードがあった場合は処理を行いません。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト  

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/bulkupsert(※2)|
|Body|以下のjsonデータを参考のこと|

(※2){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/bulkupsert

##### JSON

```
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "Keys": [
        "ClassA"
    ],
    "KeyNotFoundCreate": true,
    "Data": [
        {
            "Title": "新機能XXを開発する1",
            "ClassHash": {
                "ClassA": "RC0001"
            }
        },        
        {
            "Title": "新機能XXを開発する2",
            "ClassHash": {
                "ClassA": "RC0002"
            }
        }
    ]
}
```

|カラム|設定内容|
|:--|:--|  
|Keys|キーとなる項目を指定。複数の項目を指定可能。（省略時：全てのレコードの新規作成）|
|KeyNotFoundCreate|キーと一致するレコードが無い場合に新規作成します。（省略時：true）|
|Data|レコードの配列|

#### 指定するキー項目について

指定したキー項目をもとにAPIによるレコード作成・更新(upsert)を行います。キー項目の指定は以下のパラメータで指定します。
キー項目の指定が無い場合は全てのレコードの新規作成を行います。
Keysに指定した項目の値がNULLの場合、キー項目としての比較はされず、レコードが新規作成されます。

詳細につきましては、下記の (a)キーが無い場合、(b)単一キーの場合、(c)複合キーの場合 を参照してください。

#### APIによる画像の挿入について

BodyにImageHashを指定することで[内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[コメント](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)、[説明](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)項目に画像を挿入することが可能です。
更新系のAPI（update／upsert）で本機能によるレコード更新を行う場合、既存レコードの該当項目は[内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)項目では上書き、[コメント](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)項目では追加となります。また、更新系のAPIで[内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)項目に登録する文字列を指定するBodyやDescriptionHashを省略した状態でImageHashのみを指定すると、上書きではなく追加となります。

##### How to Specify ImageHash

<table>
<thead>
  <tr>
    <th>1st Level</th>
    <th>2nd Level</th>
    <th>3rd Level</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="9">ImageHash</td>
    <td rowspan="6">Body</td>
    <td>HeadNewLine</td>
    <td>Specify whether to insert a newline at the beginning of the image with true/false. If omitted, there will be no newline.</td>
    <td>true</td>
  </tr>
  <tr>
    <td>EndNewLine</td>
    <td>Specifies whether to insert a newline at the end of the image with true/false. If omitted, there will be no newline.</td>
    <td>true</td>
  </tr>
  <tr>
    <td>Position</td>
    <td>Specifies the position of the image to insert when setting a string in the target item in the same request. If -1 is specified or omitted, it will be inserted at the end.</td>
    <td>3</td>
  </tr>
  <tr>
    <td>Alt</td>
    <td>Specifies the string to insert into the alt attribute (text displayed instead of the image when the image cannot be displayed in the web browser). If omitted, "image" will be set.</td>
    <td>hayato</td>
  </tr>
  <tr>
    <td>Extension</td>
    <td>Specifies the file extension to register in the Binaries table. If omitted, ".png" will be set.</td>
    <td>.jpeg</td>
  </tr>
  <tr>
    <td>Base64</td>
    <td>Specify the Base64 encoded binary data of the image as a string. If you specify ImageHash, this cannot be omitted.</td>
    <td>iVBORw0KG…（the following omitted）</td>
  </tr>
  <tr>
    <td>Comments</td>
    <td>（same as above）</td>
    <td>（same as above）</td>
    <td>-</td>
  </tr>
  <tr>
    <td>DescriptionA</td>
    <td>（same as above）</td>
    <td>（same as above）</td>
    <td>-</td>
  </tr>
  <tr>
    <td>DescriptionB</td>
    <td>（same as above）</td>
    <td>（same as above）</td>
    <td>-</td>
  </tr>
</tbody>
</table>

#### APIによるプロセスの実行について

リクエストデータに、プロセスIDを指定し、プロセスを実行することが可能です。

##### Preconfiguration

Please set up the "[Process](../../../FAQ/sample-codes/faq-process-workflow.md)" in advance.

##### Limitations

When executing a process via the API, input validation set for the process

##### Process Specifying Method

Either ProccessId or ProccessIds should be set. If both are set, ProccessIds is applied.
Note that when ProccessIds is set, the specified multiple process IDs will be executed in the order in which they appear in the list of "[Process](../../../FAQ/sample-codes/faq-process-workflow.md)" set in advance.

|Setting Item|Description|Example|
|:--|:--|:--|
|ProccessId|Specify the ID of the process.|1|
|ProccessIds|Specify IDs for multiple processes.|[1,2,3]|

#### (a)キーが無い場合

Keys パラメータが無い場合には、全てのレコードを新規作成します。
KeyNotFoundCreate パラメータの値は無視されます。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "145Afa9AF2A10SafaA21641...",
    "Data": [
        {
            "Title": "新機能XXを開発する1",
            "Body": "ボディ1",
            "CompletionTime": "2018/3/31",
            "ProcessId": 1,
            "ClassHash": {
                "ClassA": "RC0001",
                "ClassB": "分類２"
            },
            "NumHash": {
                "NumA": 100
            },
            "DateHash": {
                "DateA": "2019/01/01"
            },
            "DescriptionHash": {
                "DescriptionA": "説明1"
            },
            "CheckHash": {
                "CheckA": false
            },
            "ImageHash": {
                "Body": {
                    "HeadNewLine": true,
                    "EndNewLine": true,
                    "Position": 3,
                    "Alt": "imageBody",
                    "Extension": ".jpeg",
                    "Base64": "iVBORw0KG..."
                },
                "DescriptionA": {
                    "HeadNewLine": true,
                    "EndNewLine": true,
                    "Position": 3,
                    "Alt": "imageDescriptionA",
                    "Extension": ".jpeg",
                    "Base64": "iVBORw0KG..."
                }
            }
        },
        {
            "Title": "新機能XXを開発する2",
            "Body": "ボディ2",
            "CompletionTime": "2018/3/31",
            "ProcessId": 1,
            "ClassHash": {
                "ClassA": "RC0002",
                "ClassB": "分類３"
            },
            "NumHash": {
                "NumA": 100
            },
            "DateHash": {
                "DateA": "2019/01/01"
            },
            "DescriptionHash": {
                "DescriptionA": "説明2"
            },
            "CheckHash": {
                "CheckA": false
            }
        }
    ]
}
```

#### (b)単一キーの場合

Keys パラメータにキーとなる項目の項目名を配列形式で設定します。Keys に指定した項目について、パラメータで指定した値と一致するレコードを検索します。    

下記の例では、１つ目のレコード「ClassA」項目の値が "RC0001" のレコードを検索します。  ２つ目のレコード「ClassA」項目の値が "RC0002"のレコードを検索します。  
レコードを検索した結果に応じて下記の処理が実行されます。

1. 対象のレコードが存在しなかった場合: レコードが新規作成されます。ただしKeyNotFoundCreateパラメータがfalseの場合は新規作成されません。
1. 対象のレコードが１件存在した場合: そのレコードが更新されます。
1. 対象のレコードが複数件存在した場合: レコードの作成・更新は行われず、エラーレスポンスが返却されます。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "145Afa9AF2A10SafaA21641...",
    "Keys": [
        "ClassA"
    ],
    "KeyNotFoundCreate": true,
    "Data": [
        {
            "Title": "新機能XXを開発する1",
            "Body": "ボディ1",
            "CompletionTime": "2018/3/31",
            "ProcessId": 1,
            "ClassHash": {
                "ClassA": "RC0001",
                "ClassB": "分類２"
            },
            "NumHash": {
                "NumA": 100
            },
            "DateHash": {
                "DateA": "2019/01/01"
            },
            "DescriptionHash": {
                "DescriptionA": "説明1"
            },
            "CheckHash": {
                "CheckA": false
            },
            "ImageHash": {
                "Body": {
                    "HeadNewLine": true,
                    "EndNewLine": true,
                    "Position": 3,
                    "Alt": "imageBody",
                    "Extension": ".jpeg",
                    "Base64": "iVBORw0KG..."
                },
                "DescriptionA": {
                    "HeadNewLine": true,
                    "EndNewLine": true,
                    "Position": 3,
                    "Alt": "imageDescriptionA",
                    "Extension": ".jpeg",
                    "Base64": "iVBORw0KG..."
                }
            }
        },
        {
            "Title": "新機能XXを開発する2",
            "Body": "ボディ2",
            "CompletionTime": "2018/3/31",
            "ProcessId": 1,
            "ClassHash": {
                "ClassA": "RC0002",
                "ClassB": "分類３"
            },
            "NumHash": {
                "NumA": 100
            },
            "DateHash": {
                "DateA": "2019/01/01"
            },
            "DescriptionHash": {
                "DescriptionA": "説明2"
            },
            "CheckHash": {
                "CheckA": false
            }
        }
    ]
}
```

#### (c)複合キーの場合 

Keys パラメータに複数の項目名を設定した場合、Keys に指定したすべての項目について、パラメータで指定した値と一致するレコードを検索します。    
下記の例では、１つ目のレコード「ClassA」項目の値が "RC0001" かつ、「ClassB」項目の値が "001" のレコードを検索します。  ２つ目のレコード「ClassA」項目の値が "RC0001" かつ、「ClassB」項目の値が "002" のレコードを検索します。  

1. 対象のレコードが存在しなかった場合: レコードが新規作成されます。ただしKeyNotFoundCreateパラメータがfalseの場合は新規作成されません。
1. 対象のレコードが１件存在した場合: そのレコードが更新されます。
1. 対象のレコードが複数件存在した場合: レコードの作成・更新は行われず、エラーレスポンスが返却されます。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "145Afa9AF2A10SafaA21641...",
    "Keys": [
        "ClassA",
        "ClassB"
    ],
    "KeyNotFoundCreate": true,
    "Data": [
        {
            "Title": "新機能XXを開発する1",
            "Body": "ボディ1",
            "CompletionTime": "2018/3/31",
            "ProcessId": 1,
            "ClassHash": {
                "ClassA": "RC0001",
                "ClassB": "001"
            },
            "NumHash": {
                "NumA": 100
            },
            "DateHash": {
                "DateA": "2019/01/01"
            },
            "DescriptionHash": {
                "DescriptionA": "説明1"
            },
            "CheckHash": {
                "CheckA": false
            },
            "ImageHash": {
                "Body": {
                    "HeadNewLine": true,
                    "EndNewLine": true,
                    "Position": 3,
                    "Alt": "imageBody",
                    "Extension": ".jpeg",
                    "Base64": "iVBORw0KG..."
                },
                "DescriptionA": {
                    "HeadNewLine": true,
                    "EndNewLine": true,
                    "Position": 3,
                    "Alt": "imageDescriptionA",
                    "Extension": ".jpeg",
                    "Base64": "iVBORw0KG..."
                }
            }
        },
        {
            "Title": "新機能XXを開発する2",
            "Body": "ボディ2",
            "CompletionTime": "2018/3/31",
            "ProcessId": 1,
            "ClassHash": {
                "ClassA": "RC0001",
                "ClassB": "002"
            },
            "NumHash": {
                "NumA": 100
            },
            "DateHash": {
                "DateA": "2019/01/01"
            },
            "DescriptionHash": {
                "DescriptionA": "説明2"
            },
            "CheckHash": {
                "CheckA": false
            }
        }
    ]
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

### レコードが新規作成された場合

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9994,
    "Message": "記録テーブル: 1 件追加し、0 件更新しました。"
}
```

### レコードが更新された場合

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9994,
    "Message": "記録テーブル: 0 件追加し、1 件更新しました。"
}
```

### サイト単位でエラーとなった場合

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 401,
    "Message": "認証できませんでした。"
}
```

### レコード単位でエラーとなった場合

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 500,
    "Message": "記録テーブル:エラーが発生しました。0 件追加し、0 件更新。\nIndex:1(ClassA=RC00011)\nエラー内容:条件に一致するレコードが複数存在します。"
}
```

### パラメータ[General.json](../../../setup/parameters/general.json.md)の「BulkUpsertMax」で設定した値を超えたレコードがあった場合

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 500,
    "Message": "1000 行を超えるデータは一度にインポートできません。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. ファイル名からUpsertキーを取得、キーに合致するレコードにファイルを添付する</summary>

任意のフォルダに格納されたファイルを読み取り、ファイル名よりUpsertのキー情報を取得しbulkUpsertを実行、当該ファイルを添付します。

本サンプルでは、以下のようなファイル名基準とし、”KC”+数字をキー項目として判定します。
KC001_XXXXX.txt  
 →"KC001"がUpsertキー

##### 実行前

このようなファイルを用意
![Upsertキーを含むファイル名のファイルを用意したフォルダ](https://pleasanter.org/files/images/ja/developers-guide/api/table-operations/assets/7b2f960dda714d75a0219f1e33567333.png)

登録対象のテーブルの状態、KC001、KC002のレコードが存在
![実行前のテーブル。KC001とKC002のレコードがある](https://pleasanter.org/files/images/ja/developers-guide/api/table-operations/assets/75e711e4383b4557a04d276bbc9e18ca.png)

##### 実行後

ファイル名にしたがい、ファイル添付・レコード作成
 ![実行後のテーブル。ファイルが添付され、レコードが作成されている](https://pleasanter.org/files/images/ja/developers-guide/api/table-operations/assets/112603d6edbb45cf95c03e4fbad360cd.png)

##### Python(api_record_bulkupsert_p1.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# 画像をBase64化するためのライブラリ
import base64

# JSON操作のためのライブラリ
import json

# ファイル操作や正規表現のためのライブラリ
import mimetypes

# その他標準ライブラリ
import re

# データ構造操作のためのライブラリ
from collections import defaultdict

# ファイルパス操作のためのライブラリ
from pathlib import Path

# 接続先URL
BASE_URL = "【URL】"
# サイトID
SITE_ID = 【サイトID】
# APIキー
API_KEY = "【APIキー】"
# 対象フォルダ
TARGET_FOLDER = r"【パス】"

# キーコード抽出用正規表現
KEY_REGEX = re.compile(r"^KC\d+$")

# bulkupsert のキー項目
KEYS = ["ClassA"]

# KeyNotFoundCreate=true なら、キー未存在は新規作成
KEY_NOT_FOUND_CREATE = True

# 1回で投げる Data 件数（BulkUpsertMax を超えない範囲で）
BULK_UPSERT_MAX = 10000

def extract_keycode(filename: str) -> str | None:
    # KC001_FILENAME.txt -> KC001 / ルール外は None
    if "_" not in filename:
        return None
    head = filename.split("_", 1)[0].strip()
    if not head or not KEY_REGEX.match(head):
        return None
    return head

def file_to_attachment_obj(path: Path) -> dict:
    # Pleasanter AttachmentsA の要素を作る
    ctype, _ = mimetypes.guess_type(path.name)
    if not ctype:
        ctype = "application/octet-stream"
    b64 = base64.b64encode(path.read_bytes()).decode("ascii")
    return {
        "ContentType": ctype,
        "Name": path.name,
        "Base64": b64,
    }

def chunked(lst, n):
    for i in range(0, len(lst), n):
        yield lst[i : i + n]

def bulkupsert(session: requests.Session, data_rows: list[dict]) -> dict:
    url = f"{BASE_URL}/api/items/{SITE_ID}/bulkupsert"
    payload = {
        "ApiVersion": "1.1",
        "ApiKey": API_KEY,
        "Keys": KEYS,
        "KeyNotFoundCreate": KEY_NOT_FOUND_CREATE,
        "Data": data_rows,
    }
    r = session.post(url, data=json.dumps(payload))
    if not r.ok:
        raise RuntimeError(f"HTTP {r.status_code}\n{r.text}")
    return r.json()

def main():
    folder = Path(TARGET_FOLDER)
    if not folder.is_dir():
        raise SystemExit(f"フォルダが見つかりません: {folder}")

    # キーコードごとにファイルをまとめる（同じKCに複数ファイルがある想定）
    grouped: dict[str, list[Path]] = defaultdict(list)

    for p in folder.iterdir():
        if not p.is_file():
            continue
        keycode = extract_keycode(p.name)
        if not keycode:
            # ルール不一致は処理対象外
            continue
        grouped[keycode].append(p)

    if not grouped:
        print("処理対象ファイルなし（命名規則に一致するファイルがありません）")
        return

    # bulkupsert の Data を組み立て（キーごとに 1レコード）
    # ※キー項目ClassAに keycode を入れる想定
    rows: list[dict] = []
    for keycode, paths in grouped.items():
        attachments = [file_to_attachment_obj(p) for p in paths]
        rows.append(
            {
                "Title": f"{keycode} 添付登録",
                "ClassHash": {
                    "ClassA": keycode,
                },
                # 添付Aに登録
                "AttachmentsHash": {"AttachmentsA": attachments},
            }
        )

    session = requests.Session()
    session.headers.update({"Content-Type": "application/json"})

    # BulkUpsertMax を超えないように分割送信
    for part in chunked(rows, BULK_UPSERT_MAX):
        res = bulkupsert(session, part)
        print(res)

    print(
        f"完了: 対象キー={len(grouped)}件 / 対象ファイル={sum(len(v) for v in grouped.values())}件"
    )

if __name__ == "__main__":
    main()

```

##### 実行

```
>python api_record_bulkupsert_p1.py
```

##### 実行結果

```
{'Id': 9999, 'StatusCode': 200, 'Message': '添付ファイル一括登録: 2 件追加し、1 件更新しました。'}
完了: 対象キー=3件 / 対象ファイル=4件
```
</details>

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.6.0以降|機能追加|

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)
