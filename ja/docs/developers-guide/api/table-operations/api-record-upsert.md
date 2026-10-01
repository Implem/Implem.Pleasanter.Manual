---
title: レコード作成・更新
category: API
order: '1400'
status: ''
parts: ''
urlstring: api-record-upsert
translationKey: api-record-upsert
shortname: upsert
created: 2022-06-22
updated: 2026-07-14
---

## 概要

APIを使用して、レコードを作成・更新します。

-   指定したキー項目が一致するレコードがある場合：該当レコードを更新
-   指定したキー項目の値がNULLの場合：レコードを新規作成
-   一致するレコードがない場合：レコードを新規作成

## 制限事項

1.  対象の「レコード」に「作成」および「更新」権限が必要です。
1.  [Wiki](../../../users-guide/wiki/index.md)では使用できません。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト  

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type|application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/upsert(※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/upsert

### 指定するキー項目について

指定したキー項目をもとにAPIによるレコード作成・更新(upsert)を行います。キー項目の指定は以下のパラメータで指定します。

|プロパティ名|データ型|説明|
|:--|:--|:--|
|Keys|配列(文字列)|キーとなる項目を指定。複数の項目を指定可能。|

Keysに指定した項目の値がNULLの場合、キー項目としての比較はされず、レコードが新規作成されます。

詳細につきましては、下記の (a)単一キーの場合、(b)複合キーの場合 を参照してください。

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

### (a)単一キーの場合

Keys パラメータにキーとなる項目の項目名を配列形式で設定します。Keys に指定した項目について、パラメータで指定した値と一致するレコードを検索します。

下記の例では、「ClassA」項目の値が "RC0001" のレコードを検索します。
レコードを検索した結果に応じて下記の処理が実行されます。

1.  対象のレコードが存在しなかった場合: レコードが新規作成されます。
1.  対象のレコードが１件存在した場合: そのレコードが更新されます。
1.  対象のレコードが複数件存在した場合: レコードの作成・更新は行われず、エラーレスポンスが返却されます。

#### JSON

```json
{
    "ApiVersion": 1.1,
    "ApiKey": "145Afa9AF2A10SafaA21641...",
    "Keys": [
        "ClassA"
    ],
    "Title": "新機能XXを開発する2",
    "Body": "ボディ2",
    "CompletionTime": "2018/3/31",
    "ProcessId": 1,
    "ClassHash": {
        "ClassA": "RC0001",
        "ClassB": "分類２",
        "ClassC": "その他2"
    },
    "NumHash": {
        "NumA": 100,
        "NumB": 200
    },
    "DateHash": {
        "DateA": "2019/01/01",
        "DateB": "2020/01/01"
    },
    "DescriptionHash": {
        "DescriptionA": "説明2",
        "DescriptionB": "概要2",
        "DescriptionC": "補足2"
    },
    "CheckHash": {
        "CheckA": false,
        "CheckB": true
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
}
```

### (b)複合キーの場合

Keys パラメータに複数の項目名を設定した場合、Keys に指定したすべての項目について、パラメータで指定した値と一致するレコードを検索します。
下記の例では、「ClassA」項目の値が "RC0002" かつ、「ClassB」項目の値が "01" のレコードを検索します。  

#### JSON

```json
{
    "ApiVersion": 1.1,
    "ApiKey": "ad7816s5sD2safFafaD...",
    "Keys": [
        "ClassA",
        "ClassB"
    ],
    "Title": "新機能XXを開発する2",
    "Body": "ボディ2",
    "CompletionTime": "2018/3/31",
    "ClassHash": {
        "ClassA": "RC0002",
        "ClassB": "01",
        "ClassC": "その他2"
    },
    "NumHash": {
        "NumA": 100,
        "NumB": 200
    },
    "DateHash": {
        "DateA": "2019/01/01",
        "DateB": "2020/01/01"
    },
    "DescriptionHash": {
        "DescriptionA": "説明2",
        "DescriptionB": "概要2",
        "DescriptionC": "補足2"
    },
    "CheckHash": {
        "CheckA": false,
        "CheckB": true
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
}
```

## レスポンス

下記の形式のjsonデータが返却されます。  

### レコードが新規作成された場合

```json
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9994,
    "Message": "\" 新機能XXを開発する2 \" を作成しました。"
}
```

### レコードが更新された場合

```json
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9994,
    "Message": "\" 新機能XXを開発する2 \" を更新しました。"
}
```

### 作成または更新できなかった場合

```json
{
    "Id": 12345,
    "StatusCode": 401,
    "Message": "認証できませんでした。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください

<details markdown="1">
<summary>1. ファイル名からUpsertキーを取得しUpsertを実行する</summary>

任意のフォルダに格納されたファイルを読み取り、ファイル名よりUpsertのキー情報を取得しUpsertを実行します。

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

##### Python(api_record_upsert_p1.py)

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
KEY_REGEX = re.compile(r"^(KC\d+)$")

# Upsert のキー項目
UPSERT_KEYS = ["ClassA"]

def extract_keycode(filename: str) -> str | None:
    # KC001_FILENAME.txt -> KC001 / ルール外は None
    if "_" not in filename:
        return None
    head = filename.split("_", 1)[0].strip()
    if not head:
        return None
    m = KEY_REGEX.match(head)
    return m.group(1) if m else None

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

def upsert_attachments(
    session: requests.Session, keycode: str, attachments: list[dict]
) -> dict:
    url = f"{BASE_URL}/api/items/{SITE_ID}/upsert"
    payload = {
        "ApiVersion": 1.1,
        "ApiKey": API_KEY,
        "Keys": UPSERT_KEYS,
        "ClassHash": {
            "ClassA": keycode,
        },
        "AttachmentsHash": {"AttachmentsA": attachments},
    }

    r = session.post(url, data=json.dumps(payload))
    if not r.ok:
        raise RuntimeError(f"Upsert失敗 key={keycode} HTTP {r.status_code}\n{r.text}")
    return r.json()

def main():
    folder = Path(TARGET_FOLDER)
    if not folder.is_dir():
        raise SystemExit(f"フォルダが見つかりません: {folder}")

    # キーコードごとに添付をまとめる（同一KCに複数ファイルがある場合もまとめて登録）
    grouped: dict[str, list[Path]] = defaultdict(list)

    for p in folder.iterdir():
        if not p.is_file():
            continue

        keycode = extract_keycode(p.name)
        if not keycode:
            # ルール外は処理対象外
            continue

        grouped[keycode].append(p)

    if not grouped:
        print("処理対象ファイルなし（命名規則に一致するファイルがありません）")
        return

    session = requests.Session()
    session.headers.update({"Content-Type": "application/json"})

    for keycode, paths in grouped.items():
        attachments = [file_to_attachment_obj(p) for p in paths]
        try:
            res = upsert_attachments(session, keycode, attachments)
            # Upsertのレスポンスを表示
            print(f"OK: key={keycode} 添付={len(attachments)}件 / response={res}")
        except Exception as e:
            print(f"NG: key={keycode} 添付={len(paths)}件")
            print(e)

if __name__ == "__main__":
    main()

```

##### 実行

```
>python api_record_upsert_p1.py
```

##### 実行結果

```
OK: key=KC001 添付=2件 / response={'Id': 9999, 'StatusCode': 200, 'Message': '" KC001 " を更新しました。'}
OK: key=KC002 添付=1件 / response={'Id': 9999, 'StatusCode': 200, 'Message': '" KC002 " を更新しました。'}
OK: key=KC003 添付=1件 / response={'Id': 9999, 'StatusCode': 200, 'Message': '" KC003 " を更新しました。'}
・・・・
```

</details>

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2019年10月よりAPIの仕様が一部変更となりました。**

-   分類, 数値, 日付, 説明, チェック項目はjsonにそのまま記載する方法から「～Hash」の中に記載する方法へ変更されました。

**※ 2018年11月よりAPIの仕様が一部変更となりました。**

-   URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
-   Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。
