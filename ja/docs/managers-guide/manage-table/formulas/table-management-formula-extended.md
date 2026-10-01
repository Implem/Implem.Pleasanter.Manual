---
title: 計算式（拡張）
category: 計算式
order: '40'
status: ''
parts: ''
urlstring: table-management-formula-extended
translationKey: table-management-formula-extended
shortname: 計算式（拡張）
ee_notice: columns
created: 2023-12-05
updated: 2026-02-10
---

## 概要

計算方法「拡張」は、[数値項目](../editor/editor-settings/columns/table-management-num.md)、[分類項目](../editor/editor-settings/columns/table-management-class.md)、[日付項目](../editor/editor-settings/columns/table-management-date.md)、[説明項目](../editor/editor-settings/columns/table-management-description.md)、[チェック項目](../editor/editor-settings/columns/table-management-check.md)を対象として、四則演算や専用の関数を利用した計算を行う計算方法です。

|計算方法|計算対象の項目|項目の指定方法|扱える計算|
|:--|:--|:--|:--|
|**拡張**|[数値項目](../editor/editor-settings/columns/table-management-num.md)<br>[分類項目](../editor/editor-settings/columns/table-management-class.md)<br>[日付項目](../editor/editor-settings/columns/table-management-date.md)<br>[説明項目](../editor/editor-settings/columns/table-management-description.md)<br>[チェック項目](../editor/editor-settings/columns/table-management-check.md)|[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)<br>\[[カラム名](../../../developers-guide/dev-column-name.md)\]|加算（+）<br>減算（-）<br>乗算（*）<br>除算（/）<br>半角の(と)を使った計算順序の変更<br>[計算式（拡張）の関数](formula-function-list.md)を用いた計算<br>[計算式（拡張）の場合分け計算](formula-function-logical-expression.md)を用いた計算|

## 前提条件

