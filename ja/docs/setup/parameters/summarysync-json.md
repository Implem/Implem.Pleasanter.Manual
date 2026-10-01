---
title: SummarySync.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: summarysync-json
translationKey: summarysync-json
shortname: SummarySync.json
created: 2026-05-28
updated: 2026-06-09
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。

| パラメータ名                          | 設定例 | 説明                                                                                                                                                                                                                         |
| :------------------------------------ | :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SynchronizeSummariesDelayMilliseconds | 0      | サマリ同期処理における区切りごとの待機時間（ミリ秒）を指定します。<br><br>0<br>待機なしで処理が継続されます（既定値）。<br><br>1以上の値<br>指定した件数ごとに処理が一時停止され、指定した時間（ミリ秒）だけ待機します。 |
| SynchronizeSummariesDelayChunkSize    | 100    | サマリ同期処理を何件ごとに区切るかを指定します。既定値は100です。<br><br>0<br>区切り処理が無効になります。 <br><br>1以上の値<br>指定した件数ごとに処理が区切られ、[大量データを一括操作する処理の同時実行の抑止機能によるロック時間](../additional/performance/block-site-task-while-running.md)が延長されます。|

## 対応バージョン

| 対応バージョン | 内容                                                                                                      |
| :------------- | :-------------------------------------------------------------------------------------------------------- |
| 1.5.5.0以降    | 以下のパラメータを追加<br>・SynchronizeSummariesDelayMilliseconds<br>・SynchronizeSummariesDelayChunkSize |

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
