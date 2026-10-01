---
title: items.Delete
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-delete
translationKey: server-script-items-delete
shortname: items.Delete
created: 2021-01-27
updated: 2026-01-15
---

## 概要

指定したレコードを削除します。

## 構文

```
Delete(recordId)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|recordId|object|○|対象レコードのIDを指定|

## 戻り値

レコードを削除できた場合はtrue、削除できなかった場合はfalseを返却します。

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. レコードIDを指定して削除する</summary>

状況が’910’のレコードを取得、取得できたIDでレコードを削除します。

##### JavaScript

```
// 処理対象のサイト名を指定
const siteName = '【サイト名】';
// サイト情報を取得
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
// 状況が保留(910)のデータを削除対象とする
const status_codes = `["910"]`;
const data = {
    View: {
        ColumnFilterHash: {
            Status: `${status_codes}`,
        },
    },
};
const results = Array.from(items.Get(site.SiteId, JSON.stringify(data)));
if (results.length === 0) {
    logs.LogInfo('削除対象データなし');
    return;
}
// 取得した保留(910)のデータを削除する
for (const item of results) {
    const result = items.Delete(item.ResultId);
    if (result) {
        logs.LogInfo(`削除成功：Id=${item.ResultId}`);
    } else {
        logs.LogUserError(`削除失敗：Id=${item.ResultId}`);
    }
}
```

##### 実行結果

```
(Info):削除成功：Id=9999
(Info):削除成功：Id=9999
(Info):削除成功：Id=9999
```

</details>

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)