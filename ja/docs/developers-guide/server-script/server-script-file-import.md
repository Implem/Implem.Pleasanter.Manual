---
title: サーバスクリプトによるファイルインポートサンプル
category: サーバスクリプト
order: '0'
status: ''
parts: '1'
urlstring: server-script-file-import
translationKey: server-script-file-import
shortname: ''
created: 2026-02-03
updated: 2026-03-17
---

任意のフォルダに格納されたCSVファイルをインポートするサンプルコードです。

以下処理イメージです。
![ファイルインポートの処理の流れを示す図](https://pleasanter.org/files/images/ja/developers-guide/server-script/assets/a43ae748c8954326ba349a691285b946.png)
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