---
title: 同一テーブルに対して大量データを一括操作する処理の同時実行を抑止する
category: 追加設定：パフォーマンス
order: '400'
status: ''
parts: ''
urlstring: block-site-task-while-running
translationKey: block-site-task-while-running
shortname: 大量データを一括操作する処理の同時実行の抑止機能
created: 2026-05-31
updated: 2026-08-14
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/b694d13a7f5846889b4a037c9c4b880f.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/e90159cc1f514d9c9c73f8b4236bac14.svg#only-dark)](https://pleasanter.org/support/)

## 概要

1つのテーブルに対してインポートや一括更新など大量のデータを一括操作する処理を同時に実行すると、データベースが高負荷状態になり処理時間が非常に長くなることでシステム全体のパフォーマンスが悪化する場合があります。本機能では1つのテーブルに対して大量データを一括操作する処理の同時実行を抑止することでシステム全体のパフォーマンスを安定化することができます。

設定は[General.json](../../parameters/general.json.md)のパラメータ「BlockSiteTaskWhileRunning」で行います。trueに設定することで本機能を有効にします。

## 注意事項

1. パラメータファイルの変更を反映するには、アプリケーションの再起動が必要です。

## 制限事項

1. 本機能は同一テーブルに対する同時実行を抑止する機能です。別テーブルに対する同時実行は抑止しません。
1. 旧プラン（ミニ、ライト、スタンダード、プレミアム）契約者は対象外です。

## 動作仕様

### 対象となるサイト

本機能の対象となるサイトは「期限付きテーブル」「記録テーブル」です。

### 対象となる操作

本機能の対象となる操作は以下の通りです。同じテーブルに対して同時に実行しようとすると、あとから実行したほうがブロックされます。

|実行種類| 操作の種類 | 説明 |
|---|---|---|
|画面| 「[一括更新](../../../users-guide/table/record-authoring/edit-records/table-record-bulkupdate.md)」 | 一覧画面で複数レコードをまとめて更新する |
|画面| 「[一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)」 | 一覧画面で複数レコードをまとめて削除する |
|画面| 「[インポート](../../../users-guide/table/record-authoring/create-records/table-record-import.md)」 | 一覧画面でCSVファイルからデータを取り込む |
|画面| 「[サマリ](../../../managers-guide/manage-table/summaries/index.md)」同期 | 「[テーブルの管理](../../../managers-guide/manage-table/index.md)」－「サマリ」タブで選択したサマリを再計算する |
|API| 「一括作成・更新API」 | APIで複数レコードをまとめて作成または更新する |
|API| 「一括削除API」 | APIで複数レコードをまとめて削除する |
|API| 「インポートAPI」 | APIでCSVファイルからデータを取り込む |
|API| 「エクスポートAPI」 | APIでデータをファイル出力する |
|API| 「サマリ同期API」| APIでサマリを再計算する |
|スクリプト| 「$p.apiBulkDelete」 | スクリプトで複数レコードをまとめて削除する |
|サーバスクリプト| [items.BulkDelete](../../../developers-guide/server-script/items/server-script-items-bulk-delete.md) | サーバスクリプトで複数レコードをまとめて削除する |
|サーバスクリプト| [$ps.file.import](../../../developers-guide/server-script/ps-file/server-script-ps-file-import.md) | サーバスクリプトでCSVファイルからデータを取り込む |
|サーバスクリプト| [$ps.file.export](../../../developers-guide/server-script/ps-file/server-script-ps-file-export.md) | サーバスクリプトでデータをファイル出力する |

## 動作の仕組み

![同一テーブルへの一括操作の同時実行が抑止される仕組みを示す図](https://pleasanter.org/files/images/ja/setup/additional/performance/assets/421e4edb689a47aab98c5b360524facd.png)

- 先に実行した処理が終わると、ロックは自動的に解除されます
- 処理が途中で止まった場合でも、**120秒後に自動的にロックが解除**されます（次の操作が詰まったままになりません）

### エラーメッセージ

本機能でブロックされた場合、以下のエラーメッセージが表示または返却されます。

#### 画面操作

画面下部に「別のタスクが処理中です。後で実行してください。」のエラーメッセージが表示されます。

#### API、スクリプト

APIのレスポンスとして **HTTPステータスコード：429** が返却されます。

```json
{
  "statusCode": 429,
  "message": "別のタスクが処理中です。後で実行してください。"
}
```

#### サーバスクリプト

1. items.BulkDelete
0が返却されます。

1. $ps.file.import
画面下部に「別のタスクが処理中です。後で実行してください。」のエラーメッセージが表示されます。

1. $ps.file.export
画面下部に「別のタスクが処理中です。後で実行してください。」のエラーメッセージが表示されます。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.4.12.0以降    | 機能追加 |
