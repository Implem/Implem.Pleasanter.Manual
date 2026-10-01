---
title: items.Get
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-get
translationKey: server-script-items-get
shortname: items.Get
created: 2021-01-27
updated: 2026-03-10
---

## 概要

[itemsオブジェクト](index.md)の「Getメソッド」です。指定したレコードまたは、指定したテーブルのレコードを情報を取得します。[サイト統合](../../../users-guide/table/record-authoring/edit-records/table-site-integration.md)を設定しているテーブルの場合は、統合された各レコードの情報もあわせて取得します。

## 制限事項

1. 取得できるレコードの件数は Api.json の PageSize(デフォルトで 200) が最大となります。200件以上のレコードを取得する場合は、[FAQ：APIで200レコードを超えるデータを取得したい](../../../FAQ/features-for-developers/faq-api-paging.md)を参照してください。

## 構文

```
items.Get(id, data)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|id|object|○|サイトID、レコードIDを指定|
|data|string|-|選択するレコードのフィルタやソート等をJSON形式で指定。指定内容は[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)、[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)を参照してください|

## 戻り値

該当するレコードの[apiModel](../apiModel/server-script-api-model-create.md)の配列を返却します。

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. レコードIDを指定して取得する</summary>

レコードIDを指定して取得します。

##### JavaScript

```
// レコードIDを指定し1件取得
const recordId = 【レコードID】;
const results = items.Get(recordId);
logs.LogInfo(`${results[0].Title} ${results[0].ClassA}`);
```

##### 実行結果

```
(Info):サンプル案件E 改善要望
```

</details>

<details markdown="1">
<summary>2. サイトIDを指定しレコード全件取得する</summary>

サイトIDを指定し、レコード全件します。

##### JavaScript

```
// サイト名を指定し全件取得
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
const results = items.Get(site.SiteId);
for (const item of results) {
    logs.LogInfo(`${item.Title} ${item.ClassA}`);
}
```

##### 実行結果

```
(Info):サンプル案件E 改善要望
(Info):サンプル案件D 問い合わせ
(Info):サンプル案件C 障害
(Info):サンプル案件B 改善要望
(Info):サンプル案件A 問い合わせ
```

</details>

<details markdown="1">
<summary>3. 日付の期間を指定しレコードを取得する</summary>

日付の期間を指定しレコードを取得します。

##### JavaScript

```
// サイト名と日付期間を指定し取得
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
// 取得対象の期間を指定する
const start = '2025/01/10';
const end = '2025/01/12';
const data = {
    View: {
        ColumnFilterHash: {
            DateA: `["${start} 00:00:00, ${end} 23:59:59"]`,
        },
        ColumnSorterHash: { DateA: 'asc' },
    },
};
const results = items.Get(site.SiteId, JSON.stringify(data));
for (const item of results) {
    logs.LogInfo(`${item.Title} ${item.ClassA} ${item.DateA}`);
}
```

##### 実行結果

```
(Info):サンプル案件A 問い合わせ Fri Jan 10 2025 00:00:00 GMT+0900 (日本標準時)
(Info):サンプル案件B 改善要望 Sat Jan 11 2025 00:00:00 GMT+0900 (日本標準時)
(Info):サンプル案件C 障害 Sun Jan 12 2025 00:00:00 GMT+0900 (日本標準時)
```

</details>

<details markdown="1">
<summary>4. ステータスコードを指定し取得する</summary>

ステータスを指定し取得します。

##### JavaScript

```
// サイト名とステータスコードを指定し取得
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
const status_codes = `["100","200"]`;
const data = {
    View: {
        ColumnFilterHash: {
            Status: `${status_codes}`,
        },
        ColumnSorterHash: { DateA: 'asc' },
    },
};
const results = items.Get(site.SiteId, JSON.stringify(data));
for (const item of results) {
    logs.LogInfo(`${item.Title} ${item.ClassA} ${item.Status}`);
}
```

##### 実行結果

```
(Info):サンプル案件A 問い合わせ 200
(Info):サンプル案件B 改善要望 100
(Info):サンプル案件C 障害 200
```

</details>

<details markdown="1">
<summary>5. 文字列で検索（部分一致）し取得する</summary>

文字列で検索（部分一致）し取得します。

##### JavaScript

```
// サイト名と文字列で検索（部分一致）し取得
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
const text = `リリース`;
const data = {
    View: {
        ColumnFilterHash: { DescriptionA: `${text}` },
        ColumnSorterHash: { DateA: 'asc' },
        ColumnFilterSearchTypes: { DescriptionA: 'PartialMatch' },
    },
};
const results = items.Get(site.SiteId, JSON.stringify(data));
for (const item of results) {
    logs.LogInfo(`${item.Title} ${item.ClassA} ${item.DescriptionA}`);
}
```

##### 実行結果

```
(Info):サンプル案件B 改善要望 次期リリース候補
(Info):サンプル案件E 改善要望 仕様確定しリリース済
```

</details>

<details markdown="1">
<summary>6. 200件を超えるレコードを取得する</summary>

200件を超えるレコードを取得します。

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
let offset = 0;
let totalCount = 0;
const allItems = [];
while (true) {
    const data = {
        Offset: offset,
    };
    // items.Get は第2引数に JSON 文字列を渡す
    const results = Array.from(
        items.Get(site.SiteId, JSON.stringify(data))
    );
    // 取得件数が 0 になったら終了
    if (!results || results.length === 0) {
        break;
    }
    // 今回分を配列に追加
    for (const item of results) {
        allItems.push(item);
    }
    // ログ出力
    logs.LogInfo(`Offset=${offset}, 取得件数=${results.length}`);
    totalCount += results.length;
    // Offset を「今回取得した件数ぶん」進める
    offset += results.length;
}
logs.LogInfo(`最終的な取得件数: ${totalCount} 件`);
// 取得した全レコードを処理
for (const item of allItems) {
    logs.LogInfo(`${item.Title} ${item.ClassA}`);
}
```

##### 実行結果

```
(Info):Offset=0, 取得件数=200
(Info):Offset=200, 取得件数=150
(Info):最終的な取得件数: 350 件
(Info):サンプル案件A 問い合わせ
(Info):サンプル案件B 改善要望
(Info):サンプル案件C 障害
(Info):サンプル案件D 問い合わせ
(Info):サンプル案件E 改善要望
・・・
```

</details>

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)
