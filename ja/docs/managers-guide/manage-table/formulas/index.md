---
title: 計算式
category: 計算式
order: '10'
status: ''
parts: ''
urlstring: table-management-formula
translationKey: table-management-formula
shortname: 計算式
created: 2019-04-30
updated: 2026-02-10
---

## 概要

テーブルの項目に計算式を設定することで、データ入力の手間を省いたり、入力ミスを防いだりすることができます。

### 計算式が動作するタイミング

計算式は、以下のタイミングで動作します。

1. 画面表示したとき
1. レコードを追加したとき
1. レコードを更新したとき
1. レコードを削除したとき

### 計算方法の種類

プリザンターは「計算対象の項目」と「扱える計算」が異なる、2つの「計算方法」をサポートしています。

|計算方法|計算対象の項目|項目の指定方法|扱える計算|
|:-:|:--|:--|:--|
|**既定**|[数値項目](../editor/editor-settings/columns/table-management-num.md)|[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)<br>[カラム名](../../../developers-guide/dev-column-name.md)|加算（+）<br>減算（-）<br>乗算（*）<br>除算（/）<br>半角の(と)を使った計算順序の変更|
|**拡張**|[数値項目](../editor/editor-settings/columns/table-management-num.md)<br>[分類項目](../editor/editor-settings/columns/table-management-class.md)<br>[日付項目](../editor/editor-settings/columns/table-management-date.md)<br>[説明項目](../editor/editor-settings/columns/table-management-description.md)<br>[チェック項目](../editor/editor-settings/columns/table-management-check.md)|[表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)<br>\[[カラム名](../../../developers-guide/dev-column-name.md)\]|加算（+）<br>減算（-）<br>乗算（*）<br>除算（/）<br>半角の(と)を使った計算順序の変更<br>[計算式（拡張）の場合分け計算](formula-function-logical-expression.md)を用いた計算<br>[計算式（拡張）の関数](formula-function-list.md)を用いた計算|

## 前提条件

1. 計算式を設定するには「サイトの管理権限」が必要です。

## 制限事項

1. 「<a href="#get-error-details">エラーの詳細を取得する</a>」を利用する場合は、計算式の「詳細設定」画面を開き、「計算方法」で「拡張」を選択し、「エラーを表示する」を有効化してください。
1. 計算式の「詳細設定」画面の「計算方法」で「既定」を選択した場合、「<a href="#get-error-details">エラーの詳細を取得する</a>」を有効化しても、エラーの詳細は表示されません（「エラーを表示する」が表示されず、選択できません）。

## テーブルの管理：計算式タブ

[テーブルの管理](../index.md)画面の「計算式」タブには、作成・追加した「計算式」の一覧が表示されます。

![テーブルの管理画面の「計算式」タブ。計算式の一覧と❶〜➍のボタン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/formulas/assets/6ca7b5d4968849c39c728a56d741c561.png)

一覧の左端に表示されたチェックボックスで計算式を選択することで、以下の操作を行えます。

|No|ボタン名|機能|
|:-:|:-:|:--|
|<span class="pl-callout">❶</span>|上|選択した計算式を1つ上に移動します。|
|<span class="pl-callout">➋</span>|下|選択した計算式を1つ下に移動します。|
|<span class="pl-callout">❸</span>|コピー|選択した計算式を複製します。<br>複製された計算式は一覧の一番下へ追加されます。|
|<span class="pl-callout">➍</span>|削除|選択した計算式を一覧から削除します。<br>削除ボタンをクリックすると、確認ダイアログが表示されます。<br>OKボタンをクリックすると、一覧から削除されます。|

### 新規作成

「新規作成」ボタンをクリックすると、計算式の「詳細設定」画面が開き、計算式を一覧へ追加できます。詳細は以下の各マニュアルを確認してください。

1. [計算式（既定）](table-management-formula-default.md)
1. [計算式（拡張）](table-management-formula-extended.md)

計算式を追加した場合は、コマンドボタンエリアの「更新」ボタンをクリックしてください。

### 同期

「同期」ボタンをクリックすると、任意のタイミングで選択した計算式を実行できます。以下のような場合に有用です。

1. 追加済みの「計算式」を更新した場合
1. 作成済みレコードを含むテーブルに「計算式」を追加した場合

### 作成・追加済み計算式の編集

一覧の各行をクリックすると、計算式の「詳細設定」画面が開き、作成済みの計算式を編集できます。計算式を編集した場合は、コマンドボタンエリアの「更新」ボタンをクリックしてください。

### ログを出力する

「ログを出力する」を有効化すると、計算式の設定、計算対象の各項目の値、計算結果を開発者ツールのコンソールに出力します。計算式が意図通りに動かない場合に、使用してください。詳細は[計算式のログ出力](table-management-formula-log-output.md)を確認してください。

<a id="get-error-details"></a>

### エラーの詳細を取得する

計算式の「詳細設定」で「エラーを表示する」を有効化している場合、プリザンターはシステムログへエラーメッセージを出力します。「エラーを表示する」に加えて「エラーの詳細を取得する」を有効化すると、システムログへ出力されるエラーメッセージを、開発者ツールの「コンソール」でも確認できるようになります。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.1.0 以降| 「エラーの詳細を取得する」を追加|

## 関連情報

-   [テーブルの管理：項目：数値](../editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../editor/editor-settings/advanced-settings/general/table-management-label-text.md)
-   [項目名とデータベース上のカラム名の対応](../../../developers-guide/dev-column-name.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：日付](../editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../editor/editor-settings/columns/table-management-check.md)
-   [計算式（拡張）の関数で使用する論理式](formula-function-logical-expression.md)
-   [計算式（拡張）の関数](formula-function-list.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：計算式（既定）](table-management-formula-default.md)
-   [テーブルの管理：計算式（拡張）](table-management-formula-extended.md)
-   [テーブルの管理：計算式：ログを出力する](table-management-formula-log-output.md)