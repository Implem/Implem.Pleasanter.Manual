---
title: サマリ
category: サマリ
order: '0'
status: ''
parts: ''
urlstring: table-management-summary
translationKey: table-management-summary
shortname: サマリ
created: 2019-12-09
updated: 2024-06-07
---

## 概要

[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)が設定された「子テーブル」の「レコード」の件数や[数値項目](../editor/editor-settings/columns/table-management-num.md)の合計、平均、最大、最小を「親テーブル」の[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)した「レコード」の[数値項目](../editor/editor-settings/columns/table-management-num.md)に格納します。[サマリ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)はリンク先の子レコードが追加、更新、削除された際に動作します。

## 制限事項

1. リンク項目を複数選択にしている場合には正しく集計できません。
1. サマリの設定を行う前に子レコードが存在している場合、同期機能を使用して集計結果を反映する必要があります。
1. サマリは「子テーブル」から「親テーブル」へ1階層のみ機能します。「親テーブル」にその上位の「親テーブル」へのサマリが設定されていても、多段階のサマリは行われません。

## 前提条件

1. 「サイトの管理権限」が必要です。
1. サマリを利用するためには、事前準備として「子テーブル」に[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の設定を行ってください。

## 操作手順

1. [リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)が設定された「子テーブル」を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [サマリ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)タブを開いてください。
1. 「新規作成」ボタンをクリックしてください。
1. ダイアログの左側の[サイト](../../../users-guide/site/index.md)にサマリの結果を保存する「親テーブル」を設定してください。
1. ダイアログの左側の[項目](../editor/editor-settings/columns/index.md)にサマリの結果を保存する「親テーブル」の[項目](../editor/editor-settings/columns/index.md)を設定してください。
1. 「親テーブル」に[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)が設定されている場合、ダイアログの左側の[条件](../../../FAQ/editor/faq-condition-mode-range.md)に[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)を指定することができます。[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)に指定した[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)に合致しない「親レコード」には[サマリ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)が行われません。
1. ダイアログの左側の[条件](../../../FAQ/editor/faq-condition-mode-range.md)を選択した場合、「条件が満たされていない場合ゼロにする」を指定することができます。[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)の条件に合致しない場合にゼロを格納する場合にはチェックをオンにします。チェックがオフの場合には数値が変更されません。
1. ダイアログの右側の[リンク項目](../links/index.md)に「親テーブル」と関連付けを行っている[項目](../editor/editor-settings/columns/index.md)を設定してください。
1. ダイアログの右側の「サマリ種別」に件数、合計、平均、最大、最小の何れかを設定してください。
1. ダイアログの右側の「サマリ項目」に集計する数値が格納されている[数値項目](../editor/editor-settings/columns/table-management-num.md)を設定してください。「サマリ種別」に「件数」を設定した場合には、この項目は表示されません。
1. 「子テーブル」に[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)が設定されている場合、ダイアログの右側の[条件](../../../FAQ/editor/faq-condition-mode-range.md)に[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)を指定することができます。[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)に指定した[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)に合致しない「子レコード」はサマリの集計対象になりません。
1. 「追加」ボタンをクリックしてください。
1. 画面下部の「更新」ボタンをクリックしてください。
1. 既に集計対象のレコードが存在する場合、対象の[サマリ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)にチェックを付け「同期」ボタンをクリックすると既存レコードのサマリが実行されます。

## 動作イメージ

![サマリの設定ダイアログ。サマリ種別や集計する項目を指定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/5280a4bb2c44492e8062b35e49a8f4ee.png)

サマリ種別は「件数」、「合計」、「平均」、「最小」、「最大」から選択することができます。この場合、親テーブルである「商談」テーブルの「仕入合計」項目に、サマリを設定している子テーブルの「金額」項目の「合計(サマリ種別で設定)」を挿入します。サマリ設定登録以前に登録されたデータは集計の対象とはなりませんので、設定後に「同期」ボタンをクリックしてください。同期する場合は、一覧から対象となるサマリの行左にあるチェックを付けて「同期」ボタンをクリックしてください。
![テーブルの管理のサマリ一覧。チェックを付けて「同期」ボタンを押す](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/a72d7f73fb7d4c73b1c9110c88044ea5.png)

## 使用例

例として、備品の在庫を管理するアプリを作成します。
![備品の在庫を管理するアプリの例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/2b07b1e86040446b9900abd6139e6622.png)
在庫数管理、入出荷管理という記録テーブルを作成します。

在庫数管理テーブル
![作成した在庫数管理テーブル](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/6adfc68e31c249529441e9e8f3885cdb.png)
入出荷管理テーブル
![作成した入出荷管理テーブル](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/5e215d2b90ac4778a75cc45274ec1290.png)
在庫数管理テーブルを親、入出荷管理テーブルを子としてリンクさせます。
![在庫数管理テーブルを親、入出荷管理テーブルを子としたリンクの設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/3387f71b938f416d9b2e949b35da1b80.png)
在庫数管理テーブルが備品のマスタとなりますので、商品名を登録します。
入荷数、出荷数、在庫数は自動で計算されるので0のままにしてください。
![在庫数管理テーブルに商品名を登録し、数量を0のままにしたレコード](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/28defb6334c1465e92f3d41891b694b1.png)
在庫数を自動で計算するために計算式を設定します。
![在庫数を自動で計算するための計算式の設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/19c7520007ce4e1a97ec02c9b9f19b4f.png)
入荷数と出荷数を自動計算させるために、入出荷管理テーブルで以下の通りサマリを設定します。
![入出荷管理テーブルのサマリ設定の一覧](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/cb5867dafb0a4776914cbb085e4ce791.png)
![入出荷管理テーブルのサマリ設定のダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/7751ff81f40541b9bfec0fec26102363.png)
![入出荷管理テーブルにサマリを追加したあとの状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/1d2f8ffa848742cf8d515a79139f91d3.png)
入出荷管理テーブルでレコードを新規作成します。
在庫数管理テーブルとリンクした商品名には在庫数管理テーブルに登録した商品名が表示されます。
![入出荷管理テーブルの新規作成画面。リンクした商品名を選べる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/66287489ba4c41b9b64e5f73eca6c8ef.png)
出荷数を入力し登録します。
![入出荷管理テーブルで出荷数を入力して登録したレコード](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/476e9d85f14743b6a26a2d91a2ef3d36.png)
入出荷管理テーブルで登録した内容が在庫数管理テーブルに自動的に反映されます。
![入出荷管理テーブルの登録内容が反映された在庫数管理テーブル](https://pleasanter.org/files/images/ja/managers-guide/manage-table/summaries/assets/08063d42ac6f42f2bb900e1410d26bfc.png)

## 関連情報

-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：項目：数値](../editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理](../index.md)
-   [サイト機能](../../../users-guide/site/index.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [応用編：ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [テーブルの管理：エディタ：リンク](../links/index.md)