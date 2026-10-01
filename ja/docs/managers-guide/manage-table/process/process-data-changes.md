---
title: データの変更
category: プロセス
order: '600'
status: ''
parts: ''
urlstring: process-data-update
translationKey: process-data-update
shortname: ''
created: 2025-06-19
updated: 2025-10-29
---

## 概要

プロセス用のボタン押下時のデータの変更内容を設定します。任意の値の入力や値のコピーなどが可能です。

![プロセスのデータの変更タブ。ボタン押下時の変更内容を設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/7cf90b2597914add8c37d9958cb3de48.png)

## 操作手順

1.  データの変更タブをクリックします。
1.  「新規作成」ボタンをクリックします。
1.  変更種別を選択をします。
1.  変更種別に合わせて必要な項目を設定します。
1.  「変更」ボタンをクリックします。
1.  プロセス管理の「更新」ボタンをクリックします。

## 変更種別

| No  | 選択肢         | 説明                                                                                                                                                                                                                                    |
| :-- | :------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 値のコピー     | 指定した「コピー元」の項目の値が、指定した[項目](../editor/editor-settings/columns/index.md)にコピーされます。                                                                                                 |
| 2   | 表示名のコピー | 指定した「コピー元」の項目の表示名が、指定した[項目](../editor/editor-settings/columns/index.md)にコピーされます。                                                                                             |
| 3   | 値の入力       | 指定した「値」が、指定した[項目](../editor/editor-settings/columns/index.md)にコピーされます。「値」には項目の表示名を指定することも可能です。[^1]                                                             |
| 4   | 値の関数操作   | 指定した計算式（拡張）の計算結果が、指定した項目にコピーされます。[^2]                                                                                                                                                                  |
| 5   | 日付の入力     | 「基準日時」に「期間」を単位として「値」を加算した日付が、指定した[項目](../editor/editor-settings/columns/index.md)に設定されます。値に「1」と入力し、期間に「日」を選択した場合は1日後の日付が設定されます。 |
| 6   | 日時の入力     | 「基準日時」に「期間」を単位として「値」を加算した日時が、指定した[項目](../editor/editor-settings/columns/index.md)に設定されます。値に「1」と入力し、期間に「日」を選択した場合は1日後の日時が設定されます。 |
| 7   | 組織の入力     | ログインした[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の所属する[組織](../../department-administration/index.md)が設定されます。                                   |
| 8   | ユーザの入力   | ログインした[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)が設定されます。                                                                                            |

[^1]: 角括弧（`[ ]`）囲いで項目名を指定することで、動的に値を設定することができます。

      ``` text
      申請金額 ：[金額]
      ```

[^2]: [計算式（拡張）](../formulas/table-management-formula-extended.md)が使用できます。

## 設定例

### 変更種別：値のコピー

分類Aの値を分類Bにコピーする

![変更種別「値のコピー」の設定例。分類Aの値を分類Bにコピーする](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/d4160d7149af4898bf5663aafeb3a8e4.png)

### 変更種別：表示名のコピー

分類Cの表示名を分類Dにコピーする

![変更種別「表示名のコピー」の設定例。分類Cの表示名を分類Dにコピーする](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/9541046924f149d497c869a3a6ad60d0.png)

### 変更種別：値の入力

値（固定文字列＋分類Eの値）を分類Fにコピーする

![変更種別「値の入力」の設定例。固定文字列と分類Eの値を分類Fに入れる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/f757b3406f894a9faac5ebab567c003f.png)

### 変更種別：値の関数操作

計算式（拡張）$DATE([NumA],[NumB],[NumC])の計算結果を日付Aにコピーする

![変更種別「値の関数操作」の設定例。計算式（拡張）の結果を日付Aに入れる](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/d9a94221a5ff4f46b4227f9f24832ef6.png)

-   「計算式の記載方法」、「表示名を使用しない」、「エラーを表示する」の詳細は、[計算式（拡張）](../formulas/table-management-formula-extended.md)を参照ください。
-   プロセス一覧画面の下にある「ログを出力する」の詳細は、[計算式（拡張）](../formulas/table-management-formula-extended.md)を参照ください。

### 変更種別：日付の入力

プロセスを実行した日の1日後の日付を日付Aに設定する

![変更種別「日付の入力」の設定例。実行日の1日後を日付Aに設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/414dccd72bb24839bf730bb3c52b0b35.png)

### 変更種別：日時の入力

プロセスを実行した瞬間の1ヶ月前の日時を日付Bに設定する

![変更種別「日時の入力」の設定例。実行時の1ヶ月前を日付Bに設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/0c13dec732594186bd1e1157f05d7eb3.png)

### 変更種別：組織の入力

ログインした[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の所属する[組織](../../department-administration/index.md)を分類Gに設定する

![変更種別「組織の入力」の設定例。ログインユーザの組織を分類Gに設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/fc27c28dd5be491fb16b8391a93ff061.png)

### 変更種別：ユーザの入力

-   ログインした[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の名前を分類Hに設定する

    ![変更種別「ユーザの入力」の設定例。ログインユーザの名前を分類Hに設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/e02a827401ab4877bf661ce8bc564a47.png)

-   データの変更前

    ![データの変更前のレコードの内容](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/154123c3d66e4b5b8c6434d37340136f.png)

-   データの変更後

    ![データの変更後のレコードの内容。各変更種別の結果が入っている](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/32a9e93ac7034560b838ccf227381559.png)

## 項目の型が異なる場合のデータコピー

項目の型が異なる場合であっても、次の場合は値をコピーできます。

例：[タイトル項目](../editor/editor-settings/columns/table-management-title.md)や[分類項目](../editor/editor-settings/columns/table-management-class.md)などの文字列項目から、[日付項目](../editor/editor-settings/columns/table-management-date.md)や[チェック項目](../editor/editor-settings/columns/table-management-check.md)などに値をコピーする

| 変更種別   | コピー元 | コピー元の入力文字列 | >   | コピー先  | コピーの結果       |
| :--------- | :------- | :------------------- | :-- | :-------- | :----------------- |
| 値のコピー | タイトル | 2022/07/03           | >   | 日付A     | 2022/07/03         |
| 値のコピー | タイトル | 令和4年7月3日        | >   | 日付A     | 2022/07/03         |
| 値のコピー | タイトル | abc                  | >   | 日付A     | （コピーされない） |
| 値のコピー | タイトル | 1                    | >   | チェックA | チェックON         |
| 値のコピー | タイトル | 0                    | >   | チェックA | チェックOFF        |
| 値のコピー | タイトル | true                 | >   | チェックA | チェックON         |
| 値のコピー | タイトル | false                | >   | チェックA | チェックOFF        |
| 値のコピー | タイトル | abc                  | >   | チェックA | （コピーされない） |

※ C#のToString関数で変換できる場合が該当します。

## 変更種別を複数設定している場合の実行

-   変更種別を複数設定している場合は、上から順に処理が行われます。
-   項目に[ルックアップ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)を設定している場合はそれぞれの変更種別の実行後に処理が行われます。

## 一度の[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)でデータ変更を連続実行

一度の[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)で連続してデータ変更できます。下記の例では、No.1の操作を行うことにより、No.2～4の処理が連続して実行されます。

| No  | 操作／処理                   | 補足説明                                                                                                                                                                                                   |
| :-- | :--------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 操作：プロセス用のボタン押下 | [プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能で設定を行います。                                                                                                    |
| 2   | 処理：分類Aを分類Bにコピー   | [プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能：データの変更タブで変更種別「値のコピー」の設定を行います。                                                          |
| 3   | 処理：分類Bを分類Cに転記     | [エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)機能：選択肢一覧で[ルックアップ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)の設定を行います。 |
| 4   | 処理：分類Cを分類Dにコピー   | [プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)機能：データの変更タブで変更種別「値のコピー」の設定を行います。                                                          |

## 対応バージョン

| 対応バージョン | 内容                                                                             |
| :------------- | :------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | 変更種別に値の関数操作を追加<br>メール通知の宛先にCc、Bccを追加                  |
| 1.4.11.0 以降  | 実行種別に追加したボタン／作成・更新を追加<br>共通設定・全般タブにアイコンを追加 |

## 関連情報

-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [組織管理機能](../../department-administration/index.md)
-   [テーブルの管理：計算式（拡張）](../formulas/table-management-formula-extended.md)
-   [テーブルの管理：項目：タイトル](../editor/editor-settings/columns/table-management-title.md)
-   [テーブルの管理：項目：分類](../editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：日付](../editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：チェック](../editor/editor-settings/columns/table-management-check.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
