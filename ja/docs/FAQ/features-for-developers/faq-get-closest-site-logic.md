---
title: サイト名検索で該当サイトに最も近いサイトID取得の検索順が知りたい。
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-get-closest-site-logic
translationKey: faq-get-closest-site-logic
shortname: サイト名検索
created: 2024-06-06
updated: 2024-06-11
---

## 回答

[サイト名検索](../../developers-guide/api/site-operations/api-site-get-closest-siteid.md)で該当サイトを検索する順序は以下の通りです。
1. サイトが検索対象サイトか否か
2. 同階層に検索対象サイトが存在するか
3. 同階層のフォルダ内に検索対象サイトが存在するか
4. １つ上の階層に検索対象サイトが存在するか
5. １つ上の階層のフォルダ内に検索対象サイトが存在するか

---

## 概要

[サイト名検索](../../developers-guide/api/site-operations/api-site-get-closest-siteid.md)APIやスクリプト、サーバスクリプトではサイト名で該当サイトの検索を行います。本ページでは検索する順序について説明します。
なお、プリザンターでは複数のサイトで同一の名称を設定することができますが、[サイト名検索](../../developers-guide/api/site-operations/api-site-get-closest-siteid.md)機能では同一サイト名のサイトが複数存在する場合は、使用者が望むサイトが検索されない可能性があります。[サイト名検索](../../developers-guide/api/site-operations/api-site-get-closest-siteid.md)を使用する場合はサイト名を重複しないように運用してください。

## 制限事項

1. サイト名が同名のサイトが同一階層に複数あった場合はどちらが検索されるか不定となるため、期待するサイトが検索されない可能性があります。

## 前提条件

1. [サイト名検索](../../developers-guide/api/site-operations/api-site-get-closest-siteid.md)機能はサイトの「サイト名」を検索します。あらかじめサイト名を設定してください。サイトの[タイトル](../../managers-guide/tenant-administration/tenant-logo.md)ではありませんので注意ください。
![サイトの設定画面。検索の対象となる「サイト名」の欄がある](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/be2492d00d0c4ee0b48cd62f3356ac73.png)

## 検索の順序

※）以下の説明内では言うサイトとは、フォルダ・期限付きテーブル・記録テーブル・Wiki・ダッシュボードの総称を指します。
1. 自サイトが検索サイト名の場合は自サイトのIDを返す。
1. 自サイトと同じ階層のサイト一覧から検索サイト名が見つかった場合はそのサイトのIDを返す。
1. 自サイトと同じ階層でフォルダがある場合はそのフォルダ内を深さ優先で検索を行い、検索サイト名が見つかった場合がそのサイトのIDを返す。
1. 「3」で自サイト以下に該当サイトが無い場合は自サイトより一階層上に遷移し、一階層上のサイト一覧から検索サイト名が見つかった場合はそのサイトのIDを返す
1. 以降、同様に2-4の処理を自サイトを現在サイトと読み替えて繰り返し検索処理を続け、検索サイト名が見つかった場合はそのサイトのIDを返す
1. 全てのサイトを探索して見つからない場合は-1を返す。

### 検索例

   ![検索例で使うサイトの階層構造を示した図](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/205f662252414537be993153b45a29fc.png)

|起点サイト(No)|検索サイト名|検索結果サイトNo|備考|
|:--------|:---|---:|:----------------------|
|課題管理(7)|課題管理|7|自サイトである|
|新規テーブル１(8)|課題管理|7|同階層にある|
|新規テーブル１(8)|商談|11|同階層にない→自階層の下階層(9)にある|
|新規テーブル１(8)|WBS|3|同階層にない→自階層の下階層(9)にない→自階層の上階層(2)にある|
|新規テーブル１(8)|店舗一覧|15|同階層にない→自階層の下階層にない→自階層の上階層(2)にない→上階層(2)の下階層(14)にある|

## 関連情報

-   [開発者ガイド：API：サイト操作：サイト名検索で該当サイトに最も近いサイトID取得](../../developers-guide/api/site-operations/api-site-get-closest-siteid.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../managers-guide/tenant-administration/tenant-logo.md)