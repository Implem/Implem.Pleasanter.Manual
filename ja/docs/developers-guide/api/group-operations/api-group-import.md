---
title: インポート
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-group-import
translationKey: api-group-import
shortname: ''
created: 2023-10-25
updated: 2026-03-17
---

## 概要

APIを使用してグループ情報をインポートします。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、CSVデータとJSONパラメータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |multipart/form-data|  
|文字コード|UTF-8|
|URL|http://{サーバー名}/api/groups/import (※1)|
|Body|下記「Bodyに指定する項目」を参照のこと|

(※1){サーバー名}の部分は、適宜、環境に合わせて編集してください。  

### Bodyに指定する項目

|項目名|値|
|:--|:--|  
|parameters|下記「APIパラメータ」の内容をJSON形式の文字列で指定|
|file|登録するCSVファイルのバイナリデータ|

### APIパラメータ

|項目名|設定例|備考|
|:--|:--|:--|  
|ApiVersion|1.1|APIバージョン|
|ApiKey|3da0fa3a7R61faf821...|取得したAPIキー|
|Encoding|Shift-JIS|CSVファイルのエンコーディング。"UTF-8"または"Shift-JIS"を指定|
|ReplaceAllGroupMembers|true|「メンバーを削除してからインポートする」か否かを指定。trueを指定した場合CSVファイル内のグループIDと一致するグループのメンバーがすべて削除されてからインポートが行われます。|

## 実行例のサンプル

### PowerShell（version6.0 以降）のサンプル

##### PowerShell

```
$uri = 'http://servername/api/groups/import'
$filePath = "./sample.csv"
$form = @{
    parameters = ConvertTo-Json @{
        ApiVersion = 1.1;
        ApiKey = "4d84b4773a58bbc3c4...";
        Encoding = "UTF-8";
    };
    file = Get-Item -Path $filePath;
}
Invoke-WebRequest -Uri $uri -Method Post -Form $form
```

### Pythonのサンプル

##### Python

```
import requests
import json

url = "https://servername/api/groups/import"
filePath = "./sample.csv"
data = {
    "parameters": json.dumps({
        "ApiVersion" : 1.1,
        "ApiKey" : "4d84b4773a58bbc3c4...",
        "Encoding" : "UTF-8"
    })            
}
files = {
    "file":("sample.csv", open(filePath,"rb"), "text/csv")
}
response = requests.post(url, data, files=files)
print(response.content.decode())
```

## レスポンス

下記の形式のjsonデータが返却されます。  

##### JSON

