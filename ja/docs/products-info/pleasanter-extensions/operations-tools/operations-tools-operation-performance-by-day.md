---
title: 性能状況：日別
category: 運用支援ツール
order: '4000'
status: ''
parts: ''
urlstring: operations-tools-operation-performance-by-day
translationKey: operations-tools-operation-performance-by-day
shortname: Pleasanter Extensions,Operations Tools,性能状況：日別
created: 2025-01-27
updated: 2025-02-14
---

## 概要

プリザンターの性能状況を日別で確認できる画面です。「Class」「Method」「HttpMethod」を指定してフィルタすることができます。明細情報は「年月日」の昇順で表示されます。また、明細情報の「年月日」のリンクをクリックすることにより、「運用レポート：性能状況：時間別」の画面に遷移することができます。  

![運用レポートの性能状況：日別画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/dcaeef3eba16404da95126cf9467573d.png)

| 表示種別 | 項目    | 説明                                                                      |
|------|-------|-------------------------------------------------------------------------|
| 表形式  | 年月日      | 年月日が表示されます。 |
| 表形式  | 処理時間合計(ms)      | 処理時間合計(ms)が表示されます。 |
| 表形式  | 処理時間最大(ms)      | 処理時間最大(ms)が表示されます。 |
| 表形式  | 処理時間平均(ms)      | 処理時間平均(ms)が表示されます。 |
| 表形式  | ログ件数      | ログ件数が表示されます。 |
| 表形式  | エラー件数 | SyslogsテーブルのErrMessageがNullでないレコードの件数が表示されます。0件でない場合は背景色が黄色、赤文字で表示されます。 |
| グラフ  | 全般    | 「運用レポート：全体（利用状況／性能状況）」で選択した対象年月で日別に集計された結果が折れ線グラフと棒グラフの組み合わせで表示されます。    |
