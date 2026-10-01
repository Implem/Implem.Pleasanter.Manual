---
title: 移動
category: 移動
order: '0'
status: ''
parts: ''
urlstring: table-management-move
translationKey: table-management-move
shortname: 移動先の設定
created: 2019-12-05
updated: 2025-03-11
---

## 概要

「レコード」の[移動](../../../users-guide/table/record-authoring/edit-records/table-record-move.md)機能を使用する際の移動先のテーブルを事前に設定することができます。

## 制限事項

1. 「期限付きテーブル」の場合には「記録テーブル」を設定できません。
1. 「記録テーブル」の場合には「期限付きテーブル」を設定できません。

## 前提条件

1. 設定の操作には、移動元サイトの管理権限と移動先サイトの参照権限が必要です。

## 操作手順

1. 移動元の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [移動](../../../users-guide/table/record-authoring/edit-records/table-record-move.md)タブを開いてください。
1. [選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)の検索欄に追加するサイトのIDまたはタイトルを入力します。
1. [検索](../search/index.md)ボタンをクリックすると検索条件と一致するサイトが表示されます。※1 ※2 ※3 ※4
1. [選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)のリストから対象の[テーブル](../../../users-guide/table/index.md)を選択してください。
1. 「有効化」ボタンをクリックしてください。
1. 「有効化」した[テーブル](../../../users-guide/table/index.md)が「現在の設定」の一番下に追加されるので「上」、「下」ボタンを使用して、表示する位置を調整してください。Ctrlキーを押しながら「上」、「下」ボタンをクリックすると[項目](../editor/editor-settings/columns/index.md)が最上段、最下段に移動します。
1. 不要な[テーブル](../../../users-guide/table/index.md)は「現在の設定」から選択して「無効化」ボタンをクリックしてください。
1. 画面下部の「更新」ボタンをクリックしてください。

※1 移動先サイトの検索はバージョン1.4.14.0以降で実行可能です。バージョン1.4.13.0以前では初期表示時に同じ種別の全サイトが表示されます。
※2 IDが検索キーワードと部分一致する全サイトと、タイトルが検索キーワードと部分一致する全サイトが表示されます。種別が一致しないサイトは表示されません。また、検索キーワードの複数指定はできません。  
※3 検索キーワードに「％」または空欄を指定すると全サイトが表示されます。  
※4 検索欄でEnterキーを押下した場合もサイトの検索を実行できます。

## 動作イメージ

![テーブルの管理の「移動」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/move/assets/34cc98ed9f644f67b1378bb9eedc0f13.png)
レコードを別のテーブルへ移動するための機能です。  
**同じ種別**で作成されたテーブルにレコードを移動することができます。  
対象レコードのあるテーブルが「期限付きテーブル」だった場合、移動先も「期限付きテーブル」である必要があります。

![「移動」タブで移動先のテーブルを設定した状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/move/assets/dbbf6bfdced74ec5afed88c5554beef8.png)

「移動先の設定」に有効化されたテーブルがある場合、レコードの編集画面に[移動](../../../users-guide/table/record-authoring/edit-records/table-record-move.md)ボタンが表示されます。  
※移動元および移動先のサイトの更新権限が必要です。

![レコードの編集画面に表示された「移動」ボタン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/move/assets/07577bf1410f466aa7d6d7dd2ab085da.png)

また、一覧画面に[一括移動](../../../users-guide/table/record-authoring/edit-records/table-record-bulkmove.md)ボタンが表示されます。  
※移動元および移動先のサイトの更新権限が必要です。

![一覧画面に表示された「一括移動」ボタン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/move/assets/dff696e4824d4e76bf4e6eea8333f183.png)

一覧画面では、各行左端のチェックをつけた行が移動の対象となります。
「移動設定」ダイアログでは有効化されたテーブルを「移動先」から選択します。

![「移動設定」ダイアログ。「移動先」からテーブルを選ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/move/assets/7e749df8bab44511a601de3a81c4a105.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.14.0 以降|移動先の設定に検索機能を追加|

## 関連情報

-   [テーブル機能：レコードの移動](../../../users-guide/table/record-authoring/edit-records/table-record-move.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：検索](../search/index.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [テーブル機能：レコードの一括移動](../../../users-guide/table/record-authoring/edit-records/table-record-bulkmove.md)