```
{
  "Id":0,
  "StatusCode":200,
  "Message":"50 件追加し、12 件更新しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。  

??? note "1. 外部連携されたCSVを読み込みグループをインポートする"

    本サンプルは、外部システムから出力されたCSVをもとに
    インポート用CSVを生成し、APIでインポートするサンプルです。

    #### 概要

    外部システムのユーザ・組織情報をCSV形式で受け取り、
    PleasanterのグループインポートAPIを利用してグループを作成または更新します。

    処理の流れは次の通りです。

    1. 入力CSVを読み込む
    2. Pleasanterから既存グループを取得(/api/groups/get)
    3. グループ名で既存グループを判定
    4. グループインポート用CSVを生成
    5. グループインポートAPIを実行(/api/groups/import)

    #### 前提

    ユーザは事前にPleasanterへ登録済み
    グループ名は一意である(作成/更新の判定に使用)

    #### 入力ファイル

    外部から連動想定の入力ファイルは3つです。

    ```text
    input/
     ├ groups.csv
     ├ users.csv
     └ user_group_memberships.csv
    ```

    ##### groups.csv

    グループ情報を定義するCSVです。

    | 列名         | 説明          |
    | ---------- | ----------- |
    | group_code | グループ識別コード   |
    | group_name | グループ名       |
    | is_active  | 1:有効 / 0:無効 |
    | remark     | 説明          |

    サンプル

    ```csv
    group_code,group_name,is_active,remark
    GRP_ADMIN,管理本部,1,管理部門
    GRP_SALES,営業本部,1,営業部門
    ```

    ##### users.csv

    ユーザ情報を定義するCSVです。

    | 列名        | 説明               |
    | --------- | ---------------- |
    | user_id   | ユーザ識別ID          |
    | login_id  | PleasanterログインID |
    | user_name | ユーザ名             |
    | mail      | メールアドレス          |
    | is_active | 1:有効 / 0:無効      |

    サンプル

    ```csv
    user_id,login_id,user_name,mail,is_active
    0001,yamada.taro,山田 太郎,yamada@example.co.jp,1
    0002,sato.hanako,佐藤 花子,sato@example.co.jp,1
    ```

    ##### user_group_memberships.csv

    ユーザとグループの所属関係を定義するCSVです。

    | 列名         | 説明          |
    | ---------- | ----------- |
    | user_id    | ユーザID       |
    | group_code | グループコード     |
    | is_active  | 1:有効 / 0:無効 |
    |is_group_admin| 1:グループの管理者 / 0:通常メンバー|

    サンプル

    ```csv
    user_id,group_code,is_active,is_group_admin
    0001,GRP_ADMIN,1,1
    0002,GRP_ADMIN,1,0
    ```

    #### 出力ファイル

    生成されるCSVは以下です。

    ```text
    output/
     └ groups_import.csv
    ```

    CSVのフォーマットについては、[グループインポート](../../../managers-guide/group-administration/group-import.md)の仕様に従います。

    ##### Python(api_group_import.py)
    ```python
    import csv
    import json
    from pathlib import Path

    import requests

    # ==============================
    # Pleasanter 接続設定
    # ==============================
    BASE_URL = "【URL】"
    API_KEY = "【APIキー】"
    API_VERSION = 1.1
    ENCODING = "UTF-8"

    # True : CSV生成のみ
    # False: CSV生成後インポート実行
    DRY_RUN = True

    # ==============================
    # ファイル設定(環境にあわせ適宜変更してください)
    # ==============================
    INPUT_DIR = Path("./input")
    OUTPUT_DIR = Path("./output")
    GROUPS_CSV = INPUT_DIR / "groups.csv"
    USERS_CSV = INPUT_DIR / "users.csv"
    MEMBERSHIPS_CSV = INPUT_DIR / "user_group_memberships.csv"
    GROUP_IMPORT_CSV = OUTPUT_DIR / "groups_import.csv"

    # ==============================
    # CSV入出力設定(環境にあわせ適宜変更してください)
    # ==============================
    def read_csv(path):
        with open(path, "r", encoding="utf-8-sig", newline="") as f:
            return [
                {k.strip(): (v or "").strip() for k, v in row.items()}
                for row in csv.DictReader(f)
            ]

    def write_csv(path, headers, rows):
        path.parent.mkdir(parents=True, exist_ok=True)
        with open(path, "w", encoding="utf-8-sig", newline="") as f:
            writer = csv.DictWriter(f, fieldnames=headers)
            writer.writeheader()
            writer.writerows(rows)

    def is_active(row):
        return str(row.get("is_active", "1")) == "1"

    def to_disabled(row):
        return "0" if is_active(row) else "1"

    def to_group_admin(row):
        return "1" if str(row.get("is_group_admin", "0")) == "1" else "0"

    # ==============================
    # Pleasanter API操作
    # ==============================
    def post_json(url, payload):
        r = requests.post(
            url,
            json=payload,
            headers={"Content-Type": "application/json"},
        )
        r.raise_for_status()
        return r.json()

    # ==============================
    # ファイルアップロード操作
    # ==============================
    def post_file(url, params, file_path):
        with open(file_path, "rb") as f:
            files = {"file": (file_path.name, f, "text/csv")}
            data = {"parameters": json.dumps(params)}
            r = requests.post(url, data=data, files=files)
        r.raise_for_status()
        return r.json()

    # ==============================
    # グループ登録済か確認するための辞書を作成
    # ==============================
    def get_existing_groups():
        data = post_json(
            f"{BASE_URL}/api/groups/get", {"ApiVersion": API_VERSION, "ApiKey": API_KEY}
        )

        groups = {}
        for row in data["Response"]["Data"]:
            groups[row["GroupName"]] = row
        return groups

    # ==============================
    # CSV用の行データを作成
    # ==============================
    def build_rows(groups, users, memberships, existing_groups):
        users_by_id = {u["user_id"]: u for u in users}
        groups_by_code = {g["group_code"]: g for g in groups}
        rows = []

        # グループ本体行
        for group in groups:
            current = existing_groups.get(group["group_name"], {})
            rows.append(
                {
                    "グループID": str(current.get("GroupId", "")),
                    "グループ名": group["group_name"],
                    "説明": group.get("remark", ""),
                    "メンバー種別": "",
                    "メンバーキー": "",
                    "メンバー名": "",
                    "メンバーは管理者": "0",
                    "無効": to_disabled(group),
                }
            )

        # メンバー行
        for membership in memberships:
            if not is_active(membership):
                continue

            group = groups_by_code[membership["group_code"]]
            user = users_by_id[membership["user_id"]]
            current = existing_groups.get(group["group_name"], {})

            rows.append(
                {
                    "グループID": str(current.get("GroupId", "")),
                    "グループ名": group["group_name"],
                    "説明": group.get("remark", ""),
                    "メンバー種別": "User",
                    "メンバーキー": user["login_id"],
                    "メンバー名": user["user_name"],
                    "メンバーは管理者": to_group_admin(membership),
                    "無効": to_disabled(group),
                }
            )

        return rows

    # ==============================
    # グループインポート実行
    # ==============================
    def import_groups(file_path):
        return post_file(
            f"{BASE_URL}/api/groups/import",
            {
                "ApiVersion": API_VERSION,
                "ApiKey": API_KEY,
                "Encoding": ENCODING,
                "ReplaceAllGroupMembers": True,
            },
            file_path,
        )

    # ==============================
    # メイン処理
    # ==============================
    def main():
        groups = read_csv(GROUPS_CSV)
        users = read_csv(USERS_CSV)
        memberships = read_csv(MEMBERSHIPS_CSV)

        existing_groups = get_existing_groups()
        rows = build_rows(groups, users, memberships, existing_groups)

        write_csv(
            GROUP_IMPORT_CSV,
            [
                "グループID",
                "グループ名",
                "説明",
                "メンバー種別",
                "メンバーキー",
                "メンバー名",
                "メンバーは管理者",
                "無効",
            ],
            rows,
        )

        print("CSV生成:", GROUP_IMPORT_CSV)

        if DRY_RUN:
            print("DRY_RUN=True のためインポートは実行しません")
            return

        result = import_groups(GROUP_IMPORT_CSV)
        print(json.dumps(result, indent=2, ensure_ascii=False))

    if __name__ == "__main__":
        main()
    ```

    ##### 実行
    ```text
    >python api_group_import.py
    ```
    ##### 実行結果
    ```text
    CSV生成: group_import\output\groups_import.csv
    {
      "Id": 0,
      "StatusCode": 200,
      "Message": ": グループ 0 件追加、0 件更新しました。グループメンバー 3 件追加、0 件更新しました。"
    }
    ```

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)
