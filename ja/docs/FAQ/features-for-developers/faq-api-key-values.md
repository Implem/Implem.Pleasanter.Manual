---
title: APIで表示名を取得したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-api-key-values
translationKey: faq-api-key-values
shortname: ''
created: 2023-10-13
updated: 2024-04-29
---

## 回答

「View」のApiDataTypeプロパティを"KeyValues"と指定してください。

---

## 概要

APIで子テーブルの情報を取得する際、通常レスポンスの中のリンクしている項目の値はレコードID(親テーブルの対象レコード)ですが、「View」のApiDataTypeプロパティを"KeyValues"と指定することで表示名(親テーブルの対象レコードのタイトル)でレスポンスを返却するようになります。

## サンプルデータ

このFAQでは下記の親子関係のテーブル、レコード情報をもとに記述しております。

<details markdown="1">
<summary>顧客マスタ(親テーブル)</summary>

|レコードID|顧客名|担当者|住所|連絡先|
|:--:|:--:|:--:|:--:|:--:|
|696|働き方改革推進団体|Brown Emily|東京都立川市|258-258-258|
|697|株式会社オープンソーステクノロジー|鈴木 洋一|東京都豊島区|555-555-555|
|698|生産性向上委員会|田中 恵子|東京都大田区|999-999-999|
|699|Webデータベース開発株式会社|渡邉 博|東京都練馬区|789-789-789|
|700|情報共有イノベーション研究所|山本 陽子|東京都新宿区|333-333-333|
|701|有限会社ノンプログラミング|中村 隆|東京都国分寺市|456-456-456|
|702|マネジメント快適化ホールディングス|加藤 誠|東京都中野区|123-123-123|
|703|株式会社プリザンター|斎藤 美樹|東京都中央区|111-111-111|

</details>

<details markdown="1">
<summary>商談(子テーブル)</summary>
<br>
顧客(ClassA)の選択肢一覧に顧客マスタとのリンクが設定されています。
<br>

|レコードID|件名|受注予定日|状況|管理者|担当者|顧客|商品区分|確度|売上|仕入合計|粗利|粗利率|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|704|AI技術の検証|45219|引き合い|佐々木 春香|佐々木 春香|マネジメント快適化ホールディングス|コンサルティング|0.9|1500000|1100000|400000|26.7|
|705|グループウェアのクラウド環境への移行|45226|提案|Brown Emily|Brown Emily|株式会社プリザンター|システム開発|0.9|4200000|0|4200000|100|
|706|食品工場内の環境モニタリングシステムの開発|45212|交渉|鈴木 洋一|鈴木 洋一|株式会社オープンソーステクノロジー|システム開発|0.5|4500000|3207000|1293000|28.7|
|707|グラフ化ツールの販売|45212|引き合い|田中 恵子|田中 恵子|有限会社ノンプログラミング|ソフトウェア販売|0.5|320000|280000|40000|12.5|
|708|業務改善コンサルティング|45221|提案|渡邉 博|渡邉 博|働き方改革推進団体|コンサルティング|0.3|1350000|638000|712000|52.7|
|709|営業支援ツールの追加機能開発|45228|交渉|山本 陽子|山本 陽子|情報共有イノベーション研究所|システム開発|0.9|540000|440000|100000|18.5|
|710|文書管理ソフトウェアの販売|45233|契約|中村 隆|小林 佳子|Webデータベース開発株式会社|ソフトウェア販売|0.5|688000|549000|139000|20.2|

</details>

## ①通常のレスポンスの場合

<details markdown="1">
<summary>サンプルコード (Python)</summary>
<br>
このサンプルでは商談(子テーブル)にある、商品区分(ClassB)に システム開発 が設定されているレコード情報を取得します。
<br>

```
import requests
import json

# サイトIDを指定
site_id = 620

# APIキーを指定
api_key = "de06bdbced9d395f1cf3f7afb8b084f95718e2cfb7f0759efd13210e386b4b954dbf70cbfe6f56e32492c098816a45e37616f1ec2da0ea71d2f10527795225a2"

# APIのURLを指定
url = f"http://localhost/api/items/{site_id}/get"

# 送信するデータを指定
data = {
    "ApiVersion": 1.1,
    "ApiKey": api_key,
    "View": {
        "ColumnFilterHash": {
            "ClassB": "[\"システム開発\"]"
        }
    }
}

# POSTリクエストを送信
response = requests.post(url, json=data)

# レスポンスを処理
if response.status_code == 200:
    response_data = json.loads(response.content)
    print(json.dumps(response_data, indent=4, ensure_ascii=False))
else:
    print(f"ErrorCode: {response.status_code}")
    print(response.text)
```

</details>

<details markdown="1">
<summary>レスポンス</summary>
レスポンスの顧客(ClassA)の値は顧客マスタ(親テーブル)の各レコードのIDで返却されています。

