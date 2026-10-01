---
title: レコードのインポート
category: API
order: '2000'
status: ''
parts: ''
urlstring: api-import
translationKey: api-import
shortname: レコードのインポートAPI
created: 2023-09-20
updated: 2026-07-14
---

## 概要

APIを使用して指定したテーブルにレコードをインポートします。

## 事前準備

APIの操作を行う前に[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式で、CSVデータとJSONパラメータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |multipart/form-data|  
|文字コード|UTF-8|
|URL|http://{サーバー名}/api/items/{サイトID}/import (※1)|
|Body|下記「Bodyに指定する項目」を参照のこと|

(※1){サーバー名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。  
　　pleasanter.netの場合は以下の形式になります。  
　　https\://pleasanter.net/fs/api/items/{サイトID}/import  

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
|UpdatableImport|true|「キーが一致するレコードを更新する」場合にtrueを指定|
|Key|IssueId|UpdatableImportをtrueに設定した場合のキー項目。キー項目が分類Aの場合は"ClassA"と設定|
|MigrationMode|true|[移行モードでのレコードのインポート](../../../users-guide/table/record-authoring/create-records/table-record-import-migrate-mode.md)を実施する場合にtrueを指定|

## 実行例のサンプル

以下のサンプルを実行した結果、APIキーが有効なユーザのもので間違いがなく、対象サイトに書き込み権限を持っているにも関わらず、レスポンスが403エラーとなる場合は、以下のFAQを参照してください。  
[FAQ：PowerShellを利用したAPIによるレコードのインポートで403エラーが発生する](../../../FAQ/features-for-developers/faq-api-import-error.md)

### PowerShell（version6.0 以降）のサンプル

##### PowerShell

```
$uri = 'http://servername/api/items/1234/import'
$filePath = "./sample.csv"
$form = @{
    parameters = ConvertTo-Json @{
        ApiVersion = 1.1;
        ApiKey = "4d84b4773a58bbc3c4...";
        Encoding = "UTF-8";
        UpdatableImport = $true;
        Key = "IssueId";
        MigrationMode = $false;
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

url = "https://servername/api/items/1234/import"
filePath = "./sample.csv"
data = {
    "parameters": json.dumps({
        "ApiVersion" : 1.1,
        "ApiKey" : "4d84b4773a58bbc3c4...",
        "Encoding" : "UTF-8",
        "UpdatableImport" : True,
        "Key" : "IssueId",
        "MigrationMode" : False
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
  "Id":1234,
  "StatusCode":200,
  "LimitPerDate":1000,
  "LimitRemaining":998,
  "Message":"テーブル名: 50 件追加し、12 件更新しました。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。  

??? note "1. CSVインポートにあわせて画像も登録する"

    ##### 概要

    Excelで管理していた画像とデータをPleasanterへ移行する際に、テキスト情報のCSVインポートと合わせて、画像もレコードに登録するためのバッチサンプルプログラムです。

    ##### 処理の流れ

    〇Step 1 ― テキスト情報のCSVインポート

    ExcelからCSV出力したファイルをインポートAPIで一括登録します。
    キー列が一致するレコードは更新されるため、再実行しても安全です。

    〇Step 2 ― レコードIDの取得

    インポート済みレコードをAPI経由で取得し、キー列の値とPleasanterのレコードIDを紐づけます。
    この対応関係をもとに、Step 3 でどのレコードを更新するかを決定します。

    〇Step 3 ― 画像の埋め込み登録

    画像フォルダを走査し、レコードごとに画像をAPIで登録します。
    フォルダ名でレコードを特定し、ファイル名で登録先の項目を判断します。

    ##### フォルダ名 / ファイル名と画像登録のルール

    〇フォルダ構成

    ```text
    images/
      {キーコード}/
        body.jpg
        desc_a.png
        desc_b.jpg
        desc_c.png
        comments.jpg
    ```

    〇フォルダ名のルール

    画像フォルダ直下に、**CSVのキー列の値と同じ名前**でフォルダを作成します。

    | フォルダ名 | 対応するレコード |
    |---|---|
    | P-001 | キー列の値が P-001 のレコード |
    | P-002 | キー列の値が P-002 のレコード |

    キー列の項目は、サンプルプログラム内の**KEY_COLUMN**に定義します。
    (本サンプルコードでは、’ClassB’)

    〇ファイル名のルール

    フォルダ内の画像ファイルは、**ファイル名（拡張子を除く）** によって登録先の項目が決まります。

    | ファイル名 | 登録先項目 |
    |---|---|
    | body | Body |
    | desc_a | DescriptionA |
    | desc_b | DescriptionB |
    | desc_c | DescriptionC |
    | comments | Comments |

    -   使用できる拡張子は .jpg .jpeg .png .gif です
    -   上記以外のファイル名はスキップされます
    -   登録不要な項目はファイルを置かなければ処理されません

    〇画像登録のイメージ

    ![画像フォルダ内のファイルが、レコードのBody・DescriptionA〜C・Commentsの各項目に登録されるイメージ](https://pleasanter.org/files/images/ja/developers-guide/api/table-operations/assets/0f5432989dba49e9a897e9bf36f7c7c4.png)

    ##### サンプルコード

    ```python
    import base64
    import json
    import os
    from pathlib import Path

    import requests

    # =========================
    # 設定
    # =========================
    BASE_URL = "【URL】"
    API_KEY = "【APIキー】"
    SITE_ID = 【サイトID】  # インポート先サイトのサイトID

    # CSVインポートの設定
    CSV_PATH = Path("./sample.csv")  # インポートするCSVファイルのパス
    CSV_ENCODING = "UTF-8"  # CSVのエンコーディング（"UTF-8" または "Shift-JIS"）
    KEY_COLUMN = "ClassB"  # CSVのキー列（管理番号など）。GetItems で照合に使用する

    # 画像フォルダのルートパス
    IMAGES_DIR = Path("./images")

    # "IssueId" or "ResultId"
    RECORD_ID_FIELD = "ResultId"

    # =========================
    # 共通処理
    # =========================
    # ファイル名プレフィックスと ImageHash のキー（Pleasanter の項目名）の対応
    FILE_PREFIX_MAP = {
        "body": "Body",
        "desc_a": "DescriptionA",
        "desc_b": "DescriptionB",
        "desc_c": "DescriptionC",
        "comments": "Comments",
    }

    SUPPORTED_EXTENSIONS = {".jpg", ".jpeg", ".png", ".gif"}

    def post_json(url: str, payload: dict) -> dict:
        response = requests.post(
            url,
            headers={"Content-Type": "application/json"},
            data=json.dumps(payload, ensure_ascii=False),
            timeout=60,
        )
        response.raise_for_status()
        return response.json()

    def post_file(url: str, params: dict, file_path: Path) -> dict:
        with open(file_path, "rb") as f:
            response = requests.post(
                url,
                data={"parameters": json.dumps(params, ensure_ascii=False)},
                files={"file": (file_path.name, f, "text/csv")},
                timeout=120,
            )
        response.raise_for_status()
        return response.json()

    def encode_image(file_path: Path) -> str:
        """画像ファイルをBase64エンコードして文字列で返す"""
        return base64.b64encode(file_path.read_bytes()).decode("utf-8")

    # =========================
    # Step 1: CSVインポート
    # =========================
    def step1_import_csv() -> None:
        print("=" * 50)
        print("Step 1: CSVインポート")
        print("=" * 50)

        url = f"{BASE_URL}/api/items/{SITE_ID}/import"
        params = {
            "ApiVersion": 1.1,
            "ApiKey": API_KEY,
            "Encoding": CSV_ENCODING,
            "UpdatableImport": True,  # キー一致のレコードは更新
            "Key": KEY_COLUMN,
            "MigrationMode": False,
        }

        result = post_file(url, params, CSV_PATH)
        print(f"  ステータス : {result.get('StatusCode')}")
        print(f"  メッセージ : {result.get('Message')}")

    # =========================
    # Step 2: レコードID取得
    # =========================
    def step2_get_record_ids() -> dict:
        """
        インポート済みレコードを全件取得し、キー列の値 → レコードID のマップを返す。
        レコード件数が多い場合はページングして全件取得する。
        """
        print("=" * 50)
        print("Step 2: レコードID取得")
        print("=" * 50)

        url = f"{BASE_URL}/api/items/{SITE_ID}/get"
        key_to_id = {}
        offset = 0
        page_size = 200

        while True:
            payload = {
                "ApiVersion": 1.1,
                "ApiKey": API_KEY,
                "Offset": offset,
                "PageSize": page_size,
            }

            result = post_json(url, payload)
            records = result.get("Response", {}).get("Data", [])

            if not records:
                break

            for rec in records:
                # ClassHash 形式と直接指定の両方に対応
                class_hash = rec.get("ClassHash", {})
                key_val = class_hash.get(KEY_COLUMN) or rec.get(KEY_COLUMN)
                record_id = rec.get(RECORD_ID_FIELD)
                if key_val and record_id:
                    key_to_id[str(key_val).strip()] = record_id

            if len(records) < page_size:
                break
            offset += page_size

        print(f"  取得件数 : {len(key_to_id)} 件")
        return key_to_id

    # =========================
    # Step 3: 画像の埋め込み更新
    # =========================
    def build_image_hash(key_dir: Path) -> dict:
        """
        キーディレクトリ内の画像ファイルを走査し、ImageHash 用の辞書を組み立てる。
        対象外のファイルは無視する。
        """
        image_hash = {}

        for file in sorted(key_dir.iterdir()):
            if not file.is_file():
                continue
            if file.suffix.lower() not in SUPPORTED_EXTENSIONS:
                continue

            # ファイル名のプレフィックスで登録先項目を特定
            prefix = file.stem.lower()
            target_field = FILE_PREFIX_MAP.get(prefix)
            if target_field is None:
                print(f"    [SKIP] 対象外のファイル名: {file.name}（スキップ）")
                continue

            image_hash[target_field] = {
                "HeadNewLine": True,
                "EndNewLine": True,
                "Extension": file.suffix.lower(),
                "Base64": encode_image(file),
            }
            print(f"    {file.name} → {target_field}")

        return image_hash

    def step3_update_images(key_to_id: dict) -> None:
        print("=" * 50)
        print("Step 3: 画像の埋め込み更新")
        print("=" * 50)

        if not IMAGES_DIR.exists():
            print(f"  画像フォルダが見つかりません: {IMAGES_DIR}")
            return

        success = skip = error = 0

        for key_dir in sorted(IMAGES_DIR.iterdir()):
            if not key_dir.is_dir():
                continue

            key_val = key_dir.name
            record_id = key_to_id.get(key_val)

            if record_id is None:
                print(f"  [SKIP] キー '{key_val}' に対応するレコードが見つかりません")
                skip += 1
                continue

            print(f"  キー: {key_val}  →  レコードID: {record_id}")
            image_hash = build_image_hash(key_dir)

            if not image_hash:
                print(f"    [SKIP] 登録対象の画像ファイルがありません")
                skip += 1
                continue

            payload = {
                "ApiVersion": 1.1,
                "ApiKey": API_KEY,
                "ImageHash": image_hash,
            }

            url = f"{BASE_URL}/api/items/{record_id}/update"
            try:
                result = post_json(url, payload)
                if result.get("StatusCode") == 200:
                    print(f"    [OK] 更新完了")
                    success += 1
                else:
                    print(
                        f"    [ERR] StatusCode={result.get('StatusCode')}  {result.get('Message')}"
                    )
                    error += 1
            except requests.HTTPError as e:
                print(f"    [ERR] HTTPエラー: {e}")
                error += 1

        print()
        print(f"完了  成功={success}  スキップ={skip}  エラー={error}")

    # =========================
    # メイン
    # =========================
    def main():
        step1_import_csv()
        print()
        key_to_id = step2_get_record_ids()
        print()
        step3_update_images(key_to_id)

    if __name__ == "__main__":
        main()

    ```

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../../../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../../FAQ/features-for-developers/faq-json-format.md)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.16.0 以降|MigrationModeパラメータの追加|

## 関連情報

-   [テーブル機能：移行モードでのレコードのインポート](../../../users-guide/table/record-authoring/create-records/table-record-import-migrate-mode.md)
-   [FAQ：PowerShellを利用したAPIによるレコードのインポートで403エラーが発生する](../../../FAQ/features-for-developers/faq-api-import-error.md)