---
title: テナント停止
category: API
order: '400'
status: ''
parts: ''
urlstring: api-tenant-suspend
translationKey: api-tenant-suspend
shortname: テナント停止
created: 2026-08-03
updated: 2026-08-12
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/developers-guide/api/tenant-operations/assets/2e34651fb7874a8d8ee277f97c1dbb35.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/developers-guide/api/tenant-operations/assets/6cf22670b9dc4e1e8399edcbd8b9ec65.svg#only-dark)](https://pleasanter.org/support/)

## 概要

APIを使用してテナントを停止します。停止したテナントのユーザはログインできなくなります。停止したテナントは[テナント再開](api-tenant-resume.md)で再開できます。

## 前提条件

1. 「[マルチテナント管理機能](../../../products-info/manage-multi-tenant.md)」の前提条件を確認してください。

## 制限事項

1. 保護テナント（[MultiTenant.json](../../../setup/parameters/multitenant-json.md)のパラメータ「DefaultTenantId」で指定したテナント）は停止できません。

## リクエスト

下記のリクエスト形式で、JSONデータを送信します。

| 設定項目     | 値                                                      |
| :----------- | :------------------------------------------------------ |
| HTTPメソッド | POST                                                    |
| Content-Type | application/json                                        |
| 文字コード   | UTF-8                                                   |
| URL          | http://{サーバ名}/api/tenants/{テナントID}/Suspend (※1) |
|Body|以下のJSONデータを参考のこと。詳細は「[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)」を参照してください。|

※1　{サーバ名}、{テナントID}の部分は、適宜、環境に合わせて編集してください。{テナントID}には停止対象のテナントIDを指定してください。テナントIDは[テナント一覧取得](api-tenant-get.md)で確認できます。

### Bodyに指定する項目

##### JSON

```json
{
    "ApiKey": "（特権ユーザのAPIキー）",
    "SuspendDate": "2026-08-01"
}
```

### APIパラメータ

| 項目名      | 型       | 必須 | 備考                               |
| :---------- | :------- | :--- | :--------------------------------- |
| ApiKey      | string   | ○    | 特権ユーザのAPIキー                |
| SuspendDate | DateTime | －   | 停止日。省略時は操作日が設定されます |

## 実行例のサンプル

コード内の{{ ... }}やAPIキーは適宜修正してください。

### PowerShellのサンプル

##### PowerShell

```ps1
$body = @{
    ApiKey      = "（特権ユーザのAPIキー）"
    SuspendDate = "2026-08-01"
} | ConvertTo-Json
Invoke-RestMethod -Uri "https://{{サーバ名}}/api/tenants/{{テナントID}}/Suspend" -Method Post -ContentType "application/json; charset=utf-8" -Body $body
```

### Pythonのサンプル

##### Python

```py
import requests

res = requests.post("https://{{サーバ名}}/api/tenants/{{テナントID}}/Suspend", json={
    "ApiKey": "（特権ユーザのAPIキー）",
    "SuspendDate": "2026-08-01",
})
print(res.status_code, res.json())
```

## レスポンス

成功した場合、下記の形式のJSONデータが返却されます。「Response.Id」は停止したテナントのテナントIDです。

##### JSON

```json
{
    "StatusCode": 200,
    "Response": {
        "Id": 2,
        "Message": "（テナント名を含む停止完了メッセージ）"
    }
}
```

エラーの場合は下記が返却されます。

| StatusCode | 状況                                                         |
| :--------- | :----------------------------------------------------------- |
| 400        | URLに指定したテナントIDが不正（0以下）                       |
| 403        | 保護テナントを指定した                                       |
| 404        | 指定したテナントIDのテナントが存在しない、または削除申請済み |

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。  

