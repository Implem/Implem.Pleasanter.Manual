---
title: 一覧画面の列の幅を調整したい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-adjust-column-width
translationKey: faq-adjust-column-width
shortname: ''
created: 2019-09-12
updated: 2025-10-14
---

## 回答

バージョン1.4.20.0以降は[セルの横幅](../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)で設定可能です。それより前のバージョンは[スタイル](../../developers-guide/style/index.md)を使用します。

---

## 概要

バージョン1.4.20.0以降は[セルの横幅](../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)で設定可能です。それより前のバージョンは[スタイル](../../developers-guide/style/index.md)を使用します。

## 制限事項

バージョン1.4.20.0以降では、[スタイル](../../developers-guide/style/index.md)を使った変更よりも、[セルの横幅](../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)の変更が優先されます。

## [セルの横幅](../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)を使った操作手順（バージョン1.4.20.0以降）

1. 対象のテーブルを開きます。
1. 「管理」→[テーブルの管理](../../managers-guide/manage-table/index.md)をクリックします。
1. [一覧](../../managers-guide/manage-table/grid/index.md)タブをクリックします。
1. 現在の設定リストで、幅を調整したい項目をクリックし、リスト上部の詳細設定ボタンをクリックします。
1. セルの横幅にピクセル数を入力します。
1. 変更ボタンをクリックします。
1. コマンドボタンエリアの更新ボタンをクリックします。
1. 対象テーブルの一覧画面を開き、列の幅を確認します。

## [スタイル](../../developers-guide/style/index.md)を使った操作手順（バージョン1.4.20.0より前）

1. 対象のテーブルを開きます。
1. 「管理」→[テーブルの管理](../../managers-guide/manage-table/index.md)をクリックします。
1. [スタイル](../../developers-guide/style/index.md)タブを開きます。
1. 「＋新規作成」ボタンをクリックし、ダイアログを表示します。
1. タイトルに「一覧画面の列の幅を調整」等の任意のタイトルを入力します。
1. スタイルに列の幅を調整するスタイル（下記、スタイルの例をご覧ください）を入力します。
1. 出力先の「全て」のチェックを外し、[一覧](../../managers-guide/manage-table/grid/index.md)にチェックします。
1. ダイアログの追加ボタンをクリックします。
1. コマンドボタンエリアの更新ボタンをクリックします。
1. 対象のテーブルの一覧画面を開き、列の幅を確認します。

### スタイルの例（CSS）

```
table {
  table-layout: fixed;
  width: 80%;     /* 表全体の横幅を指定。ウィンドウ全体なら100% */
}

th[data-name="Title"]        {width: 35%;} /* タイトル列の横幅  */
th[data-name="ClassA"]       {width: 10%;} /* 分類A列の横幅     */
th[data-name="NumA"]         {width:  5%;} /* 数値A列の横幅     */
th[data-name="DateA"]        {width: 15%;} /* 日付A列の横幅     */
th[data-name="DescriptionA"] {width: 25%;} /* 説明A列の横幅     */
th[data-name="CheckA"]       {width:  5%;} /* チェックA列の横幅 */
```

## 関連情報

[テーブルの管理：一覧画面：項目の詳細設定：セルの横幅](../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)
