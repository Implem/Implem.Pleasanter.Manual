---
title: items.Create
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-create
translationKey: server-script-items-create
shortname: items.Create
created: 2021-01-27
updated: 2026-03-10
---

## 概要

指定したサイトIDのテーブルにレコードを作成します。

-   構文①：オブジェクトを指定する方法 > 使用例①
-   構文②：JSON文字列を指定する方法 > 使用例②、使用例③

## 制限事項

作成したレコードのIDを、items.Createの戻り値から取得することはできません。

-   構文①で記述すると、作成したレコードのIDを取得できます。> 使用例①
-   構文②で記述すると、作成したレコードのIDを取得できません。> 使用例②、使用例③

## 構文①

```
items.Create(siteId, model)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|siteId|object|○|対象テーブルのサイトIDを指定|
|model|object|○|items.NewSite,items.NewIssue,Items.Resultメソッドで取得したapiModelオブジェクトを指定|

## 戻り値

レコードを作成できたらtrue、作成できなかったらfalseを返却します。
作成したレコード内容はレコードIDを含めmodelに反映されます。

## 構文②

```
items.Create(siteId, json)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|siteId|object|○|対象テーブルのサイトIDを指定|
|json|string|○|JSON文字列を指定。指定内容は[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)、[JSONデータレイアウト：Item](../../json-data-layout/api-item.md)を参照してください|

## 戻り値

レコードを作成できたらtrue、作成できなかったらfalseを返却します。

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. 構文①でレコード作成</summary>

構文①でレコードを新規作成します。

##### JavaScript

```
// サイト名を指定しレコードを1件作成
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
let apiModel = items.NewResult();
apiModel.Title = 'サンプル案件_P1';
apiModel.Status = 200;
apiModel.ClassA = '問い合わせ';
apiModel.DateA = '2025/01/10';
apiModel.NumA = 5;
items.Create(site.SiteId, apiModel);
// ブラウザのコンソールに作成したレコードのIDを出力
logs.LogInfo(apiModel.ResultId);
```

##### 実行結果

```
(Info):9999
```

</details>
<details markdown="1">
<summary>2. 構文②でレコード作成</summary>

構文②でレコードを新規作成します。

##### JavaScript

```
// サイト名を指定しレコードを1件作成
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
const data = {
    ApiVersion: 1.1,
    Title: 'サンプル案件_P1',
    Status: 200,
    ClassHash: { ClassA: '問い合わせ' },
    DateHash: { DateA: '2025/1/10' },
    NumHash: { NumA: 5 },
};
const result = items.Create(site.SiteId, JSON.stringify(data));
if (result) {
    logs.LogInfo('レコード作成成功');
} else {
    logs.LogInfo('レコード作成失敗');
}
```

##### 実行結果

```
(Info):レコード作成成功
```

</details>
<details markdown="1">
<summary>3. CSVファイルを読み込み複数件レコード作成</summary>

CSVを読み込み、複数件のレコードを作成します。

##### CSV(projects_data.csv)

```
サンプル案件E,900,改善要望,10,9,2025/1/20,2025/2/10,仕様確定しリリース済
サンプル案件D,900,問い合わせ,2,2,2025/1/15,2025/1/18,クローズ済
サンプル案件C,200,障害,4,2,2025/1/12,2025/1/13,一時回避済、本対応検討中
サンプル案件B,100,改善要望,16,0,2025/1/11,2025/1/31,次期リリース候補
```

##### JavaScript

```
// サイト名を指定
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
// セクションとファイルパスを指定し、CSVファイルを読み込み
const section = 'files';
const path = 'projects_data.csv';
const file = $ps.file.readAllText(section, path);
// CSV文字列を配列に変換
const csvRec = $ps.CSV.str2csv(file);
// 配列の各行をレコードとして作成
for (const rec of csvRec) {
    let apiModel = items.NewResult();
    apiModel.Title = rec[0];
    apiModel.Status = rec[1];
    apiModel.ClassA = rec[2];
    apiModel.NumA = rec[3];
    apiModel.NumB = rec[4];
    apiModel.DateA = rec[5];
    apiModel.DateB = rec[6];
    apiModel.DescriptionA = rec[7];
    items.Create(site.SiteId, apiModel);
    // ブラウザのコンソールに作成したレコードのIDを出力
    logs.LogInfo(`レコード作成しました/${apiModel.ResultId}`);
}
```

##### 実行結果

```
(Info):レコード作成しました/9999
(Info):レコード作成しました/9999
(Info):レコード作成しました/9999
・・・
```

</details>

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)  
-   [itemsオブジェクト：NewSiteメソッド](server-script-items-new-site.md)
-   [itemsオブジェクト：NewIssueメソッド](server-script-items-new-issue.md)
-   [itemsオブジェクト：NewResultメソッド](server-script-items-new-result.md)
-   [apiModelオブジェクト](../apiModel/index.md)
-   [$ps.fileオブジェクト](../ps-file/index.md)
-   [$ps.fileオブジェクト：readAllTextメソッド](../ps-file/server-script-ps-file-read-all-text.md)