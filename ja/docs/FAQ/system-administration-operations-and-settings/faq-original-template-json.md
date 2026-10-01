---
title: オリジナルのテンプレートを追加したい
category: FAQ：システム管理の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-original-template-json
translationKey: faq-original-template-json
shortname: ''
created: 2022-06-21
updated: 2025-01-30
---

## 回答

プリザンターのフォルダ内¥App_Data¥Definitions¥Definition_Templateに設定ファイル2つを格納し、プリザンターを再起動してください。

---

## 注意事項

本FAQはプリザンターのバージョン1.3.6.0以降の内容です。バージョン1.3.5.0以前をご利用の場合は以下FAQを参照ください。
[FAQ：オリジナルのテンプレートを追加したい（ver.1.3.5.0以前）](faq-original-template.md)

## 制限事項

1.  オリジナルテンプレートを登録するタブを新たに作成することはできません。既存のタブから選択してください。

## 概要

テーブルの新規作成で選択できるテンプレートとして独自に作成したオリジナルテンプレートを登録することができます。

## 操作方法

1.  テンプレートとして登録したいテーブルを新規作成します。作成後、そのサイトIDを記録しておいてください。
1.  SQLServer Management Studioなどを使ってImplem.Pleasanterのdbo.sitesテーブルを開き、SiteIdが1。で記録したサイトIDと一致するレコードを選択し、SiteSettingsカラムの内容をコピーしてください。この内容がオリジナルテンプレートの構成になります。

    ![SQL Server Management Studio で dbo.sites の SiteSettings をコピーするところ](https://pleasanter.org/files/images/ja/FAQ/system-administration-operations-and-settings/assets/cdb98aff949d4f6495ab71c72ca57785.png)

1.  プリザンターのフォルダ内¥App_Data¥Definitions¥Definition_Templateフォルダを開きます。
1.  オリジナルテンプレートを定義する以下2つのjsonファイルを作成します。作成内容は「オリジナルテンプレート定義ファイル」を参照ください。
1.  プリザンターを再起動してください。新規作成時、指定した場所に追加したテンプレートが追加されていることを確認してください。

    ![新規作成の画面。追加したテンプレートが表示されている](https://pleasanter.org/files/images/ja/FAQ/system-administration-operations-and-settings/assets/2c622c9256624860b8bea90138f1fa7e.png)

## オリジナルテンプレート定義ファイル

| No  | ファイル名                                   | 例                                    |
| :-- | :------------------------------------------- | :------------------------------------ |
| 1   | （テンプレートID）.json                      | Template999.json                      |
| 2   | （テンプレートID）_SiteSettingsTemplate.json | Template999_SiteSettingsTemplate.json |

### 1. （テンプレートID）.json

| No  | 設定項目              | 説明                                                                                                               |
| :-- | :-------------------- | :----------------------------------------------------------------------------------------------------------------- |
| 1   | Id                    | 他のテンプレートと重複しない任意の値を指定します。ここで指定した値がファイル名となる（テンプレートID）になります。 |
| 2   | Language              | 言語を指定します。                                                                                                 |
| 3   | Title                 | オリジナルのテンプレート名を指定します。                                                                           |
| 4   | Tags                  | タブの画面表示名 [^1] を指定します。                                                                               |
| 5   | タブの設定項目名 [^1] | タブ内に表示する順番（n番目）を数値で指定します。                                                                  |

[^1]: 以下の表から選択してください。

| No  | タブの画面表示名 | タブの設定項目名                |
| :-- | :--------------- | :------------------------------ |
| 1   | 標準             | Standard                        |
| 2   | プロジェクト     | Project                         |
| 3   | 営業             | Sales                           |
| 4   | 顧客・サービス   | Customer                        |
| 5   | 店舗・販売       | Store                           |
| 6   | マーケティング   | Marketing                       |
| 7   | 情報システム     | InformationSystem               |
| 8   | 経営企画         | CorporatePlanning               |
| 9   | 人事・総務       | HumanResourcesAndGeneralAffairs |
| 10  | 教育・人材開発   | Education                       |
| 11  | 商品一覧         | ProductList                     |
| 12  | 分類マスタ       | Classification                  |

### 設定例

``` json linenums="1"
{
    "Id": "Template999",
    "Language": "ja",
    "Title": "オリジナルテンプレ",
    "Tags": "プロジェクト",
    "Project": "11"
}
```

### 2. （テンプレートID）_SiteSettingsTemplate.json

手順2でコピーしたSiteSettingsカラムの内容を貼り付けてください。
