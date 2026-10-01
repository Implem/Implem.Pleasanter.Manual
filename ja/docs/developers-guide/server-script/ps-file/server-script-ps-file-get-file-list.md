---
title: "$ps.file.getFileList"
icon: material/alpha-m-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file-get-file-list
translationKey: server-script-ps-file-get-file-list
shortname: $ps.file.getFileList
created: 2024-12-23
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)で[$ps.file](index.md)を使用して指定ディレクトリ内のファイル名一覧を取得します。

## 前提条件

[Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileを false に設定することが必要です。

## 構文

```
$ps.file.getFileList(section, path)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|section|string|○|セクション名。セクションについては[$ps.file](index.md)の「セクションについて」を参照ください。|
|path|string|○|ディレクトリ名。ディレクトリの区切り文字はWindow、Linux共に「/」を利用する。|

## 戻り値

ファイル名文字列の配列を返却します。

## 例外

C#内で例外が発生した場合はサーバスクリプト内に例外クラス名とエラーメッセージをErrorオブジェクトに入れて例外を発生させます。

## 使用例

以下の例では、Webサーバ内の指定ディレクトリ内のファイル名一覧を取得し、結果をログに出力します。

##### JavaScript

```
const lists = $ps.file.getFileList('test_data','parts');
context.Log('listCnt='+lists.length);
for (const element of lists) {
	context.Log('list='+element);
}
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

??? note "2. 任意のフォルダにテーブルのデータをエクスポートする"

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
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：$ps.file](index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)

