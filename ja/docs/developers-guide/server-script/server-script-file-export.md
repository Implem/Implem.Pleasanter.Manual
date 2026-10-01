---
title: サーバスクリプトによるファイルエクスポートサンプル
category: サーバスクリプト
order: '0'
status: ''
parts: '1'
urlstring: server-script-file-export
translationKey: server-script-file-export
shortname: ''
created: 2026-02-03
updated: 2026-03-17
---

任意のフォルダにテーブルのデータをエクスポートするサンプルコードです。

以下処理イメージです。
![ファイルエクスポートの処理の流れを示す図](https://pleasanter.org/files/images/ja/developers-guide/server-script/assets/464e338fc1e2435096f4ccf9af85b359.png)
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