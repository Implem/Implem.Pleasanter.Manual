---
title: 計算式（既定）
category: 計算式
order: '30'
status: ''
parts: ''
urlstring: table-management-formula-default
translationKey: table-management-formula-default
shortname: 計算式（既定）
created: 2023-12-05
updated: 2026-02-10
---

## 概要

計算方法「既定」は、**[数値項目](../editor/editor-settings/columns/table-management-num.md)**を対象として、**四則計算**を行う計算方法です。

|計算方法|計算対象の項目|項目の指定方法|扱える計算|
|:--|:--|:--|:--|
|**既定**|[数値項目](../editor/editor-settings/columns/table-management-num.md)|[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)<br>[カラム名](../../../developers-guide/dev-column-name.md)|加算（+）<br>減算（-）<br>乗算（*）<br>除算（/）<br>半角の(と)を使った計算順序の変更|

1. 「既定」は、[数値項目](../editor/editor-settings/columns/table-management-num.md)のみを対象とした計算方法です。  
   数値項目以外の項目も対象とする場合は、「拡張」を選択してください。
1. 「既定」は、四則計算（加算、減算、乗算、除算）と半角の(と)による計算順序の変更のみを扱えます。  
   関数を使った計算が必要な場合は、「拡張」を選択してください。

## 制限事項

1. 計算方法で「既定」を選択した場合、[テーブルの管理](../index.md)画面の[計算式](index.md)タブにある「[エラーの詳細を取得する](index.md#get-error-details)」を有効化しても、エラーの詳細は表示されません。

## 「詳細設定」画面の設定項目

### 計算方法

「既定」の計算方法を使用するには、「計算方法」で「既定」を選択してください。

![計算式の「詳細設定」画面で「計算方法」に「既定」を選んだ状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/7417fdd0616345b3aa6029275eadb506.png)

### ID

計算式の追加後にプリザンターによって割り当てられる管理番号です。

### 対象

計算結果を入れる数値項目を選択してください。

### 計算式

以下の要領で計算式を入力してください。計算式中で使用する項目は、事前に[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)で有効化しておく必要があります。

1. +（加算）、-（減算）、*（乗算）、/（除算）を演算子として利用できます。
1. 演算子の前後には、半角スペースを追加してください。
1. 計算の対象となる数値項目は、[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)または[カラム名](../../../developers-guide/dev-column-name.md)で指定してください。
1. 半角の丸括弧で囲った部分は、先に計算されます。

#### 計算対象の表示名に半角丸括弧が含まれる場合

たとえば「消費税(10%)」のように、表示名が半角括弧を含む場合は、NumAのような[カラム名](../../../developers-guide/dev-column-name.md)を指定してください。[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)に半角括弧を使用した項目を指定するとエラーが発生し、追加・変更を行えません。

![表示名に半角丸括弧を含む項目を指定してエラーになった例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/d98377928b2441c4bde773b8bf7da439.png)

その場合、下図のようにカラム名で指定してください。

![同じ計算式をカラム名で指定した例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/a187bf20fba245329e145a0622628033.png)

### 表示名を使用しない

「表示名で作成した計算式」を「カラム名で作成した計算式」として保存したい場合に有効化してください。

### 条件／条件外の場合

テーブルにビューを定義している場合、[条件](../../../FAQ/editor/faq-condition-mode-range.md)プルダウンメニューが表示されます。[条件](../../../FAQ/editor/faq-condition-mode-range.md)でビューを選択すると、「条件外の場合」テキストボックスが表示されます。ビューのフィルタ条件を満たした場合は[計算式](index.md)が動作し、ビューのフィルタ条件を満たさない場合は「条件外の場合」に入力した計算式が動作します。

![「条件」でビューを選び「条件外の場合」が表示された設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/65364498e235439c870eee7421ba109b.png)

### 無効

編集中の計算式を一時的に動作させなくする場合に有効化してください。

計算式を追加、変更した場合は、同期やテーブルの更新を実行してください。

## 関連情報

-   [テーブルの管理：項目：数値](../editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)
-   [項目名とデータベース上のカラム名の対応](../../../developers-guide/dev-column-name.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：計算式](index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)