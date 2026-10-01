---
title: グループ取得
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-group-get
translationKey: api-group-get
shortname: グループ取得API
created: 2022-05-16
updated: 2026-09-08
---

## 概要

APIを使用してグループのレコードを取得することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/groups/get (※1)|
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/groups/get

##### JSON  

```
{
    "ApiVersion": 1.1,
    "ApiKey": "sad610bHDo04720DoloA356...",
    "View": {
        "ColumnFilterHash": {
            "GroupId": "[11,12]"
        }
    }
}
```

GroupIdによるフィルタは、複数の値を指定可能な配列となっておりますので上記のように記述してください。

## レスポンス

下記の形式のjsonデータが選択したGroupIdの数だけ返却されます。  データのレイアウトは[こちら](../../json-data-layout/api-group.md)を参照してください。  

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
                "TenantId": 1,
                "GroupId": 11,
                "Ver": 1,
                "GroupName": "グループA",
                "Body": "",
                "Disabled": false,
                "Comments": "[]",
                "Creator": 1,
                "Updator": 1,
                "CreatedTime": "2023-04-01T12:00:00",
                "UpdatedTime": "2023-08-15T12:00:00",
                "GroupMembers": [
                    "User,1,True",
                    "User,2,False",
                    "Dept,1,True"
                ],
                "GroupChildren": [
                     "Group,1,"
                ],
                "ApiVersion": 1.1,
                "ClassHash": {
                },
                "NumHash": {
                },
                "DateHash": {
                },
                "DescriptionHash": {
                },
                "CheckHash": {
                },
                "AttachmentsHash": {
                }
            }
        ]
    }
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

