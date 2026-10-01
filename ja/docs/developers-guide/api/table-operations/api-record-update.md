---
title: レコード更新
category: API
order: '1400'
status: ''
parts: ''
urlstring: api-record-update
translationKey: api-record-update
shortname: ''
created: 2019-05-02
updated: 2026-07-14
---

## 概要

APIを使用してレコードを更新することができます。レコードの内容の変更に加え、[添付ファイル](../../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)の追加、削除や[レコードのアクセス制御](../../../users-guide/access-control/table-record-access-control.md)の変更が可能です。

## 制限事項

1. 対象の「レコード」に「更新」権限が必要です。
1. [Wiki](../../../users-guide/wiki/index.md)でImageHashを使用した画像の挿入機能は、プリザンター 1.4.19.0以降が必要です。
1. [レコードのアクセス制御](../../../users-guide/access-control/table-record-access-control.md)を変更するには「権限の管理」権限が必要です。
1. レコードのアクセス制御の更新機能は、プリザンター 1.1.36.0 以降、プリザンター .NET Framework版 0.50.260 以降のバージョンが必要です。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト  

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバー名}/api/items/{レコードID}/update(※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバー名}、{レコードID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{レコードID}/update

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

### (a)通常の更新  

ClassやNum等の項目を設定する際は以下のように"{項目名}Hash"と記載してください。 

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "ad7816s5sD2safFafaD...",
    "Title": "新機能XXを開発する2",
    "Body": "ボディ2",
    "CompletionTime": "2018/3/31",
    "ProcessId": 1,
    "ClassHash": {
        "ClassA": "分類2",
        "ClassB": "未分類2",
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
    "AttachmentsHash": {
        "AttachmentsA": [
            {
                "ContentType": "text/plain",
                "Name": "Readme.txt",
                "Base64": "4O5O4jjfui..."
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
            "Base64": "iVBORw0KG…"
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

(日付項目をNULLにするには[FAQ：APIで日付項目をNULLに設定したい](../../../FAQ/features-for-developers/faq-api-set-date-to-null.md)を参照)

### (b)添付ファイル削除  

AttachmentsA内のGuidにはファイルのGUIDを指定してください。  
**添付ファイルを削除する場合、GUIDの指定は必ず大文字で記載してください。**  
また、AttachmentsA内のDeletedには1を指定してください。 

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "2bcb8a909da1d8827c99c...",
    "AttachmentsHash": {
        "AttachmentsA": [
            {
                "Guid": "7AB84732...",
                "Deleted": 1
            }
        ]
    }
}
```

### 添付ファイルのGuidの取得方法

添付ファイルのあるレコードを以下のリンク先に従って取得します。  
[API機能：単一レコード取得](api-record-get.md)  
取得したjsonファイルの"Attachments"項目に添付ファイルのGuidが記載されているのでその値を使用してください。

### (c)レコードのアクセス制御の設定

レコードのアクセス制御を変更するにはRecordPermissionsを指定します。「権限の管理」権限を持ったApiKeyを指定する必要があります。下記の例では、組織ID:1に書き込み権限、グループID:1に管理権限、ユーザID:10に読み取り権限を付与しています。レコードのアクセス制御を指定すると、既存の設定を削除し、指定したものに置き換えます。追加や一部を削除することはできません。

##### JSON

```
{
    "ApiVersion": 1.1,
    "ApiKey": "2bcb8a909da1d8827c99c...",
    "RecordPermissions": [
        "Dept,1,31",
        "Group,1,511",
        "User,10,1"
    ]
}
```

### 権限の種類

権限の種類は下記のとおりです。与える権限の値の合計値を計算し設定してください。例えば読み取りと作成と更新を与えるには、1+2+4で7とします。すべての権限を与えるには511とします。

|No|権限|値|
|:----|:----|:----|
|1|読み取り|1|
|2|作成|2|
|3|更新|4|
|4|削除|8|
|5|メール送信|16|
|6|エクスポート|32|
|7|インポート|64|
|8|サイトの管理|128|
|9|権限の管理|256|

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
    "Id": 12345,
    "StatusCode": 200,
    "LimitPerDate": 10000,
    "LimitRemaining": 9994,
    "Message": "\" 新機能XXを開発する2 \" を更新しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。  

<details markdown="1">
<summary>1. レコードIDを直接指定し更新</summary>

レコードIDを直接指定し更新します。

##### Python(api_record_update_p1.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# 対象URLとAPIキーの設定
BASE_URL = "【対象URL】"
API_KEY = "【APIキー】"

# 更新対象のレコードID
RECORD_ID = 【レコードID】

# リクエスト生成
payload = {
    "ApiKey": API_KEY,
    "Title": "タイトル変更",
    "ClassHash": {
        "ClassA": "障害",
    },
}

# API 呼び出し
url = f"{BASE_URL}/api/items/{RECORD_ID}/update"
response = requests.post(
    url,
    headers={"Content-Type": "application/json"},
    data=json.dumps(payload),
)

# 結果判定
if response.ok:
    print("更新成功")
else:
    print("更新失敗")

print(response.status_code, response.text)
```

##### 実行

```
>python api_record_update_p1.py
```

##### 実行結果

```
更新成功
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件C \" を更新しました。"}
```

</details>

<details markdown="1">
<summary>2. 複数のレコードを更新</summary>

条件に該当するレコードを取得し、該当するレコード複数件を更新します。

##### Python(api_record_update_p2.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# 対象URLとAPIキーの設定
BASE_URL = "【対象URL】"
API_KEY = "【APIキー】"

# 更新対象のサイトID
SITE_ID = 【サイトID】

# 1. Status=100 のレコードを取得
# 取得パラメータ、Status=100 のフィルタを指定
get_payload = {
    "ApiKey": API_KEY,
    "View": {"ColumnFilterHash": {"Status": '["100"]'}},
}
# API 呼び出し
get_url = f"{BASE_URL}/api/items/{SITE_ID}/get"
response = requests.post(
    get_url,
    headers={"Content-Type": "application/json"},
    data=json.dumps(get_payload),
)

# 結果判定
if not response.ok:
    print("API 呼び出し失敗")
    print(response.status_code, response.text)
    exit()

# 取得したレコード一覧（配列）
results = response.json()
if len(results["Response"]["Data"]) <= 0:
    print("対象レコード0件")
    exit()

# 2. 取得したレコードを順に更新
for item in results["Response"]["Data"]:
    # 更新対象レコードID取得
    record_id = item.get("ResultId")
    # 更新リクエスト生成
    update_payload = {
        "ApiKey": API_KEY,
        "Id": record_id,
        "Status": "910",  # 保留
    }
    # API 呼び出し
    update_url = f"{BASE_URL}/api/items/{record_id}/update"
    update_response = requests.post(
        update_url,
        headers={"Content-Type": "application/json"},
        data=json.dumps(update_payload),
    )

    # 結果判定
    if update_response.ok:
        print(f"更新成功：Id={record_id}")
    else:
        print(f"更新失敗：Id={record_id}")

    print(update_response.status_code, update_response.text)
```

##### 実行

```
>python api_record_update_p2.py
```

##### 実行結果

```
更新成功：Id=9999
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件B \" を更新しました。"}
更新成功：Id=9999
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件C \" を更新しました。"}
```

</details>

<details markdown="1">
<summary>3. 添付ファイルを削除</summary>

特定のレコードに添付されている添付ファイルをすべて削除します。

##### Python(api_record_update_p3.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# 対象URLとAPIキーの設定
BASE_URL = "【対象URL】"
API_KEY = "【APIキー】"

# 更新対象のレコードID
RECORD_ID = 【レコードID】

# 1. レコード取得
get_payload = {"ApiKey": API_KEY}
# API 呼び出し
get_url = f"{BASE_URL}/api/items/{RECORD_ID}/get"
response = requests.post(
    get_url, headers={"Content-Type": "application/json"}, data=json.dumps(get_payload)
)

# 結果判定
if not response.ok:
    print(f"レコード取得失敗: Id={RECORD_ID}")
    print(response.status_code, response.text)
    exit()
# 取得したレコード一覧（配列）
results = response.json()

# 2. AttachmentsA 取得
attachments = (
    results["Response"]["Data"][0]["AttachmentsHash"].get("AttachmentsA") or []
)

# JSON文字列をオブジェクトに変換
attachments = json.loads(json.dumps(attachments))

# 添付ファイルがない場合は処理終了
if len(attachments) == 0:
    print(f"添付ファイルなしのため更新不要: Id={RECORD_ID}")
    exit()

# 3. 添付 Guid すべてを Deleted=1 にして更新
# 更新リクエスト生成
update_payload = {
    "ApiKey": API_KEY,
    "Id": RECORD_ID,
    "AttachmentsHash": {
        "AttachmentsA": [{"Guid": att["Guid"], "Deleted": 1} for att in attachments]
    },
}

# API 呼び出し
update_url = f"{BASE_URL}/api/items/{RECORD_ID}/update"
update_response = requests.post(
    update_url,
    headers={"Content-Type": "application/json"},
    data=json.dumps(update_payload),
)

# 結果判定
if update_response.ok:
    print(f"更新成功: Id={RECORD_ID}, 削除対象={len(attachments)}件")
else:
    print(f"更新失敗: Id={RECORD_ID}")

print(update_response.status_code, update_response.text)

```

##### 実行

```
>python api_record_update_p3.py
```

##### 実行結果

```
更新成功: Id=9999, 削除対象=3件
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件C \" を更新しました。"}
```

</details>

<details markdown="1">
<summary>4. レコードのアクセス制御を設定</summary>

特定のレコードにレコードのアクセス制御を設定します。

##### Python(api_record_update_p4.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# 対象URLとAPIキーの設定
BASE_URL = "【対象URL】"
API_KEY = "【APIキー】"

# 更新対象のレコードID
RECORD_ID = 【レコードID】

# リクエスト生成
payload = {
    "ApiKey": API_KEY,
    "RecordPermissions": ["Group,1,511"],
}

# API 呼び出し
url = f"{BASE_URL}/api/items/{RECORD_ID}/update"
response = requests.post(
    url,
    headers={"Content-Type": "application/json"},
    data=json.dumps(payload),
)

# 結果判定
if response.ok:
    print("更新成功")
else:
    print("更新失敗")

print(response.status_code, response.text)

```

##### 実行

```
>python api_record_update_p4.py
```

##### 実行結果

```
更新成功
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件C \" を更新しました。"}
```

</details>

<details markdown="1">
<summary>5. プロセスを実行</summary>

任意のプロセスを実行します。

##### Python(api_record_update_p5.py)

```
# WebサイトやAPIと通信するためのライブラリ
import requests

# JSON操作のためのライブラリ
import json

# 対象URLとAPIキーの設定
BASE_URL = "【対象URL】"
API_KEY = "【APIキー】"

# 更新対象のレコードID
RECORD_ID = 【レコードID】

# リクエスト生成
payload = {
    "ApiKey": API_KEY,
    "ProcessId": 1,
}

# API 呼び出し
url = f"{BASE_URL}/api/items/{RECORD_ID}/update"
response = requests.post(
    url,
    headers={"Content-Type": "application/json"},
    data=json.dumps(payload),
)

# 結果判定
if response.ok:
    print("更新成功")
else:
    print("更新失敗")

print(response.status_code, response.text)

```

##### 実行

```
>python api_record_update_p5.py
```

##### 実行結果

```
更新成功
200 {"Id":9999,"StatusCode":200,"Message":"\" サンプル案件C \" を更新しました。"}
```

</details>

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.19.0以降|[Wiki](../../../users-guide/wiki/index.md)でのImageHashを使用した画像の挿入機能を追加|

## 仕様変更について

**※ 2019年10月よりAPIの仕様が一部変更となりました。**
- 分類, 数値, 日付, 説明, チェック項目はjsonにそのまま記載する方法から「～Hash」の中に記載する方法へ変更されました。

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。