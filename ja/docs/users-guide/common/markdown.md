---
title: マークダウン
category: 共通機能
order: '4'
status: ''
parts: ''
urlstring: markdown
translationKey: markdown
shortname: マークダウン
created: 2019-04-29
updated: 2026-01-13
---

## 概要

マークダウン記法を使用して、テキストの装飾、書式付けを行えます。

マークダウン記法は、以下の場所で使用できます。

1. [内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
1. [説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
1. [コメント項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
1. 各画面の[ガイド](../site/site-guide.md)
1. [Wiki](../wiki/index.md)

## 制約事項

1. マークダウン内では、HTMLタグを使用できません。

## 操作手順

1. [内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[コメント項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)の詳細設定で、[スタイル](../../developers-guide/style/index.md)から「マークダウン」を選択してください。
1. 各項目の入力欄の1行目に以下の内容を入力してください。
   ```
   [md]
   ```
   入力しない場合には通常のテキストとして表示されます。
1. レコードの編集画面や一覧画面でレンダリング結果を確認できます。

![マークダウンで入力した内容がレンダリングされた表示例](https://pleasanter.org/files/images/ja/users-guide/common/assets/c74ca00ee261492ba942c2c4aaf6f3ce.png)

## 使用できるマークダウン記法

プリザンターで使用できるマークダウン記法は、以下のFAQを参照してください。

[FAQ：マークダウン記法を用いた記述方法を教えてほしい](../../FAQ/others/faq-markdown.md)

## プラグインの使用

本機能はプラグイン[marked.js](https://marked.js.org/)を使用しています。

## 関連情報

-   [テーブルの管理：項目：内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：説明](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：コメント](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [サイト機能：ガイドの設定](../site/site-guide.md)
-   [Wiki機能](../wiki/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [FAQ：マークダウン記法を用いた記述方法を教えてほしい](../../FAQ/others/faq-markdown.md)
-   [marked.js](https://marked.js.org/)