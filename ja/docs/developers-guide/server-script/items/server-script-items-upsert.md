---
title: items.Upsert
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-upsert
translationKey: server-script-items-upsert
shortname: items.Upsert
created: 2023-07-11
updated: 2026-07-14
---

## 概要

指定したサイトでキー項目に該当するレコードが存在する場合は更新し、存在しない場合は新規作成します。

## 制限事項

1. 作成・更新したレコードのIDを、items.Upsertの戻り値や、items.Upsertで使用する変数からは取得できません。

## 構文

```
items.Upsert(siteId, json)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|siteId|object|○|サイトIDを指定|
|json|string|○|JSON文字列を指定。後述の「キー項目」の他に指定できる内容は[JSONデータレイアウト：共通](../../json-data-layout/api-common.md)、[JSONデータレイアウト：Item](../../json-data-layout/api-item.md)を参照してください|

#### 指定するキー項目について

指定したキー項目をもとにAPIによるレコード作成・更新(upsert)を行います。キー項目の指定は以下のパラメータで指定します。

|プロパティ名|データ型|説明|
|:--|:--|:--|
|Keys|配列(文字列)|キーとなる項目を指定。複数の項目を指定可能です。|

Keysに指定した項目の値がNULLの場合、キー項目としての比較はされず、レコードが新規作成されます。

## 戻り値

レコードを更新または、新規作成ができた場合は true、できなかった場合は false を返却します。

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. 2テーブル間でデータを同期管理する。</summary>

2つのテーブルで同じ情報を常に1対1で対応させたい場合、片方のテーブルで更新が発生したタイミングで、もう片方へ内容を同期（転記）します。  

このとき転記先テーブルには、対応元レコードを識別できるように**「元レコードID（外部キー）」を保存する項目**を用意します。

Upsert では、この外部キー項目を Keys に指定することで、

-   既に同じ外部キーを持つレコードがあれば 更新
-   存在しなければ 新規作成

を自動で判定できます。これにより、「存在チェック → あれば更新 / なければ作成」の分岐ロジックを書かずに、2テーブル間の1対1同期をシンプルに実装できます。

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
// 1対1同期のための「外部キー」
// ※転記元レコード(ResultId)を転記先テーブルの ClassB に保存し、UpsertのKeysに指定する
const sourceId = model.ResultId;
// リクエストを生成
const data = {
    Keys: ['ClassB'], // 外部キー項目（この値で更新/新規を判定）
    Title: model.Title,
    Status: model.Status,
    ClassHash: {
        ClassA: model.ClassA,
        ClassB: sourceId, // 外部キー（転記元ID）
    },
};
// レコードを作成/更新
const result = items.Upsert(site.SiteId, JSON.stringify(data));
if (result) {
    logs.LogInfo(`Upsert成功（外部キー=${sourceId}）`);
} else {
    logs.LogUserError(`Upsert失敗（外部キー=${sourceId}）`);
}
```

##### 実行結果

```
(Info):Upsert成功（外部キー=6830）
```

</details>

<details markdown="1">
<summary>2. 祝日データを定期的に取り込む</summary>

祝日APIは、すべての祝日データを毎回返す仕様のため、単純に登録すると同じ日付の祝日が重複して作成されてしまいます。

本サンプルでは、祝日の日付を一意なキーとして扱い、Upsert の Keys に日付項目（DateA）を指定しています。

これにより、

-   同じ日付のレコードが存在する場合は更新
-   存在しない場合は新規作成

が自動で判定され、祝日APIを何度実行しても差分のみを安全に反映できます。

##### JavaScript

```
// 祝日カレンダーサイト名
const siteName = '【サイト名】';
// 祝日APIから祝日データを取得する
const getNationalHolidays = () => {
    try {
        // 祝日APIへのHTTPリクエスト
        httpClient.RequestUri =
            'https://holidays-jp.github.io/api/v1/date.json';
        const response = httpClient.Get();
        if (httpClient.IsSuccess) {
            return JSON.parse(response);
        } else {
            logs.LogInfo(
                `祝日API取得エラー: (${httpClient.StatusCode}) ${response}`
            );
            return null;
        }
    } catch (e) {
        logs.LogInfo(`祝日API取得例外: ${e}`);
        return null;
    }
};
// 祝日レコード作成
const upsertHolidayRecord = (date, name, siteId) => {
    try {
        const data = {
            Keys: ['DateA'], // 祝日の日付を一意キーとして Upsert 判定
            ClassHash: { ClassA: name },
            DateHash: { DateA: date },
        };
        return items.Upsert(siteId, JSON.stringify(data));
    } catch (e) {
        logs.LogInfo(`祝日レコード作成例外: ${e}`);
        return false;
    }
};
// メイン処理
const nationalHolidays = getNationalHolidays();
if (!nationalHolidays) {
    logs.LogInfo('祝日データ取得失敗');
    return false;
}
const site = items.GetClosestSite(siteName);
if (!site) {
    logs.LogInfo(`${siteName} サイト情報取得失敗`);
    return false;
}
// 祝日データをもとにレコードを作成/更新
for (const date in nationalHolidays) {
    const result = upsertHolidayRecord(
        date,
        nationalHolidays[date],
        site.SiteId
    );
    if (result) {
        logs.LogInfo(
            `祝日レコード作成/更新成功: ${date} ${nationalHolidays[date]}`
        );
    } else {
        logs.LogInfo(
            `祝日レコード作成/更新失敗: ${date} ${nationalHolidays[date]}`
        );
    }
}
```

##### 実行結果

```
(Info):祝日レコード作成/更新成功: 2024-01-01 元日
(Info):祝日レコード作成/更新成功: 2024-01-08 成人の日
(Info):祝日レコード作成/更新成功: 2024-02-11 建国記念の日
(Info):祝日レコード作成/更新成功: 2024-02-12 建国記念の日 振替休日
(Info):祝日レコード作成/更新成功: 2024-02-23 天皇誕生日
(Info):祝日レコード作成/更新成功: 2024-03-20 春分の日
(Info):祝日レコード作成/更新成功: 2024-04-29 昭和の日
(Info):祝日レコード作成/更新成功: 2024-05-03 憲法記念日
(Info):祝日レコード作成/更新成功: 2024-05-04 みどりの日
(Info):祝日レコード作成/更新成功: 2024-05-05 こどもの日
(Info):祝日レコード作成/更新成功: 2024-05-06 こどもの日 振替休日
・・・・
```

</details>

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [itemsオブジェクト](index.md)
-   [開発者ガイド：API：テーブル操作：レコード作成・更新](../../api/table-operations/api-record-upsert.md)  