??? note "2. 外部連携されたCSVを読み込みグループおよび親子関係を作成/更新する"

    本サンプルは、外部システムから出力されたCSVをもとに
    Pleasanterのグループ作成API / グループ更新APIを利用して
    グループおよび親子関係を登録するサンプルです。

    #### 概要

    外部システムの組織情報をCSVで受け取り、
    Pleasanterのグループ作成・更新APIを利用してグループ構造を作成します。

    本サンプルでは **2フェーズ処理** で実現しています。

    | フェーズ   | 処理内容                |
    | ------ | ------------------- |
    | Phase1 | グループ本体とメンバーを作成 / 更新 |
    | Phase2 | グループ親子関係を更新         |

    処理の流れは次の通りです。

    1. 入力CSVを読み込む
    2. Pleasanterから既存グループを取得する（/api/groups/get）
    3. Pleasanterから既存ユーザを取得する（/api/users/get）
    4. Phase1-グループ名をもとに create / update を判定し、グループ本体とメンバーを登録する（/api/groups/create または /api/groups/{GroupId}/update）
    5. Pleasanterから既存グループを再取得する（/api/groups/get）
    6. Phase2-親子関係を含めてグループを再更新する（/api/groups/{GroupId}/update）

    #### 前提

    ユーザは事前にPleasanterへ登録済み
    グループ名は一意である(作成/更新の判定に使用)

    ####  入力ファイル

    入力ファイルは4つです。

    ```text
    input/
     ├ groups.csv
     ├ users.csv
     ├ user_group_memberships.csv
     └ group_relations.csv
    ```

    ##### groups.csv

    グループ情報を定義します。

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
    GRP_EAST,東日本営業部,1,営業東日本
    ```

    ##### users.csv

    ユーザ情報を定義します。

    | 列名        | 説明               |
    | --------- | ---------------- |
    | user_id   | ユーザ識別ID          |
    | login_id  | PleasanterログインID |
    | user_name | ユーザ名             |
    | mail      | メール              |
    | is_active | 1:有効 / 0:無効    |

    サンプル

    ```csv
    user_id,login_id,user_name,mail,is_active
    0001,yamada.taro,山田 太郎,yamada@example.co.jp,1
    0002,sato.hanako,佐藤 花子,sato@example.co.jp,1
    ```

    ##### user_group_memberships.csv

    グループのメンバー情報を定義します。

    | 列名             | 説明        |
    | -------------- | --------- |
    | user_id        | ユーザID     |
    | group_code     | グループコード   |
    | is_active      | 1:有効 / 0:無効     |
    | is_group_admin | 1:グループ管理者 / 0:通常ユーザ　 |

    サンプル

    ```csv
    user_id,group_code,is_active,is_group_admin
    0001,GRP_ADMIN,1,1
    0002,GRP_SALES,1,0
    ```

    ##### group_relations.csv

    グループの親子関係を定義します。

    | 列名                | 説明    |
    | ----------------- | ----- |
    | parent_group_code | 親グループ |
    | child_group_code  | 子グループ |
    | is_active         | 1:対象 / 0:対象外  |

    サンプル

    ```csv
    parent_group_code,child_group_code,is_active
    GRP_SALES,GRP_EAST,1
    ```

    ##### Python(api_group_upsert.py)
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

    # ==============================
    # ファイル設定(環境にあわせ適宜変更してください)
    # ==============================
    INPUT_DIR = Path("./input")
    GROUPS_CSV = INPUT_DIR / "groups.csv"
    USERS_CSV = INPUT_DIR / "users.csv"
    MEMBERSHIPS_CSV = INPUT_DIR / "user_group_memberships.csv"
    RELATIONS_CSV = INPUT_DIR / "group_relations.csv"

    # ==============================
    # CSV入力設定(環境にあわせ適宜変更してください)
    # ==============================
    def read_csv(path):
        with open(path, "r", encoding="utf-8-sig", newline="") as f:
            return [
                {k.strip(): (v or "").strip() for k, v in row.items()}
                for row in csv.DictReader(f)
            ]

    def is_active(row):
        return str(row.get("is_active", "1")).strip() == "1"

    def to_bool_text(value):
        return "True" if str(value).strip() == "1" else "False"

    # ==============================
    # Pleasanter API操作
    # ==============================
    def post_json(url, payload):
        r = requests.post(
            url,
            json=payload,
            headers={"Content-Type": "application/json"},
            timeout=60,
        )
        r.raise_for_status()
        return r.json()

    # ==============================
    # グループ取得
    # ==============================
    def get_groups():
        data = post_json(
            f"{BASE_URL}/api/groups/get",
            {"ApiVersion": API_VERSION, "ApiKey": API_KEY},
        )
        return {
            row["GroupName"]: row
            for row in data.get("Response", {}).get("Data", [])
            if row.get("GroupName")
        }

    # ==============================
    # ユーザー取得
    # ==============================
    def get_users():
        data = post_json(
            f"{BASE_URL}/api/users/get",
            {"ApiVersion": API_VERSION, "ApiKey": API_KEY},
        )
        return {
            row["LoginId"]: row
            for row in data.get("Response", {}).get("Data", [])
            if row.get("LoginId")
        }

    # ==============================
    # グループの作成/更新
    # ==============================
    def upsert_group(group_name, payload, existing_groups):
        current = existing_groups.get(group_name)

        if current:
            url = f"{BASE_URL}/api/groups/{current['GroupId']}/update"
            result = post_json(url, payload)
            print(f"[UPDATE] {group_name}")
        else:
            url = f"{BASE_URL}/api/groups/create"
            result = post_json(url, payload)
            print(f"[CREATE] {group_name}")

        return result

    # ==============================
    # グループメンバーの設定
    # ==============================
    def build_member_map(memberships):
        result = {}
        for row in memberships:
            if not is_active(row):
                continue
            group_code = row["group_code"]
            result.setdefault(group_code, []).append(row)
        return result

    # ==============================
    # 親子関係の構築
    # ==============================
    def build_relation_map(relations):
        result = {}
        for row in relations:
            if not is_active(row):
                continue
            parent_code = row["parent_group_code"]
            result.setdefault(parent_code, []).append(row["child_group_code"])
        return result

    # ==============================
    # Phase1のリクエストペイロードの構築
    # ==============================
    def build_payload_phase1(group_row, member_rows, users_by_id, pleasanter_users):
        members = []

        for row in member_rows:
            user = users_by_id[row["user_id"]]
            login_id = user["login_id"]
            pleasanter_user = pleasanter_users[login_id]
            user_id = pleasanter_user["UserId"]
            is_admin = to_bool_text(row.get("is_group_admin", "0"))
            members.append(f"User,{user_id},{is_admin}")

        return {
            "ApiVersion": API_VERSION,
            "ApiKey": API_KEY,
            "GroupName": group_row["group_name"],
            "Body": group_row.get("remark", ""),
            "GroupMembers": members,
            "GroupChildren": [],
        }

    # ==============================
    # Phase2のリクエストペイロードの構築
    # ==============================
    def build_payload_phase2(
        group_row,
        member_rows,
        child_codes,
        users_by_id,
        groups_by_code,
        pleasanter_users,
        existing_groups,
    ):
        members = []

        for row in member_rows:
            user = users_by_id[row["user_id"]]
            login_id = user["login_id"]
            pleasanter_user = pleasanter_users[login_id]
            user_id = pleasanter_user["UserId"]
            is_admin = to_bool_text(row.get("is_group_admin", "0"))
            members.append(f"User,{user_id},{is_admin}")

        children = []

        for child_code in child_codes:
            child_name = groups_by_code[child_code]["group_name"]
            child_group = existing_groups[child_name]
            children.append(f"Group,{child_group['GroupId']},")

        return {
            "ApiVersion": API_VERSION,
            "ApiKey": API_KEY,
            "GroupName": group_row["group_name"],
            "Body": group_row.get("remark", ""),
            "GroupMembers": members,
            "GroupChildren": children,
        }

    # ==============================
    # メイン処理
    # ==============================
    def main():
        groups = read_csv(GROUPS_CSV)
        users = read_csv(USERS_CSV)
        memberships = read_csv(MEMBERSHIPS_CSV)
        relations = read_csv(RELATIONS_CSV)

        groups_by_code = {row["group_code"]: row for row in groups}
        users_by_id = {row["user_id"]: row for row in users}
        members_by_group = build_member_map(memberships)
        children_by_parent = build_relation_map(relations)

        pleasanter_users = get_users()
        existing_groups = get_groups()

        # Phase 1: 全グループを作成/更新（子グループなし）
        print("=== Phase 1 ===")
        for group in groups:
            payload = build_payload_phase1(
                group,
                members_by_group.get(group["group_code"], []),
                users_by_id,
                pleasanter_users,
            )
            upsert_group(group["group_name"], payload, existing_groups)
            existing_groups = get_groups()

        # Phase 2: 親子関係を更新
        print("=== Phase 2 ===")
        existing_groups = get_groups()

        for group in groups:
            payload = build_payload_phase2(
                group,
                members_by_group.get(group["group_code"], []),
                children_by_parent.get(group["group_code"], []),
                users_by_id,
                groups_by_code,
                pleasanter_users,
                existing_groups,
            )
            upsert_group(group["group_name"], payload, existing_groups)

    if __name__ == "__main__":
        main()
    ```

    ##### 実行
    ```text
    >python api_group_upsert.py
    ```
    ##### 実行結果
    ```text
    === Phase 1 ===
    [CREATE] 管理本部
    [CREATE] 営業本部
    [CREATE] 東日本営業部
    === Phase 2 ===
    [UPDATE] 管理本部
    [UPDATE] 営業本部
    [UPDATE] 東日本営業部
    ```

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 仕様変更について

**※ 2018年11月よりAPIの仕様が一部変更となりました。**
- URLの形式が '/pleasanter/api_items/xxxx' から '/pleasanter/api/items/xxxx' に変更されました。
- Content-Type の指定が'application/x-www-form-urlencoded' から 'application/json'に変更されました。