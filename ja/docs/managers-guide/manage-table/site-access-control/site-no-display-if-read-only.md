---
title: 読取専用の場合は画面に表示しない
category: アクセス制御
order: '400'
status: ''
parts: ''
urlstring: site-no-display-if-read-only
translationKey: site-no-display-if-read-only
shortname: 読み取り専用の場合は画面に表示しない
created: 2021-05-31
updated: 2025-09-16
---

## 概要

[サイト](../../../users-guide/site/index.md)の「読み取り権限」のみを有するユーザに対し、「サイトメニュー」、[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)、[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)の使用を禁止する場合にオンにします。[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)機能からの参照など、マスタテーブルとしてのみの利用を許可する場合に使用できます。オンにした場合[サイト](../../../users-guide/site/index.md)が非表示となり、直接URLを要求した場合でもアクセス不能となります。「読み取り権限」以外の権限を有するユーザはアクセス可能です。

![「読取専用の場合は画面に表示しない」のチェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/site-access-control/assets/695326551e5341269ff1527ccf98765d.png)

## 前提条件

1. 「サイトの管理権限」と「権限の管理権限」が必要です。

## 操作手順

1. 各サイトを開き、ナビゲーションメニューより「管理」-「〇〇の管理」をクリックしてください。
1. [サイトのアクセス制御](index.md)タブを選択してください。
1. 「読取専用の場合は画面に表示しない」をオンにしてください。
1. コマンドボタンエリアにある「更新」ボタンをクリックしてください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.27.0 以降|機能追加|

## 関連情報

-   [サイト機能](../../../users-guide/site/index.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [サイトのアクセス制御](index.md)
