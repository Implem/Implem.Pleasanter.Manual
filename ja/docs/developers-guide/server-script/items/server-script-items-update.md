---
title: items.Update
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-update
translationKey: server-script-items-update
shortname: items.Update
created: 2021-01-27
updated: 2026-08-06
---

## 概要

指定したレコードを更新します。

## 構文

```
items.Update(recordId, data)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|recordId|object|○|対象レコードのレコードIDを指定|
|data|string|○|更新内容をJSON形式で指定。指定内容は[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)、[JSONデータレイアウト：Item](../../json-data-layout/api-item.md)を参照してください|

## 戻り値

レコードを更新できたらtrue、更新できなかったらfalseを返却します。

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. レコードIDを直接指定し更新</summary>

レコードIDを直接指定し更新します。

##### JavaScript

```
// レコードIDを指定しレコードを更新
const recordId = 【レコードID】;
const data = {
    Title: 'タイトル変更',
    ClassHash: {
        ClassA: '障害',
    },
};
const result = items.Update(recordId, JSON.stringify(data));
if (result) {
    logs.LogInfo(`更新成功`);
} else {
    logs.LogUserError(`更新失敗`);
}
```

##### 実行結果

```
(Info):更新成功
```

</details>

<details markdown="1">
<summary>2. 複数のレコードを更新</summary>

条件に該当するレコードを取得し、該当するレコード複数件を更新します。

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
// 状況が未着手(100)のデータを抽出対象とする
const status_codes = `["100"]`;
const data = {
    View: {
        ColumnFilterHash: {
            Status: `${status_codes}`,
        },
    },
};
const results = Array.from(items.Get(site.SiteId, JSON.stringify(data)));
for (const item of results) {
    // 状況を保留(910)に更新
    const data = {
        Status: '910',
    };
    const result = items.Update(item.ResultId, JSON.stringify(data));
    if (result) {
        logs.LogInfo(`更新成功：Id=${item.ResultId}`);
    } else {
        logs.LogUserError(`更新失敗：Id=${item.ResultId}`);
    }
}
```

##### 実行結果

```
(Info):更新成功：Id=9999
(Info):更新成功：Id=9999
(Info):更新成功：Id=9999
```

</details>

<details markdown="1">
<summary>3. 添付ファイルを削除</summary>

特定のレコードに添付されている添付ファイルをすべて削除します。

##### JavaScript

```
// 処理対象のレコードID
const recordId = 【レコードID】;
// レコード取得
const results = Array.from(items.Get(recordId));
if (!results || results.length === 0) {
    logs.LogInfo(`レコードが見つかりませんでした: Id=${recordId}`);
    return;
}
// AttachmentsAを扱いやすい形にパース
const attachments = JSON.parse(
    $ps.JSON.stringify(results[0].AttachmentsA || [])
);
if (attachments.length === 0) {
    logs.LogInfo(`添付ファイルなしのため更新不要: Id=${recordId}`);
    return;
}
// すべての添付の Guid を指定、Deleted=1 にして更新する（添付を削除する）
const data = {
    AttachmentsHash: {
        AttachmentsA: attachments.map((attachment) => ({
            Guid: attachment.Guid,
            Deleted: 1,
        })),
    },
};
const result = items.Update(recordId, JSON.stringify(data));
if (result) {
    logs.LogInfo(
        `更新成功: Id=${recordId}, 削除対象=${attachments.length}件`
    );
} else {
    logs.LogUserError(`更新失敗: Id=${recordId}`);
}
```

##### 実行結果

```
(Info):更新成功: Id=9999, 削除対象=3件
```

</details>

<details markdown="1">
<summary>4. レコードのアクセス制御を設定</summary>

特定のレコードにレコードのアクセス制御を設定します。

##### JavaScript

```
// 処理対象のレコードID
const recordId = 【レコードID】;
// グループID=1に対して管理者権限をレコードのアクセス制御に付与する
const data = {
    RecordPermissions: ['Group,1,511'],
};
const result = items.Update(recordId, JSON.stringify(data));
if (result) {
    logs.LogInfo(`更新成功: Id=${recordId}`);
} else {
    logs.LogUserError(`更新失敗: Id=${recordId}`);
}
```

##### 実行結果

```
(Info):更新成功：Id=9999
```

</details>

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [itemsオブジェクト](index.md)