```
{
    "StatusCode": 200,
    "Response": {
        "Offset": 0,
        "PageSize": 200,
        "TotalCount": 3,
        "Data": [
            {
                "SiteId": 620,
                "UpdatedTime": "2023-09-27T10:41:00",
                "IssueId": 709,
                "Ver": 1,
                "Title": "営業支援ツールの追加機能開発",
                "Body": "５年前よりスクラッチで開発していた人事システムに、残業管理機能の追加を行います。\r\n本システム の開発当初から担当しているR社に発注し開発を行います。",
                "StartTime": "2023-10-05T00:00:00",
                "CompletionTime": "2023-10-29T00:00:00",
                "WorkValue": 0.0,
                "ProgressRate": 0.0,
                "RemainingWorkValue": 0.0,
                "Status": 200,
                "Manager": 13,
                "Owner": 13,
                "Locked": false,
                "Comments": "[]",
                "Creator": 13,
                "Updator": 13,
                "CreatedTime": "2023-09-27T10:41:00",
                "ItemTitle": "営業支援ツールの追加機能開発",
                "ApiVersion": 1.1,
                "ClassHash": {
                    "ClassA": "700",
                    "ClassB": "システム開発",
                    "ClassC": "90%"
                },
                "NumHash": {
                    "NumA": 540000.0,
                    "NumB": 440000.0,
                    "NumC": 100000.0,
                    "NumD": 18.5
                },
                "DateHash": {},
                "DescriptionHash": {},
                "CheckHash": {},
                "AttachmentsHash": {
                    "AttachmentsA": []
                }
            },
            {
                "SiteId": 620,
                "UpdatedTime": "2023-09-26T16:56:00",
                "IssueId": 705,
                "Ver": 1,
                "Title": "グループウェアのクラウド環境への移行",
                "Body": "ハードウェアの老朽化に伴いグループウェアをクラウド環境に移行します。\r\n新バージョンのデータへ のコンバートが必要となるためI社の技術コンサルを使います。\r\n\r\n",
                "StartTime": "2023-09-29T00:00:00",
                "CompletionTime": "2023-10-27T00:00:00",
                "WorkValue": 0.0,
                "ProgressRate": 0.0,
                "RemainingWorkValue": 0.0,
                "Status": 150,
                "Manager": 9,
                "Owner": 9,
                "Locked": false,
                "Comments": "[]",
                "Creator": 9,
                "Updator": 9,
                "CreatedTime": "2023-09-26T16:56:00",
                "ItemTitle": "グループウェアのクラウド環境への移行",
                "ApiVersion": 1.1,
                "ClassHash": {
                    "ClassA": "703",
                    "ClassB": "システム開発",
                    "ClassC": "90%"
                },
                "NumHash": {
                    "NumA": 4200000.0,
                    "NumB": 0.0,
                    "NumC": 4200000.0,
                    "NumD": 100.0
                },
                "DateHash": {},
                "DescriptionHash": {},
                "CheckHash": {},
                "AttachmentsHash": {
                    "AttachmentsA": []
                }
            },
            {
                "SiteId": 620,
                "UpdatedTime": "2023-09-26T09:22:00",
                "IssueId": 706,
                "Ver": 1,
                "Title": "食品工場内の環境モニタリングシステムの開発",
                "Body": "関東6拠点の食品工場に温度、湿度を計測するセンサーを配置し状態の変化をモニタリングするシステムを開発したいとの依頼がありました。\r\nセンサーはarduinoで実装し、構内のWiFi経由でデータセンターに接続する方式を提案します 。\r\nモニタリングや分析のためのシステムはD社パッケージをカスタマイズして導入する方式を提案します。\r\n",
                "StartTime": "2023-10-02T00:00:00",
                "CompletionTime": "2023-10-13T00:00:00",
                "WorkValue": 0.0,
                "ProgressRate": 0.0,
                "RemainingWorkValue": 0.0,
                "Status": 200,
                "Manager": 10,
                "Owner": 10,
                "Locked": false,
                "Comments": "[]",
                "Creator": 10,
                "Updator": 10,
                "CreatedTime": "2023-09-26T09:22:00",
                "ItemTitle": "食品工場内の環境モニタリングシステムの開発",
                "ApiVersion": 1.1,
                "ClassHash": {
                    "ClassA": "697",
                    "ClassB": "システム開発",
                    "ClassC": "50%"
                },
                "NumHash": {
                    "NumA": 4500000.0,
                    "NumB": 3207000.0,
                    "NumC": 1293000.0,
                    "NumD": 28.7
                },
                "DateHash": {},
                "DescriptionHash": {},
                "CheckHash": {},
                "AttachmentsHash": {
                    "AttachmentsA": []
                }
            }
        ]
    }
}
```

</details>

## ②レスポンスの形式を表示名に変更した場合