[テーブルの管理](../index.md)画面の[計算式](index.md)タブにある「[エラーの詳細を取得する](index.md#get-error-details)」を使用する場合、「詳細設定」画面の「エラーを表示する」を有効化する必要があります。

## 「詳細設定」画面の設定項目

「拡張」の計算方法を使用するには、「計算方法」で「拡張」を選択してください。

![計算式の「詳細設定」画面で「計算方法」に「拡張」を選んだ状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b829e886f82f4ec5b74bfd2624e4483e.png)

### ID

計算式の追加後にプリザンターによって割り当てられる管理番号です。

### 対象

計算結果を入れる数値項目を選択してください。事前に[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)で有効化しておく必要があります。

### 計算式

以下の要領で計算式を入力してください。

1. +（加算）、-（減算）、*（乗算）、/（除算）を演算子として利用できます。
1. 演算子の前後には、半角スペースを追加してください。
1. 計算の対象となる項目（[数値項目](../editor/editor-settings/columns/table-management-num.md)、[分類項目](../editor/editor-settings/columns/table-management-class.md)、[日付項目](../editor/editor-settings/columns/table-management-date.md)、[説明項目](../editor/editor-settings/columns/table-management-description.md)、[チェック項目](../editor/editor-settings/columns/table-management-check.md)）は、[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)または[カラム名](../../../developers-guide/dev-column-name.md)で指定してください。
1. 半角の丸括弧でくくった部分は、先に計算されます。
1. 計算方法「拡張」で、計算対象として[カラム名](../../../developers-guide/dev-column-name.md)を使用する場合は、[カラム名](../../../developers-guide/dev-column-name.md)を半角の角かっこ[と]とで括ってください。追加・変更すると、表示名に変わります。  
   <br>🔽**追加・変更前**
   ![カラム名を角かっこで囲んで入力した、追加・変更前の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/5261f1f0c9384127a4ef10dcae69e544.png)  
   🔽**追加・変更後**  
   ![表示名に変換された、追加・変更後の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/701a5954505c459bbe23a54dc0bdb71a.png)
1. 計算式中で関数を使用できます。使用できる関数は[計算式（拡張）の関数](formula-function-list.md)を参照してください。「計算式（拡張）の条件判定」を使った計算も可能です。
   ![関数を使った計算式の入力例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/fc377cee55434022a6826c9defbaa964.png)

### 表示名を使用しない

「表示名を使用しない」を有効化すると、角かっこ（[]）で囲んだ[カラム名](../../../developers-guide/dev-column-name.md)のまま追加・変更します（[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)に変換しません）。<br>  
🔽**追加・変更前**  
![「表示名を使用しない」有効時の、追加・変更前の計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/4d9ecfb401994cb2b098594c4c9da540.png)  
🔽**追加・変更後**  
![「表示名を使用しない」有効時の、カラム名のまま保存された計算式](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a61f108b178548eba2d61d9fb03c90c2.png)

## エラーを表示する

計算式でエラーが発生すると、[システムログ](../../system-log-administration/index.md)にエラー内容が記録されます。

たとえば、以下のように3つの数値項目と、1つの日付項目を有効化し、レコードを1件作成します。日付Aはレコード作成時は空のままとします。

|数値A|数値B|数値C|日付A|
|:-:|:-:|:-:|:-:|
|-10|12|11|－|

レコードを作成したら、日付Aに計算式を追加し、コマンドボタンエリアの「更新」ボタンをクリックします。計算式で使用している「$DATE」は数値から日付を作る関数ですが、年月日として不正な数値を与えるとエラーとなります。

![日付Aにエラーとなる$DATE関数の計算式を追加した設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ac1832c7c8de4eee8837cccf1e11d557.png)

計算式でエラー発生するため、対象の項目には計算結果は表示されませんが、レコードの更新処理は正常終了します。

![計算結果が表示されないまま更新が完了したレコードの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/ea5612e92b2748c296d1793137d92b59.png)

「管理」－[システムログの管理](../../system-log-administration/index.md)を選択することで、エラーログを確認できます。なお[システムログの管理](../../system-log-administration/index.md)画面を開くには、特権ユーザである必要があります。

![システムログの管理画面に記録されたエラーログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/b2e3c89d99e742cb818463118b457dcc.png)

「エラーを表示する」を有効化すると、システムログにエラー内容が記録されるとともに、コマンドボタンエリアのすぐ上に「計算式の計算に失敗しました…」というメッセージが表示されます。

![「計算式の計算に失敗しました…」というメッセージが表示された画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/59f23f3bfd9145e487f70874cdbea02b.png)

なお、プリザンター1.5.1.0以降では、[テーブルの管理](../index.md)画面の[計算式](index.md)タブで「エラーの詳細を取得する」を有効化することで、開発者ツールのコンソールで詳しいエラー内容を確認できます。

### 条件／条件外の場合

テーブルにビューを定義している場合、[条件](../../../FAQ/editor/faq-condition-mode-range.md)プルダウンメニューが表示されます。
[条件](../../../FAQ/editor/faq-condition-mode-range.md)でビューを選択すると、「条件外の場合」テキストボックスが表示されます。ビューのフィルタ条件を満たした場合は[計算式](index.md)が動作し、ビューのフィルタ条件を満たさない場合は「条件外の場合」に入力した計算式が動作します。

![「条件」でビューを選び「条件外の場合」が表示された設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/c796ca389f8542ce9b7c05832c97f7ec.png)

### 無効

編集中の計算式を一時的に動作させなくする場合に有効化してください。

計算式を追加、変更した場合は、同期やテーブルの更新を実行してください。

## 関連情報

-   [テーブルの管理：項目：数値](../editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：日付](../editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)
-   [項目名とデータベース上のカラム名の対応](../../../developers-guide/dev-column-name.md)
-   [計算式（拡張）の関数](formula-function-list.md)
-   [計算式（拡張）の関数で使用する論理式](formula-function-logical-expression.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：計算式](index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [システムログ管理機能](../../system-log-administration/index.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)