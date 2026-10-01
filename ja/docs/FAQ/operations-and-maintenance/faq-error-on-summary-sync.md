---
title: サマリ同期処理が終わらずエラーになる
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-error-on-summary-sync
translationKey: faq-error-on-summary-sync
shortname: ''
created: 2026-05-28
updated: 2026-05-28
---

## 回答

[SummarySync.json](../../setup/parameters/summarysync-json.md)のパラメータを調整し、サマリ同期処理を細かく区切ってください。

---

## 概要

大量のレコードを含むテーブルでサマリ同期を実行すると、処理時間が長時間に及び、WebサーバのHTTPタイムアウトを超過してエラーになることがあります。[SummarySync.json](../../setup/parameters/summarysync-json.md)のパラメータSynchronizeSummariesDelayChunkSizeの値を小さくして区切り単位を細かくするか、[SummarySync.json](../../setup/parameters/summarysync-json.md)のパラメータSynchronizeSummariesDelayMillisecondsを大きくして区切り間に待機時間を設けることで、処理の継続性を確保できます。

詳細な設定手順と推奨値は「[サマリ同期処理によるサーバ負荷を軽減する](../../setup/additional/performance/long-term-summary-sync.md)」を参照してください。

## 注意事項

1. 待機時間（SynchronizeSummariesDelayMilliseconds）を大きくするほど、同期処理全体の完了時間が長くなります。HTTPタイムアウトのリスクが高まるため、リバースプロキシ・ロードバランサ側のタイムアウト設定との整合性を確認してください。
1. パラメータファイルの変更を反映するには、アプリケーションの再起動が必要です。

## 制限事項

1. WebサーバのHTTPタイムアウトはサーバ側の設定に依存します。パラメータの調整で解消しない場合は、サーバの処理時間制限設定を確認してください。

## 操作手順

エラーが解消しない場合は、以下の順序で確認してください。

1. [SummarySync.json](../../setup/parameters/summarysync-json.md)を開いてください。
1. SynchronizeSummariesDelayChunkSize の値を小さくしてください。
1. SynchronizeSummariesDelayMilliseconds の値を大きくしてください。
1. アプリケーションを再起動してください。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.5.0以降    | 機能追加 |
