---
title: $p.getValue
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-get-value
translationKey: script-get-value
shortname: $p.getValue
created: 2024-12-26
updated: 2026-08-05
---

## 概要

編集画面上で対象の項目名から値を取得するメソッドの説明です。  対象の項目の値を利用するときに使用してください。

## 制限事項

1.  [コメント](../../../users-guide/common/comment.md)の値は取得できません。

## 構文

##### JavaScript

```
$p.getValue('項目名または表示名')
```

## 取得内容

[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)で以下のような取得結果になります。

### 分類項目

-   選択肢の指定内容に応じて以下の内容を取得します。「ID」、「バージョン」、[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)、[状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)、「管理者」、「担当者」も同様です。

|選択肢の設定|取得内容|備考|
|---|---|---|
|未設定|入力した文字列|「ID」、「バージョン」、[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)はこちらに該当します。フリーテキスト形式の項目|
|文字列|選択肢の文字列||
|コードと文字列|選択肢のコード|[状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)はこちらに該当します。選択肢の文字列を取得したい場合は[$p.getControl](../value-operations/script-get-control.md)を使用してください。|
|他テーブルのリンク|選択肢のコード（レコードID）|「管理者」、「担当者」はこちらに該当します。選択肢の文字列を取得したい場合は[$p.getControl](../value-operations/script-get-control.md)を使用してください。|

### 数値項目

-   入力値を「文字列」として取得します。スクリプトで利用する際は必要に応じて型変換してください。
-   小数点以下は有効桁数を0埋めした値を取得します。（コントロール種別：スピナーで読取専用OFFの場合に限り画面表示の値を取得します。）
-   書式を指定している場合、書式変換前の値を取得します。
-   単位を設定している場合、取得する値には単位は含まれません。
-   「作業量」、[進捗率](../../../users-guide/table/record-authoring/edit-records/table-record-progression-rate.md)、「残作業量」も同様です。

### 日付項目

-   入力値を「文字列」として取得します。スクリプトで利用する際は必要に応じて型変換してください。
-   「開始」、「完了」も同様です。

### 説明項目

-   入力値を「文字列」として取得します。
-   貼り付けた画像はURL文字列として取得します。
-   [内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)も同様です。

### チェック項目

-   入力したチェックON／OFFに応じてtrue／falseの真偽値を取得します。

### 添付ファイル項目

-   以下のような配列形式の「文字列」として取得します。

```
[{"Guid":"1234...","Name":"テストPDFファイル.pdf","Size":12345},{"Guid":"ABCD...","Name":"テストxlsxファイル.xlsx","Size":45678},{"Guid":"4E5F6G...","Name":"テストpptxファイル.pptx","Size":901234}]
```

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定し出力先は「編集」にした後、編集画面に遷移してください。開発者ツールのConsoleに値を出力します。

##### JavaScript

```
$p.events.on_editor_load = function () {
    // 開発者ツールのConsoleに値を出力
    console.log($p.getValue('顧客'));       // 『顧客』（ClassA）で選択した選択肢のコード（レコードID）
    console.log($p.getValue('ClassA'));     // 『顧客』の項目名であるClassAでも取得可能
    console.log($p.getValue('件名'));       // 『件名』
    console.log($p.getValue('Body'));       // 『内容』の項目名であるBodyで取得
    console.log($p.getValue('状況'));       // 『状況』で選択した選択肢のコード
    console.log($p.getValue('受注予定日'));  // 『受注予定日』
    console.log($p.getValue('ClassB'));     // 『商品区分』の項目名であるClassBで取得
    console.log($p.getValue('売上'));       // 『売上』、書式変換前の数値を取得
    console.log($p.getValue('NumD'));       // 『粗利率』の項目名であるNumDで取得、単位を除いた数値を取得
}
```

#### 出力結果

![$p.getValueの出力結果](https://pleasanter.org/files/images/ja/developers-guide/script/uncategorized/assets/00b546ab00514245b336cb6fe5013a1e.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [共通機能：コメントを追加](../../../users-guide/common/comment.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [$p.getControl](../value-operations/script-get-control.md)
-   [テーブル機能：レコードの進捗率表示](../../../users-guide/table/record-authoring/edit-records/table-record-progression-rate.md)
-   [テーブルの管理：項目：内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
