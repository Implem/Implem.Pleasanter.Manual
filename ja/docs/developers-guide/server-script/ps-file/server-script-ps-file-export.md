---
title: "$ps.file.export"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-export
translationKey: server-script-ps-file-export
shortname: $ps.file.export
created: 2025-01-27
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用してエクスポートをする際に使用します。

## 前提条件

1. [Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。
2. [テーブル](../../../users-guide/table/index.md)の「エクスポート権限」が必要です。

## 構文

```
$ps.file.export(section, path, siteId, json);
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ファイル名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|
|siteId|string|○|サイトID|
|json|string|○|エクスポート用パラメータ|

## 戻り値

成功した場合にtrueを返します。失敗した場合はfalseを返します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内のcsvファイルのエクスポートを行い、結果をログに出力します。

### (a) 標準のエクスポート設定でテーブルをエクスポートする。

##### JavaScript

```
const siteId = 100;
const param = {
};
const result = $ps.file.export('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log(result);
```

### (b) 文字コード：Shift-JIS の例

##### JavaScript

```
const siteId = 100;
const param = {
    Encoding = "Shift-JIS"
};
const result = $ps.file.export('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log(result);
```

### (c) Pleasanterで作成済みの[エクスポート](../../api/table-operations/api-export.md)設定を使用してテーブルをエクスポートする

##### JavaScript

```
const siteId = 100;
const param = {
    ExportId: 1
};
const result = $ps.file.export('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log(result);
```

### (e) 直接記述してテーブルをエクスポートする

##### JavaScript

```
const siteId = 100;
const param = {
    Export: {
        Columns: [
            {
                ColumnName: 'ClassA'
            },
            {
                ColumnName: 'UpdatedTime'
            }
        ],
        Header: false,
        Type: 'csv'
    }
};
const result = $ps.file.export('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log(result);
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

??? note "1. 任意のフォルダにテーブルのデータをエクスポートする"

    任意のフォルダにテーブルのデータをエクスポートするサンプルコードです。

    以下処理イメージです。
    ![前回エクスポートしたCSVファイルをbackup/sendへ移動し、エクスポートしたCSVファイルをsendフォルダへ格納する処理イメージ](https://pleasanter.org/files/images/ja/developers-guide/server-script/ps-file/assets/464e338fc1e2435096f4ccf9af85b359.png)
    ①sendフォルダに格納されている前回エクスポートしたCSVファイルをbackup/sendへ移動
    ②エクスポートしたCSVファイルをsendフォルダへ格納

    ##### JavaScript
    ```javascript
    // 各種設定
    const SECTION = 'files';
    const SEND = 'send';
    const BACKUP_SEND = 'backup/send';
    const SITE_NAME = '【サイト名】';
    const FILE_DATE_FORMAT = 'utilities';
    // 処理日時の文字列取得
    function getDateTimeString() {
        return new Date()
            .toLocaleString('ja-JP', {
                year: 'numeric',
                month: '2-digit',
                day: '2-digit',
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit',
                hour12: false, // 24時間表示
            })
            .replaceAll('/', '')
            .replaceAll(':', '')
            .replaceAll(' ', '');
    }
    // サイト情報取得
    const site = items.GetClosestSite(SITE_NAME);
    if (!site) {
        logs.LogException(`サイト：${SITE_NAME}が見つかりません。`);
        return false;
    }
    const siteId = site.SiteId;
    // 送信フォルダにあるファイルをバックアップフォルダに移動
    const lists = $ps.file.getFileList(SECTION, SEND);
    if (lists.length > 0) {
        for (const element of lists) {
            const moveResult = $ps.file.moveFile(
                SECTION,
                `${SEND}/${element}`,
                `${BACKUP_SEND}/${element}`,
            );
            if (!moveResult) {
                logs.LogException(`ファイル移動失敗 ファイル名：${element}`);
                return false;
            } else {
                logs.LogInfo(`ファイル移動成功 ファイル名：${element}`);
            }
        }
    }
    // ファイルエクスポート：エクスポート定義のID：1を使用。対象レコードは「対象月が今年」のレコード
    const param = {
        ExportId: 1,
        View: {
            ColumnFilterHash: {
                DateA: '["ThisYear"]',
            },
        },
    };
    const path = `${SEND}/${FILE_DATE_FORMAT}${getDateTimeString()}.csv`;
    const exportResult = $ps.file.export(
        SECTION,
        path,
        siteId,
        $ps.JSON.stringify(param),
    );
    if (!exportResult) {
        logs.LogException(`エクスポートに失敗しました。 ファイル名：${path}`);
        return false;
    } else {
        logs.LogInfo(`エクスポート成功 ファイル名：${path}`);
    }
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.13.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [開発者ガイド：API：テーブル操作：テーブルのエクスポート](../../api/table-operations/api-export.md)

