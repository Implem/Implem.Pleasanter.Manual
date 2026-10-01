---
title: 集計
category: 集計
order: '0'
status: ''
parts: ''
urlstring: table-management-aggregation
translationKey: table-management-aggregation
shortname: 集計
created: 2019-12-04
updated: 2024-06-03
---

## 概要

[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の上部にある「集計」欄に表示する[項目](../editor/editor-settings/columns/index.md)を設定します。[分類項目](../editor/editor-settings/columns/table-management-class.md)などを使用すると、分類ごとに「グループ化」して集計できます。

[一覧画面]: ../../../users-guide/table/record-authoring/data-analysis/table-grid.md
[項目]: ../editor/editor-settings/columns/index.md
[分類項目]: ../editor/editor-settings/columns/table-management-class.md

=== "デフォルトの一覧画面"

    ![集計を設定していないデフォルトの一覧画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/5e1a8130211944619e15aaf5d6f004c0.png)

=== "「担当者」を「追加」し、集計種別「件数」で集計"

    ![「担当者」を追加し集計種別に「件数」を設定した「集計」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/9613690c784d4a6db22ef7053533c10f.png)

=== "集計結果"

    ![一覧画面に表示された集計結果](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/67b42eb01bf94f64a832514f01549b23.png)

### チェック項目を追加した場合

集計項目として[チェック項目](../editor/editor-settings/columns/table-management-check.md)を「追加」した場合、「チェックなし」と「チェックあり」で集計します。下図の左側が「チェックなし」、右側が「チェックあり」の表示です。

[チェック項目]: ../editor/editor-settings/columns/table-management-check.md

![チェック項目の集計結果。左が「チェックなし」、右が「チェックあり」](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/4199390d9b674babb0098232827f5949.png)

## 制限事項

1.  「合計」、「平均」の集計には[作業量項目](../editor/editor-settings/columns/table-management-work-value.md)、[残作業量項目](../editor/editor-settings/columns/table-management-remaining-work-value.md)、[数値項目](../editor/editor-settings/columns/table-management-num.md)以外使用できません。
1.  「グループ化」の[項目](../editor/editor-settings/columns/index.md)には[状況項目](../editor/editor-settings/columns/table-management-status.md)、[管理者項目](../editor/editor-settings/columns/table-management-manager.md)、[担当者項目](../editor/editor-settings/columns/table-management-owner.md)、[分類項目](../editor/editor-settings/columns/table-management-class.md)、[チェック項目](../editor/editor-settings/columns/table-management-check.md)以外使用できません。
1.  [複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)を有効化している[分類項目](../editor/editor-settings/columns/table-management-class.md)による「グループ化」は行えません。

[作業量項目]: ../editor/editor-settings/columns/table-management-work-value.md
[残作業量項目]: ../editor/editor-settings/columns/table-management-remaining-work-value.md
[数値項目]: ../editor/editor-settings/columns/table-management-num.md
[項目]: ../editor/editor-settings/columns/index.md
[状況項目]: ../editor/editor-settings/columns/table-management-status.md
[管理者項目]: ../editor/editor-settings/columns/table-management-manager.md
[担当者項目]: ../editor/editor-settings/columns/table-management-owner.md
[分類項目]: ../editor/editor-settings/columns/table-management-class.md
[チェック項目]: ../editor/editor-settings/columns/table-management-check.md
[複数選択]: ../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md
[分類項目]: ../editor/editor-settings/columns/table-management-class.md

## 必要な権限

![サイトの管理権限](../../../assets/badge_manage_site.svg)

## 操作手順

1.  該当のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [テーブルの管理](../index.md)をクリックしてください。

    ![「管理」メニューを開いたナビゲーションメニュー。「テーブルの管理」が並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/bbb54a98085a42449c552d39f2ed77fb.png)

1.  「集計」タブをクリックしてください。「選択肢一覧」で集計したい[項目](../editor/editor-settings/columns/index.md)をクリックし、「追加」ボタンをクリックすると、「現在の設定」へ移動します。「詳細設定」ボタンをクリックすると、「集計種別」を設定できます。

    ![テーブルの管理の「集計」タブ。選択肢一覧と現在の設定が並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/abb65aa34be949f9a349eb9ba782683b.png)

    !!! tip
        「選択肢一覧」で「分類なし」を選択すると、グループ化せずに全体の「集計」を行います。

1.  「集計種別」では「件数」、「合計」、「平均」からいずれか1つを選択してください。

    ![集計の詳細設定。「集計種別」を選ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/aggregations/assets/7e918078b8754116b505bab49a13e8c5.png)

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：作業量](../editor/editor-settings/columns/table-management-work-value.md)
-   [テーブルの管理：項目：残作業量](../editor/editor-settings/columns/table-management-remaining-work-value.md)
-   [テーブルの管理：項目：数値](../editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：状況](../editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理：項目：管理者](../editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../editor/editor-settings/columns/table-management-owner.md)
-   [テーブルの管理：項目：チェック](../editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [テーブルの管理](../index.md)
