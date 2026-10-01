---
title: 日別
category: 運用支援ツール
order: '6000'
status: ''
parts: ''
urlstring: operations-tools-usage-by-day
translationKey: operations-tools-usage-by-day
shortname: Pleasanter Extensions,Operations Tools,利用状況詳細：日別
created: 2025-01-27
updated: 2025-02-14
---

## 概要

プリザンターの利用状況詳細を日別で確認できる画面です。「開始日」「終了日」を指定して最長１年間をフィルタすることができます。明細情報は「年月日」の昇順で表示されます。  

> **Note**  
> 「APIリクエスト件数」は[システムログの拡張機能](../../../managers-guide/system-log-administration/syslog-extension.md)を利用している場合のみ確認することができます。  
> 
> システムログの拡張機能 | Pleasanter  
> https://pleasanter.org/manual/syslog-extension  

![利用状況詳細の日別画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/ab7628afa26f4f23a89d108fd312d26f.png)

| 表示種別 | 項目         | 説明                                                          |
|------|------------|-------------------------------------------------------------|
| 表形式  | 全般         | 「開始日」「終了日」でフィルタした期間内または[利用状況詳細：月別](operations-tools-usage-by-month.md)で選択した対象年月の利用状況が日別で表示されます。 |
| 表形式  | 新規ユーザ数     | 「開始日」「終了日」でフィルタした期間内での新規登録されたユーザ数が表示されます。                   |
| 表形式  | アクティブユーザ数  | 「開始日」「終了日」でフィルタした期間内でのログインしたユーザ数が表示されます。                    |
| 表形式  | ログイン回数     | 「開始日」「終了日」でフィルタした期間内でのユーザのログイン回数が表示されます。                    |
| 表形式  | アクション回数    | 「開始日」「終了日」でフィルタした期間内でのすべてのアクション回数（Syslogsのレコード件数）が表示されます。   |
| 表形式  | メール送信件数    | 「開始日」「終了日」でフィルタした期間内でのメール送信件数が表示されます。                       |
| 表形式  | APIリクエスト件数 | 「開始日」「終了日」でフィルタした期間内でのAPIリクエスト件数が表示されます。                    |
| 表形式  | 新規レコード数    | 「開始日」「終了日」でフィルタした期間内での新規レコード数が表示されます。                       |
| 表形式  | 更新レコード数    | 「開始日」「終了日」でフィルタした期間内での更新レコード数が表示されます。                       |
| 表形式  | バイナリサイズ    | 「開始日」「終了日」でフィルタした期間内でのバイナリサイズ（添付ファイルや貼り付けた画像などのサイズ）が表示されます。 |
| 表形式  | 前日比率       | 前日に対しての増減が%形式で表示されます。                                       |

## 関連情報

-   [システムログの拡張機能](../../../managers-guide/system-log-administration/syslog-extension.md)
-   [Operations Tools：利用状況詳細：月別](operations-tools-usage-by-month.md)
