---
title: サイト作成
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-site-create
translationKey: api-site-create
shortname: ''
created: 2022-04-15
updated: 2026-09-11
---

## 概要

APIを使用してサイトを作成することができます。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。また、この機能はテナント管理者でないと行えないため、ユーザ管理からテナント管理者の設定を行ってください。

## リクエスト

下記のリクエスト形式で、jsonデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバ名}/api/items/{親サイトID}/createsite(※１)| 
|Body|以下のjsonデータを参考のこと|

(※1){サーバ名}、{親サイトID}の部分は、適宜、環境に合わせて編集してください。
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{親サイトID}/createsite  
　　{親サイトID}には、サイトを作成する対象の親サイトを指定してください。

##### JSON

```
{
    "ApiVersion": "1.1",
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "TenantId": 1,
    "Title": "サイト名",
    "ReferenceType": "Issues",
    "InheritPermission": 99999,
    "SiteSettings": {
        "Version": 1.017,
        "ReferenceType": "Issues",
        "GridColumns": [
            "IssueId",
            "TitleBody",
            "Comments",
            "StartTime",
            "CompletionTime",
            "WorkValue",
            "ProgressRate",
            "RemainingWorkValue",
            "Status",
            "Manager",
            "Owner",
            "Updator",
            "UpdatedTime"
        ],
        "EditorColumnHash": {
            "General": [
                "IssueId",
                "Ver",
                "Title",
                "Body",
                "StartTime",
                "CompletionTime",
                "WorkValue",
                "ProgressRate",
                "RemainingWorkValue",
                "Status",
                "Manager",
                "Owner",
                "Comments"
            ]
        }
    }
}
```
※TenantID以降のパラメータについては、サイトパッケージをエクスポートした際の、"Site”パラメータと同等の値を設定してください。

以下の例ではWikiを作成します。

##### JSON

```json
{
    "ApiVersion": 1.1,
    "ApiKey": "345yuAjA6789dA09d8uj6...",
    "Title": "Wiki test",
    "ReferenceType": "Wikis",
    "ParentId": 1,
    "InheritPermission": 1,
    "SiteSettings": {
        "ReferenceType": "Wikis"
    }
}
```

## サンプルコード

##### コード内の{{ ... }} は適宜修正してください。

<details markdown="1">
<summary>1. 任意のサイトパッケージを読み込み、その情報でサイトを作成する</summary>

任意のフォルダにサイトパッケージを配置しておき、プログラムで読み込み、その内容をもってサイトを作成します。

なお、サイトパッケージは複数サイトをエクスポートすることも可能ですが、当サンプルコードでは、その中の1番目のサイトの情報で作成します。(Site[0]から作成)

また、Python実行時にサイト名を指定する仕様となっています。未指定の場合、エラーとなります。

##### api_site_create_p1.py

```
# 引数取得のためのライブラリ
import argparse

# JSON操作、システム操作、パス操作のためのライブラリ
import json

# システム操作のためのライブラリ
import sys

# パス操作のためのライブラリ
from pathlib import Path

# HTTPリクエスト送信用のライブラリ
import requests

# サーバ名、APIキー
BASE_URL = "{{URL}}"
API_KEY = "{{APIキー}}"

# サイト作成先となる親サイト
PARENT_SITE_ID = {{サイトID}}

# サイトパッケージの配置フォルダ
PACKAGE_DIR = Path(r"{{ファイルパス}}")

# 利用するサイトパッケージファイル名
PACKAGE_FILE_NAME = "{{サイトパッケージファイル名}}.json"

# サイトパッケージJSONを読み込む。
def load_site_package() -> dict:
    package_path = PACKAGE_DIR / PACKAGE_FILE_NAME
    if not package_path.exists():
        raise FileNotFoundError(f"サイトパッケージが見つかりません: {package_path}")

    with package_path.open("r", encoding="utf-8-sig") as f:
        return json.load(f)

# サイトパッケージの Sites[0] をベースに、サイト作成API用のBodyを組み立てる。
def build_create_site_body(site_package: dict, title: str) -> dict:
    sites = site_package.get("Sites", [])
    if not sites:
        raise ValueError("サイトパッケージに 'Sites' が存在しない、または空です。")

    body = dict(sites[0])  # Sites[0] をコピー

    # 作成API用の必須/上書き項目
    body["ApiVersion"] = "1.1"
    body["ApiKey"] = API_KEY
    body["TenantId"] = 1

    body["Title"] = title
    body["SiteName"] = title

    # 親サイト配下に作成し、権限は親から継承
    body["ParentId"] = PARENT_SITE_ID
    body["InheritPermission"] = PARENT_SITE_ID

    # SiteId は新規作成時に不要なため削除
    body.pop("SiteId", None)

    return body

# サイト作成APIを呼び出す。
def create_site(body: dict) -> dict:
    url = f"{BASE_URL.rstrip('/')}/api/items/{PARENT_SITE_ID}/createsite"
    headers = {"Content-Type": "application/json"}

    response = requests.post(
        url,
        headers=headers,
        data=json.dumps(body, ensure_ascii=False),
    )

    if not response.ok:
        raise RuntimeError(f"API Error: {response.status_code}\n{response.text}")

    return response.json()

def main():
    parser = argparse.ArgumentParser(description="Pleasanter サイト作成API サンプル")
    parser.add_argument("title", help="作成するサイト名")
    args = parser.parse_args()

    site_package = load_site_package()
    body = build_create_site_body(site_package, args.title)
    result = create_site(body)

    print(json.dumps(result, ensure_ascii=False, indent=2))

if __name__ == "__main__":
    try:
        main()
    except Exception as e:
        print(f"エラー: {e}", file=sys.stderr)
        sys.exit(1)

```

##### 実行

引数に任意のサイト名を指定します。
```
>python api_site_create_p1.py {{サイト名}}
```

##### 実行結果

```
{
  "Id": 9999,
  "StatusCode": 200,
  "Message": "\" 課題管理_{{サイト名}} \" を作成しました。"
}
```

</details>

スクリプトでの使用方法は、以下のマニュアルを参照してください。  
[$p.apiCreateSite](../../script/script-api/script-api-create-site.md)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.4.0 以降|機能追加|
