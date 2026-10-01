---
title: apiModel.Delete
icon: material/alpha-m-box
category: サーバスクリプト
order: '20000'
status: ''
parts: ''
urlstring: server-script-api-model-delete
translationKey: server-script-api-model-delete
shortname: apiModel.Delete
created: 2021-01-22
updated: 2026-01-26
---

## 概要

既存レコードを削除します。

## 構文

```
apiModel.Delete()
```

## 戻り値

レコードを削除できたらtrue、削除できなかったらfalseを返却します。

## 使用例

以下の例ではレコードIDが123のレコードを削除します。

##### JavaScript

```
let records = items.Get(123);
if (records.Length === 1) {
    let record = records[0];
    record.Delete();
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. 任意の条件に合致するレコードを削除する</summary>

状況が’910’のレコードを取得し削除します。

##### JavaScript

```js
// 状況が保留(910)のデータを抽出対象とする
const targetStatus = '910';
// 処理対象のサイト名を指定
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
const data = {
    View: {
        ColumnFilterHash: {
            Status: `[\"${targetStatus}\"]`,
        },
    },
};
const results = items.Get(site.SiteId, JSON.stringify(data));
// 抽出した結果を削除
for (const item of results) {
    const result = item.Delete();
    if (result) {
        logs.LogInfo(`削除成功：Id=${item.ResultId}`);
    } else {
        logs.LogUserError(`削除失敗：Id=${item.ResultId}`);
    }
}
```

##### 実行結果

```
(Info):削除成功：Id=9001
(Info):削除成功：Id=9002
(Info):削除成功：Id=9003
(Info):削除成功：Id=9004
(Info):削除成功：Id=9005
```

</details>

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](../items/index.md)  
-   [apiModelオブジェクト](index.md)