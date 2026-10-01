---
title: apiModel.Update
icon: material/alpha-m-box
category: サーバスクリプト
order: '20000'
status: ''
parts: ''
urlstring: server-script-api-model-update
translationKey: server-script-api-model-update
shortname: apiModel
created: 2021-01-22
updated: 2026-01-26
---

## 概要

既存レコードを更新します。

## 構文

```
apiModel.Update()
```

## 戻り値

レコードを更新できたらtrue、更新できなかったらfalseを返却します。

## 使用例

下記の例では、レコードIDが 123 のレコード情報を取得し、[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を 完了(900) に更新します。

##### JavaScript

```
let records = items.Get(123);
if (records.Length === 1) {
    let record = records[0];
    record.Status = 900;
    record.Update();
}
```

##### コード内の【 ... 】 は適宜修正してください。

??? note "1. 任意の条件でレコードを取得し一括で任意の項目を更新する"

    状況が’100’のレコードを取得し、'200'に更新する。

    ##### JavaScript

    ```
    // 状況が未着手(100)のデータを抽出対象とする
    const targetStatus = '100';
    // 実施中(200)に更新する
    const updateStatus = '200';
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
    const results = Array.from(items.Get(site.SiteId, JSON.stringify(data)));
    // 抽出した結果に対し状況を更新
    for (const item of results) {
        item.Status = updateStatus;
        const result = item.Update();
        if (result) {
            logs.LogInfo(`更新成功：Id=${item.ResultId}`);
        } else {
            logs.LogUserError(`更新失敗：Id=${item.ResultId}`);
        }
    }
    ```

    ##### 実行結果

    ```
    (Info):更新成功：Id=9001
    (Info):更新成功：Id=9002
    ```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](../items/index.md)  
-   [apiModelオブジェクト](index.md)