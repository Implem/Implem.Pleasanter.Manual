---
title: レコード作成
category: API
order: '1300'
status: ''
parts: ''
urlstring: api-record-create
translationKey: api-record-create
shortname: レコード作成API
created: 2019-05-02
updated: 2026-07-14
---

## 概要

APIを使用して新規にレコードを作成することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{サイトID}/create (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/create

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

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "XXXXXXXXXX...",
    "Title": "新機能XXを開発する",
    "Body": "ボディ",
    "CompletionTime": "2018/3/31",
    "ProcessId": 1,
    "ClassHash": {
        "ClassA": "分類",
        "ClassB": "未分類",
        "ClassC": "その他"
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
        "DescriptionA": "説明",
        "DescriptionB": "概要",
        "DescriptionC": "補足"
    },
    "CheckHash": {
        "CheckA": true,
        "CheckB": false
    },
    "AttachmentsHash": {
        "AttachmentsA": [
            {
                "ContentType": "text/plain",
                "Name": "Readme.txt",
                "Base64": "5yY5Trfi4..."
            }
        ]
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

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9996,
    "Message": "\" 新機能XXを開発する \" を作成しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。  

<details markdown="1">
<summary>1. 添付ファイル・画像を含まないレコードを作成する</summary>

添付ファイル・画像を含まないレコードを作成します。

##### Python(api_record_create_p1.py)

```
import requests

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】

url = f"{BASE_URL}/api/items/{SITE_ID}/create"

# 単純レコード作成
payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "Title": "サンプル案件F",
    "Status": 200,
    "ClassHash": {"ClassA": "障害"},
    "DateHash": {"DateA": "2025/1/20", "DateB": "2025/1/25"},
    "NumHash": {"NumA": 20, "NumB": 3},
}

res = requests.post(url, json=payload, headers={"Content-Type": "application/json"})

print(res.status_code, res.text)
```

##### 実行

```
>python api_record_create_p1.py
```

##### 実行結果

```
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件F \" を作成しました。"}
```

</details>

<details markdown="1">
<summary>2. 添付ファイルを含むレコードを作成する</summary>

添付ファイルを含むレコードを作成します。

##### Python(api_record_create_p2.py)

```
import requests
import base64

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】
FILE_NAME = "【添付ファイル名】"
CONTENT_TYPE = "【ファイル形式】" 

# 添付ファイルをBase64化
b64 = base64.b64encode(open(FILE_NAME, "rb").read()).decode()

url = f"{BASE_URL}/api/items/{SITE_ID}/create"

# 添付ファイルを含むレコード作成
payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "Title": "添付付きレコード",
    "DescriptionHash": {
        "DescriptionA": "添付ファイルを登録するサンプルです",
    },
    "AttachmentsHash": {
        "AttachmentsA": [
            {
                "ContentType": CONTENT_TYPE,
                "Name": FILE_NAME,
                "Base64": b64,
            }
        ]
    },
}

res = requests.post(url, json=payload, headers={"Content-Type": "application/json"})
print(res.status_code, res.text)
```

##### 実行

```
>python api_record_create_p2.py
```

##### 実行結果

```
200 {"Id":9999,"StatusCode":200,"Message":"\" 添付付きレコード \" を作成しました。"}
```

</details>

<details markdown="1">
<summary>3. 画像を含むレコードを作成する</summary>

画像を含むレコードを作成します。

##### Python(api_record_create_p3.py)

```
import requests
import base64

# サーバ名、APIキー、サイトID
BASE_URL = "【サーバ名】"
API_KEY = "【APIキー】"
SITE_ID = 【サイトID】
FILE_NAME = "【画像ファイル名】"
EXTENSION = "【画像ファイル拡張子】"

# 画像ファイルをBase64化
b64 = base64.b64encode(open(FILE_NAME, "rb").read()).decode()

url = f"{BASE_URL}/api/items/{SITE_ID}/create"

# 画像を含むレコード作成
payload = {
    "ApiVersion": 1.1,
    "ApiKey": API_KEY,
    "Title": "画像付きレコード",
    "DescriptionHash": {
        "DescriptionA": "画像を登録するサンプルです",
    },
    "ImageHash": {
        "DescriptionA": {
            "HeadNewLine": "true",
            "EndNewLine": "true",
            "Alt": "imageDescriptionA",
            "Extension": EXTENSION,
            "Base64": b64,
        }
    },
}

res = requests.post(url, json=payload, headers={"Content-Type": "application/json"})
print(res.status_code, res.text)
```

##### 実行

```
>python api_record_create_p3.py
```

##### 実行結果

```
200 {"Id":9999,"StatusCode":200,"Message":"\" 画像付きレコード \" を作成しました。"}
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