??? note "1. テナントをコマンドラインから作成・一覧取得・停止・再開・削除申請する（Python）"

    Pleasanterのマルチテナント管理API（Create・Get・Suspend・Resume・Delete）を、コマンドラインから操作します。

    ### 実務での使いどころ

    1. マルチテナント管理者（特権ユーザ）が、契約に応じたテナントのライフサイクル管理（新規契約時の作成、稼働状況の一覧取得、一時停止からの再開、解約時の停止→削除申請）を行う際に使えます。
    2. GUIでの操作と異なり、複数テナントに対する一連の操作をコマンドやスクリプトから素早く実行できます。
    3. deleteは誤操作防止のため、対象テナントの名前を完全一致で手入力する確認を必ず経由する設計です。誤って別のテナントを削除してしまう事故を防ぐための、意図した制約です。

    ### 事前準備

    1. [特権ユーザ](../../../managers-guide/user-administration/user-management-privileged-users.md)で[APIキー](../basics/api-key.md)を発行してください。

        > **注意**: 一般ユーザのAPIキーでは、すべてのコマンドが403エラーになり、正しく動作しません。

    2. 発行したAPIキーを、環境変数「**PLEASANTER_API_KEY**」に設定してください。

        - コマンドプロンプトで実行の場合
          ```
          set PLEASANTER_API_KEY=APIキー
          ```
        - PowerShellで実行の場合
          ```
          $env:PLEASANTER_API_KEY="APIキー"
          ```

    3. 必要なPythonパッケージ（requests）をインストールしてください。

        ```
        pip install requests
        ```

    ### 使い方

    ```
    python tenant_admin.py <サブコマンド> [オプション]
    ```

    | サブコマンド | 必須 | オプション | 説明 |
    |:--|:--|:--|:--|
    | create | --tenant-name --login-id --name --notify-mail | --title --lang | テナントと初期管理ユーザを作成する |
    | get | なし | なし | 全テナントの一覧を取得する |
    | suspend | --tenant-id | --suspend-date YYYY-MM-DD | テナントを停止する |
    | resume | --tenant-id | なし | テナントを再開する |
    | delete | --tenant-id | なし | テナントの削除を申請する（対話的な名前確認あり） |

    ### Python(tenant_admin.py)

    ```python
    import argparse
    import datetime
    import os

    import requests

    # =========================
    # 設定
    # =========================
    BASE_URL = "【URL】"  # PleasanterサーバーのベースURL
    API_KEY = os.environ.get("PLEASANTER_API_KEY")  # 特権ユーザのAPIキー。直書きせず環境変数から取得する
    if not API_KEY:
        raise SystemExit("エラー: 環境変数 PLEASANTER_API_KEY が設定されていません。")

    API_VERSION = 1.1  # マルチテナント管理APIのApiVersion固定値
    DATE_FORMAT = "%Y-%m-%d"  # --suspend-date で受け付ける日付形式
    PAGE_SIZE = 200  # Get実行時のページサイズ（Api.jsonの既定値に合わせる）

    TENANTS_CREATE_PATH = "/api/tenants/Create"  # テナント作成APIのエンドポイントパス
    TENANTS_GET_PATH = "/api/tenants/Get"  # テナント一覧取得APIのエンドポイントパス

    # =========================
    # 共通処理
    # =========================
    def call_api(path: str, extra_payload: dict | None = None) -> dict:
        """共通ヘッダ（ApiVersion・ApiKey）を付与してPOSTし、レスポンスJSONを返す"""
        payload = {"ApiVersion": API_VERSION, "ApiKey": API_KEY, **(extra_payload or {})}
        try:
            r = requests.post(f"{BASE_URL}{path}", json=payload, timeout=30)
        except requests.exceptions.RequestException as e:
            raise SystemExit(f"エラー: APIサーバーへの接続に失敗しました。({e})")
        try:
            return r.json()
        except ValueError:
            raise SystemExit(f"エラー: APIから不正な応答が返されました。(HTTP {r.status_code})")

    def print_result(body: dict) -> bool:
        """StatusCode・Messageを加工せずラベル付きで表示する。StatusCode=200かどうかを返す"""
        message = (body.get("Response") or {}).get("Message") or body.get("Message")
        print(f"  ステータス : {body.get('StatusCode')}")
        print(f"  メッセージ : {message}")
        return body.get("StatusCode") == 200

    def fetch_all_tenants() -> list[dict]:
        """
        テナント一覧を全件取得する（delete時の安全確認などに使う内部処理）。
        PageSizeを明示指定し、Offsetを進めながらページングする。
        """
        tenants, offset = [], 0
        while True:
            body = call_api(TENANTS_GET_PATH, {"Offset": offset, "PageSize": PAGE_SIZE})
            if body.get("StatusCode") != 200:
                print_result(body)
                raise SystemExit(1)
            page = (body.get("Response") or {}).get("Data") or []
            tenants.extend(page)
            if len(page) < PAGE_SIZE:
                return tenants
            offset += PAGE_SIZE

    def valid_date(value: str) -> str:
        """--suspend-date引数がYYYY-MM-DD形式であることを検証する"""
        try:
            datetime.datetime.strptime(value, DATE_FORMAT)
        except ValueError:
            raise argparse.ArgumentTypeError(f"日付は{DATE_FORMAT}形式で指定してください。")
        return value

    # =========================
    # サブコマンド処理
    # =========================
    def cmd_create(args):
        """createサブコマンドの処理：テナントと初期管理ユーザを作成する"""
        payload = {
            "TenantName": args.tenant_name,
            "LoginId": args.login_id,
            "Name": args.name,
            "NotifyMailAddress": args.notify_mail,
        }
        if args.title:
            payload["Title"] = args.title
        if args.lang:
            payload["Language"] = args.lang
        if not print_result(call_api(TENANTS_CREATE_PATH, payload)):
            raise SystemExit(1)

    def cmd_get(args):
        """getサブコマンドの処理：全テナントを取得して一覧表示する"""
        tenants = fetch_all_tenants()
        print(f"  取得件数 : {len(tenants)} 件")
        for t in tenants:
            print(f"    TenantId : {t.get('TenantId')}  TenantName : {t.get('TenantName')}")

    def cmd_suspend(args):
        """suspendサブコマンドの処理：指定テナントを停止する"""
        payload = {"SuspendDate": args.suspend_date} if args.suspend_date else {}
        if not print_result(call_api(f"/api/tenants/{args.tenant_id}/Suspend", payload)):
            raise SystemExit(1)

    def cmd_resume(args):
        """resumeサブコマンドの処理：指定テナントを再開する"""
        if not print_result(call_api(f"/api/tenants/{args.tenant_id}/Resume")):
            raise SystemExit(1)

    def cmd_delete(args):
        """
        誤操作防止のため、一覧取得 → テナント名の入力確認 → 完全一致時のみ削除申請、の順で行う。
        """
        tenants = fetch_all_tenants()
        target = next((t for t in tenants if t.get("TenantId") == args.tenant_id), None)
        if target is None:
            raise SystemExit(f"エラー: テナントID {args.tenant_id} は一覧の中に見つかりませんでした。削除申請を中断します。")

        tenant_name = target.get("TenantName")
        prompt = f"削除申請対象: {tenant_name}（テナントID: {args.tenant_id}）。確認のため、テナント名を入力してください: "
        if input(prompt) != tenant_name:
            raise SystemExit("テナント名が一致しないため、削除申請を中断しました。")

        if not print_result(call_api(f"/api/tenants/{args.tenant_id}/Delete")):
            raise SystemExit(1)

    def build_arg_parser():
        """5つのサブコマンド（create/get/suspend/resume/delete）を持つArgumentParserを構築する"""
        parser = argparse.ArgumentParser(description="Pleasanter マルチテナント管理APIクライアント")
        sub = parser.add_subparsers(dest="command", required=True)

        p = sub.add_parser("create", help="テナントを作成する")
        p.add_argument("--tenant-name", required=True)
        p.add_argument("--login-id", required=True)
        p.add_argument("--name", required=True)
        p.add_argument("--notify-mail", required=True)
        p.add_argument("--title")
        p.add_argument("--lang")

        sub.add_parser("get", help="テナント一覧を取得する")

        p = sub.add_parser("suspend", help="テナントを停止する")
        p.add_argument("--tenant-id", type=int, required=True)
        p.add_argument("--suspend-date", type=valid_date, help="YYYY-MM-DD、省略時は即時停止")

        p = sub.add_parser("resume", help="テナントを再開する")
        p.add_argument("--tenant-id", type=int, required=True)

        p = sub.add_parser("delete", help="テナントの削除を申請する")
        p.add_argument("--tenant-id", type=int, required=True)

        return parser

    COMMAND_HANDLERS = {
        "create": cmd_create,
        "get": cmd_get,
        "suspend": cmd_suspend,
        "resume": cmd_resume,
        "delete": cmd_delete,
    }

    # =========================
    # メイン
    # =========================
    def main():
        """エントリポイント：引数を解析し、対応するサブコマンド処理を呼び出す"""
        args = build_arg_parser().parse_args()
        COMMAND_HANDLERS[args.command](args)

    if __name__ == "__main__":
        main()
    ```

    ### 実行例

    下記は、1つのテナントに対して一連の操作を行う例です。

    1. テナントを新規作成します。

        #### 実行

        ```
        python tenant_admin.py create --tenant-name 検証用テナント02 --login-id verifytenant01 --name 検証太郎 --notify-mail verify@example.com
        ```

        #### 実行結果

        ```
          ステータス : 200
          メッセージ : "検証用テナント02" を作成しました。
        ```

    2. テナント一覧を取得します。

        #### 実行

        ```
        python tenant_admin.py get
        ```

        #### 実行結果

        ```
          取得件数 : 2 件
            TenantId : 1  TenantName : 検証用テナント01
            TenantId : 2  TenantName : 検証用テナント02
        ```

    3. テナントを一時停止します。

        #### 実行

        ```
        python tenant_admin.py suspend --tenant-id 2
        ```

        #### 実行結果

        ```
          ステータス : 200
          メッセージ : "検証用テナント02" を停止しました。
        ```

    4. 一時停止したテナントを再開します。

        #### 実行

        ```
        python tenant_admin.py resume --tenant-id 2
        ```

        #### 実行結果

        ```
          ステータス : 200
          メッセージ : "検証用テナント02" を再開しました。
        ```

    5. テナントを停止してから削除を申請します。

        #### 実行

        ```
        python tenant_admin.py suspend --tenant-id 2
        python tenant_admin.py delete --tenant-id 2
        ```

        #### 実行結果

        ```
          ステータス : 200
          メッセージ : "検証用テナント02" を停止しました。
        削除申請対象: 検証用テナント02（テナントID: 2）。確認のため、テナント名を入力してください: 検証用テナント02
          ステータス : 200
          メッセージ : "検証用テナント02" を削除しました。
        ```

    ### エラー時の確認事項

    すべてのコマンド共通で、APIのStatusCodeが200以外の場合は次の形式で表示されます。

    メッセージ部分にはAPIから返された内容がそのまま表示されます。エラーの詳細については各マニュアルを参照してください。

    ```
      ステータス : <コード>
      メッセージ : <APIから返されたメッセージ>
    ```

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.7.0 以降   | 機能追加 |

## 関連情報

-   [マルチテナント管理機能](../../../products-info/manage-multi-tenant.md)  
-   [テナント作成](api-tenant-create.md)  
-   [テナント一覧取得](api-tenant-get.md)  
-   [テナント再開](api-tenant-resume.md)  
-   [テナント削除](api-tenant-delete.md)