送信するデータのViewの中で ApiDataType プロパティを指定することでレスポンスの形式を表示名で返却するように変更できます。ApiDataType プロパティの詳細については以下マニュアルを参照してください。
[開発者ガイド：JSONデータレイアウト：View ](../../developers-guide/json-data-layout/api-view/index.md)

<details markdown="1">
<summary>サンプルコード (Python)</summary>
<br>
Viewの中にApiDataType プロパティと関連するApiColumnKeyDisplayType、ApiColumnValueDisplayTypeプロパティを追加して、レスポンスの各項目のKeyをカラム名(ColumnName)、Valueを表示名(DisplayValue)として返却するようにしております。
<br>

```
import requests
import json

# サイトIDを指定
site_id = 620

# APIキーを指定
api_key = "xxxxx..."

# APIのURLを指定
url = f"http://localhost/api/items/{site_id}/get"

# 送信するデータを指定
data = {
    "ApiVersion": 1.1,
    "ApiKey": api_key,
    "View": {
        "ApiDataType": "KeyValues",
        "ColumnFilterHash": {
            "ClassB": "[\"システム開発\"]"
        },
        "ApiColumnKeyDisplayType": "ColumnName",
        "ApiColumnValueDisplayType": "DisplayValue"
    }
}

# POSTリクエストを送信
response = requests.post(url, json=data)

# レスポンスを処理
if response.status_code == 200:
    response_data = json.loads(response.content)
    print(json.dumps(response_data, indent=4, ensure_ascii=False))
else:
    print(f"ErrorCode: {response.status_code}")
    print(response.text)
```

</details>

<details markdown="1">
<summary>レスポンス</summary>
<br>
上記のレスポンスとは異なり、顧客(ClassA)がレコードIDではなく、表示名で返却されています。
<br>

```
{
    "StatusCode": 200,
    "Response": {
        "Offset": 0,
        "PageSize": 200,
        "TotalCount": 3,
        "Data": [
            {
                "IssueId": 709,
                "ClassA": "情報共有イノベーション研究所",
                "TitleBody": "営業支援ツールの追加機能開発\n５年前よりスクラッチで開発していた人事システムに、残業管理機能の追加を行います。\r\n本システムの開発当初から担当しているR社に発注し開発を行います。",
                "Comments": null,
                "ClassB": "システム開発",
                "CompletionTime": "2023-10-29T00:00:00",
                "Status": "交渉",
                "ClassC": "90%",
                "NumA": 540000.0,
                "NumB": 440000.0,
                "NumC": 100000.0,
                "NumD": 18.5,
                "Manager": "山本 陽子",
                "Owner": "山本 陽子",
                "Updator": "山本 陽子",
                "UpdatedTime": "2023-09-27T10:41:00",
                "Title": "営業支援ツールの追加機能開発"
            },
            {
                "IssueId": 705,
                "ClassA": "株式会社プリザンター",
                "TitleBody": "グループウェアのクラウド環境への移行\nハードウェアの老朽化に伴いグループウェアをクラウド環境に移行します。\r\n新バージョンのデータへのコンバートが必要となるためI社の技術コンサルを使います。\r\n\r\n",
                "Comments": null,
                "ClassB": "システム開発",
                "CompletionTime": "2023-10-27T00:00:00",
                "Status": "提案",
                "ClassC": "90%",
                "NumA": 4200000.0,
                "NumB": 0.0,
                "NumC": 4200000.0,
                "NumD": 100.0,
                "Manager": "Brown Emily",
                "Owner": "Brown Emily",
                "Updator": "Brown Emily",
                "UpdatedTime": "2023-09-26T16:56:00",
                "Title": "グループウェアのクラウド環境への移行"
            },
            {
                "IssueId": 706,
                "ClassA": "株式会社オープンソーステクノロジー",
                "TitleBody": "食品工場内の環境モニタリングシステムの開発\n関東6拠点の食品工場に温度、湿度を計測するセン サーを配置し状態の変化をモニタリングするシステムを開発したいとの依頼がありました。\r\nセンサーはarduinoで実装し、構内のWiFi経由でデータセンターに接続する方式を提案します。\r\nモニタリングや分析のためのシステムはD社パッケージをカスタマイズして導入する方式を提案します。\r\n",
                "Comments": null,
                "ClassB": "システム開発",
                "CompletionTime": "2023-10-13T00:00:00",
                "Status": "交渉",
                "ClassC": "50%",
                "NumA": 4500000.0,
                "NumB": 3207000.0,
                "NumC": 1293000.0,
                "NumD": 28.7,
                "Manager": "鈴木 洋一",
                "Owner": "鈴木 洋一",
                "Updator": "鈴木 洋一",
                "UpdatedTime": "2023-09-26T09:22:00",
                "Title": "食品工場内の環境モニタリングシステムの開発"
            }
        ]
    }
}
```

</details>

## 関連情報

-   [開発者ガイド：JSONデータレイアウト：View ](../../developers-guide/json-data-layout/api-view/index.md)

