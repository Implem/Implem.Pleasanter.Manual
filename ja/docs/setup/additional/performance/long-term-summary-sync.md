---
title: サマリ同期処理によるサーバ負荷を軽減する
category: 追加設定：パフォーマンス
order: '300'
status: ''
parts: ''
urlstring: long-term-summary-sync
translationKey: long-term-summary-sync
shortname: サマリ同期処理によるサーバ負荷を軽減する
created: 2026-05-28
updated: 2026-06-09
---

## 概要

大量のレコードを含むテーブルで「サマリ同期」を実行する場合、データベースが高負荷状態で処理時間が長時間に及ぶ場合があります。本機能はサマリ同期処理を一定件数ごとに区切り、区切りごとに待機時間を設けることで、データベースの高負荷を抑えることができます。

設定は[SummarySync.json](../../parameters/summarysync-json.md)パラメータファイルで行います。既定値は待機なし（SynchronizeSummariesDelayMillisecondsが0）であり、既存環境の挙動は変わりません。

## 注意事項

1. 待機時間（SynchronizeSummariesDelayMilliseconds）を大きく設定するほど、同期処理全体の完了時間が長くなり、HTTPタイムアウトが発生するリスクが高まります。リバースプロキシやロードバランサ側のタイムアウト設定との整合性を確認してください。
1. パラメータファイルの変更を反映するには、アプリケーションの再起動が必要です。

## 制限事項

1. 本設定はサマリ同期処理にのみ適用されます。ファイルインポート・一括削除・一括更新などの処理には適用されません。
1. 最適な設定値はサーバの性能・負荷状況に依存します。以下の設定例はあくまでも目安です。

## 大量データを一括操作する処理の同時実行の抑止機能との関連性

[大量データを一括操作する処理の同時実行の抑止機能](block-site-task-while-running.md)を有効にしたうえで本機能を設定すると、サマリ同期が終了するまでの時間（ロック時間）が自動的に延長します。

## 操作手順

### 設定例1：区切り処理のみ有効（待機なし）

同時実行の抑止機能が有効に設定した場合は、SynchronizeSummariesDelayChunkSizeを設定することで、サマリ同期処理が終了するまでロック時間が自動的に延長されます。

```json
{
    "SynchronizeSummariesDelayMilliseconds": 0,
    "SynchronizeSummariesDelayChunkSize": 100
}
```

100件ごとにロック時間が延長され、サマリ同期処理が終了するまでロックが継続されます。

### 設定例2：軽度の負荷抑制

処理時間の増加を最小限に抑えながら、データベース負荷を軽減する場合の設定です。

```json
{
    "SynchronizeSummariesDelayMilliseconds": 50,
    "SynchronizeSummariesDelayChunkSize": 100
}
```

100件ごとに50ミリ秒の待機が挿入されます。1万件の処理では約5秒の追加時間が発生します。

### 設定例3：中程度の負荷抑制

データベース負荷を適度に抑制する場合の設定です。

```json
{
    "SynchronizeSummariesDelayMilliseconds": 200,
    "SynchronizeSummariesDelayChunkSize": 100
}
```

100件ごとに200ミリ秒の待機が挿入されます。1万件の処理では約20秒の追加時間が発生します。

### 設定例4：強度の負荷抑制

データベース負荷を最大限に抑制する場合の設定です。  
HTTPタイムアウトのリスクに注意してください。

```json
{
    "SynchronizeSummariesDelayMilliseconds": 500,
    "SynchronizeSummariesDelayChunkSize": 50
}
```

50件ごとに500ミリ秒の待機が挿入されます。1万件の処理では約100秒の追加時間が発生します。

### データ件数別の推奨設定

下記はあくまでも目安です。実際のサーバ性能や負荷状況に応じて調整してください。

| データ件数  | SynchronizeSummariesDelayChunkSize | SynchronizeSummariesDelayMilliseconds |
| :---------- | ---------------------------------: | ------------------------------------: |
| 1,000件未満 | 100                                | 0                                     |
| 1万〜10万件 | 500                                | 1000                                  |
| 10万件以上  | 1000                               | 2000                                  |

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.5.0以降    | 機能追加 |

## 関連情報

-   [同一テーブルに対して大量データを一括操作する処理の同時実行を抑止する](block-site-task-while-running.md)
