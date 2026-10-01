---
title: 基本項目
category: 項目
order: '100'
status: ''
parts: ''
urlstring: table-management-column
translationKey: table-management-column
shortname: 基本項目
ee_notice: columns
created: 2021-05-10
updated: 2025-10-24
---

## 概要

**基本項目**は、テーブルの作成時点で有効化されている[項目](index.md)です。「基本項目」は「期限付きテーブル」と「記録テーブル」とで異なります。

基本項目以外には、[分類項目](table-management-class.md)、[数値項目](table-management-num.md)、[日付項目](table-management-date.md)、[説明項目](table-management-description.md)、[チェック項目](table-management-check.md)、[添付ファイル項目](table-management-attachments.md)があります。これらと基本項目の[ロック項目](table-management-lock.md)を使うには、有効化が必要です。操作方法は[エディタの設定](../index.md)をご覧ください。

### 基本項目の一覧表

以下に、基本項目をまとめます。✓は各テーブルで設定可能な項目であることを意味します。

|項目名|内容|期限付きテーブル|記録テーブル|
|:--|:--|:-:|:-:|
|[ID項目](table-management-id.md)| レコードの一意なID | ✓ | ✓ |
|[バージョン項目](table-management-ver.md)| レコードのバージョン番号 | ✓ | ✓ |
|[タイトル項目](table-management-title.md)| レコードを識別するための文字列 | ✓ | ✓ |
|[内容項目](table-management-body.md)|レコードの内容を示す文字列 | ✓ | ✓ |
|[開始項目](table-management-start-time.md)|作業の開始を示す日時 |✓| |
|[完了項目](table-management-completion-time.md)|作業の期限を示す日時 |✓| |
|[作業量項目](table-management-work-value.md)|	作業の量を示す数値 |✓| |
|[進捗率項目](table-management-progress-rate.md)|	作業の進捗率（0～100%）を示す数値|✓||
|[残作業量項目](table-management-remaining-work-value.md)|作業量と進捗率から自動計算される数値|✓||
|[状況項目](table-management-status.md)|作業の状況（ステータス）を示す数値|✓|✓|
|[管理者項目](table-management-manager.md)|	作業の管理者であるユーザ|✓|✓|
|[担当者項目](table-management-owner.md)|	作業の担当者であるユーザ|✓|✓|
|[ロック項目](table-management-lock.md)|	レコードへの書き込み禁止スイッチ|✓|✓|
|[コメント項目](table-management-comments.md)|レコードに対するコメントを示すフリーテキスト|✓|✓|
|[作成者項目](table-management-creator.md)|	レコードの作成者であるユーザ|✓	|✓|
|[更新者項目](table-management-updator.md)|	レコードの更新者であるユーザ|✓	|✓|
|[作成日時項目](table-management-created-time.md)|レコードの作成日時|✓|✓|
|[更新日時項目](table-management-updated-time.md)|レコードの更新日時|✓|✓|

上記の表で、「項目名」列のリンクをクリックすると、各項目の詳細を確認できます。

## 操作方法

### 1. レコードの編集画面で使う項目を有効化する

詳細は[エディタの設定](../index.md)をご覧ください。

### 2. 一覧画面で使う項目を有効化する

詳細は[一覧画面の項目の設定](../../../grid/table-management-grid-columns.md)をご覧ください。

## 関連情報

-   [テーブルの管理：項目](index.md)
-   [テーブルの管理：項目：分類](table-management-class.md)
-   [テーブルの管理：項目：数値](table-management-num.md)
-   [テーブルの管理：項目：日付](table-management-date.md)
-   [テーブルの管理：項目：説明](table-management-description.md)
-   [テーブルの管理：項目：チェック](table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](table-management-attachments.md)
-   [テーブルの管理：項目：ロック](table-management-lock.md)
-   [テーブルの管理：エディタ：エディタの設定](../index.md)
-   [テーブルの管理：項目：ID](table-management-id.md)
-   [テーブルの管理：項目：バージョン](table-management-ver.md)
-   [テーブルの管理：項目：タイトル](table-management-title.md)
-   [テーブルの管理：項目：内容](table-management-body.md)
-   [テーブルの管理：項目：開始](table-management-start-time.md)
-   [テーブルの管理：項目：完了](table-management-completion-time.md)
-   [テーブルの管理：項目：作業量](table-management-work-value.md)
-   [テーブルの管理：項目：進捗率](table-management-progress-rate.md)
-   [テーブルの管理：項目：残作業量](table-management-remaining-work-value.md)
-   [テーブルの管理：項目：状況](table-management-status.md)
-   [テーブルの管理：項目：管理者](table-management-manager.md)
-   [テーブルの管理：項目：担当者](table-management-owner.md)
-   [テーブルの管理：項目：コメント](table-management-comments.md)
-   [テーブルの管理：項目：作成者](table-management-creator.md)
-   [テーブルの管理：項目：更新者](table-management-updator.md)
-   [テーブルの管理：項目：作成日時](table-management-created-time.md)
-   [テーブルの管理：項目：更新日時](table-management-updated-time.md)
-   [テーブルの管理：一覧画面：一覧画面の項目の設定](../../../grid/table-management-grid-columns.md)
-   [Contact](https://implem.co.jp/contact)
