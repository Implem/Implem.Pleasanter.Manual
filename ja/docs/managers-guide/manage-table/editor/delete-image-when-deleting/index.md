---
title: 削除時に画像を削除
category: エディタ
order: '24000'
status: ''
parts: ''
urlstring: table-management-delete-image-when-deleting
translationKey: table-management-delete-image-when-deleting
shortname: 削除時に画像を削除
created: 2022-06-21
updated: 2025-01-30
---

## 概要

レコードの削除時に画像を削除しないように設定します。

## 制限事項

1.  フルテキストを利用するため、対象項目のエディタ設定で[フルテキストの種類](../editor-settings/advanced-settings/general/table-management-full-text-type.md)が「無し」の場合はチェックをオフにしても機能しません。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1.  対象の[テーブル](../../../../users-guide/table/index.md)を開いてください。
1.  「管理」メニューから[テーブルの管理](../../index.md)をクリックしてください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  画面下部にある「削除時に画像を削除」のチェックボックスをオフにしてください。
1.  画面下部の「更新」ボタンをクリックしてください。

## 動作イメージ

項目に画像登録があるレコードをコピー後、コピー元のレコードを削除した場合、コピー先レコードの表示は以下のイメージとなります。

-   「削除時に画像を削除」のチェックがオンの場合

    ![「削除時に画像を削除」がオンのとき、コピー元削除後のコピー先レコード](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/delete-image-when-deleting/assets/9d4c4e80c93f45d896eb2f276816b5c5.png)

-   「削除時に画像を削除」のチェックがオフの場合

    ![「削除時に画像を削除」がオフのとき、コピー元削除後のコピー先レコード](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/delete-image-when-deleting/assets/2a944fcd4adf4551abf6a249dc058f48.png)

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../editor-settings/advanced-settings/general/table-management-full-text-type.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理](../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
