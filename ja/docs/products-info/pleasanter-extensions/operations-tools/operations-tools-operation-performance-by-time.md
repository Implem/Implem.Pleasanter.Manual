---
title: 性能状況：時間別
category: 運用支援ツール
order: '5000'
status: ''
parts: ''
urlstring: operations-tools-operation-performance-by-time
translationKey: operations-tools-operation-performance-by-time
shortname: Pleasanter Extensions,Operations Tools,性能状況：時間別
created: 2025-01-27
updated: 2025-02-14
---

## 概要

プリザンターの性能状況を時間別（15分単位）で確認できる画面です。明細情報は「時間」の昇順で表示されます。「Class」「Method」「HttpMethod」を指定してフィルタすることができます。  

![運用レポートの性能状況：時間別画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/a33a3a5e0a8246609e25ceb956d7d6e8.png)

| 表示種別 | 項目    | 説明                                                                      |
|------|-------|-------------------------------------------------------------------------|
| 表形式  | 年月日      | 年月日が表示されます。 |
| 表形式  | 時間      | 時間が表示されます。 |
| 表形式  | 処理時間合計(ms)      | 処理時間合計(ms)が表示されます。 |
| 表形式  | 処理時間最大(ms)      | 処理時間最大(ms)が表示されます。 |
| 表形式  | 処理時間平均(ms)      | 処理時間平均(ms)が表示されます。 |
| 表形式  | ログ件数      | ログ件数が表示されます。 |
| 表形式  | エラー件数 | SyslogsテーブルのErrMessageがNullでないレコードの件数が表示されます。0件でない場合は背景色が黄色、赤文字で表示されます。 |
| グラフ  | 全般    | 「運用レポート：性能状況：日別」で選択した対象日で時間別に集計された結果が折れ線グラフと棒グラフの組み合わせで表示されます。          |
