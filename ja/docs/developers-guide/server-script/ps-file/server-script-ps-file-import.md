---
title: "$ps.file.import"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-import
translationKey: server-script-ps-file-import
shortname: $ps.file.import
created: 2025-01-27
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用してインポートをする際に使用します。

## 前提条件

1. [Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。
2. [テーブル](../../../users-guide/table/index.md)の「インポート権限」が必要です。

## 構文

```
$ps.file.import(section, path, siteId, json);
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ファイル名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|
|siteId|string|○|サイトID|
|json|string|○|インポート用パラメータ|

## 戻り値

成功した場合に新規登録数と更新数を返します。失敗した場合はnullを返します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内のcsvファイルのインポートを行い、結果をログに出力します。

##### JavaScript

```
const siteId = 100;
const param = {
};
const result = $ps.file.import('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log($ps.JSON.stringify(result));
```

##### 出力例

```
{insertCount:10,updateCount:0}
```

文字コード：Shift-JIS の例
```
const siteId = 100;
const param = {
    Encoding: 'Shift-JIS'
};
const result = $ps.file.import('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log($ps.JSON.stringify(result));
```

##### 出力例

```
{insertCount:10,updateCount:0}
```

キーが一致するレコードを更新 の例
```
const siteId = 100;
const param = {
    UpdatableImport: true,
    Key: 'ClassA'
};
const result = $ps.file.import('01_develop', 'parts/01_parts.csv', siteId, $ps.JSON.stringify(param));
context.Log($ps.JSON.stringify(result));
```

##### 出力例

```
{insertCount:10,updateCount:10}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

??? note "1. 任意のフォルダに格納されたCSVファイルをインポートする"

    任意のフォルダに格納されたCSVファイルをインポートするサンプルコードです。

    以下処理イメージです。
    ![receivedフォルダのCSVファイルをPleasanterへインポートし、処理後にbackup/receivedへ移動する処理イメージ](https://pleasanter.org/files/images/ja/developers-guide/server-script/ps-file/assets/a43ae748c8954326ba349a691285b946.png)
    ①receivedフォルダに格納されているCSVファイルをPleasanterへインポート  
    ②処理後、backup/receivedへ移動

    ##### JavaScript
    ```javascript
    const SECTION = 'files';
    const RECEIVED = 'received';
    const BACKUP_RECEIVED = 'backup/received';
    const SITE_NAME = '【サイト名】';
    // サイト情報取得
    const site = items.GetClosestSite(SITE_NAME);
    if (!site) {
        logs.LogException(`サイト：${SITE_NAME}が見つかりません。`);
        return false;
    }
    const siteId = site.SiteId;
    // 受信フォルダのファイルを読み込み、インポートする
    const param = {};
    const lists = $ps.file.getFileList(SECTION, RECEIVED);
    if (lists.length > 0) {
        for (const element of lists) {
            const result = $ps.file.import(
                SECTION,
                `${RECEIVED}/${element}`,
                siteId,
                $ps.JSON.stringify(param),
            );
            if (!result) {
                logs.LogException(
                    `インポートに失敗しました。 ファイル名：${element}`,
                );
                return false;
            } else {
                logs.LogInfo(
                    `インポート成功 ファイル名：${element} 結果：${$ps.JSON.stringify(
                        result,
                    )}`,
                );
            }
        }
        // インポート完了後、ファイルをバックアップファイルに移動
        for (const element of lists) {
            const moveResult = $ps.file.moveFile(
                SECTION,
                `${RECEIVED}/${element}`,
                `${BACKUP_RECEIVED}/${element}`,
            );
            if (!moveResult) {
                logs.LogException(`ファイル移動失敗 ファイル名：${element}`);
                return false;
            } else {
                logs.LogInfo(`ファイル移動成功 ファイル名：${element}`);
            }
        }
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

