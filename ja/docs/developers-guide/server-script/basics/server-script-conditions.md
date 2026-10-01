---
title: 条件
category: サーバスクリプト
order: '1000'
status: ''
parts: ''
urlstring: server-script-conditions
translationKey: server-script-conditions
shortname: サーバスクリプトの条件,条件
created: 2021-01-22
updated: 2026-02-09
---

## 概要

[サーバスクリプト](../index.md)はサーバサイドで実行する条件を制御することが可能です。各条件について説明します。

![サーバスクリプトの条件の設定欄](https://pleasanter.org/files/images/ja/developers-guide/server-script/basics/assets/91ac5e26fff84516a1a08e028ed1f227.png)

## 制限事項

1. [一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)時は「削除前」、「削除後」のどちらの条件でも実行しません。「一括削除前」、「一括削除後」をご使用ください。
2. 単一レコードの[削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)時は「一括削除前」、「一括削除後」のどちらの条件も実行しません。「削除前」、「削除後」をご使用ください。

## 設定内容

|No|条件|説明|
|:----|:----|:----|
|1|サイト設定の読み込み時|[既定のビュー](../../../managers-guide/manage-table/grid/table-management-default-view.md)を変更する際に使用します。|
|2|ビュー処理時|[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)を使用し[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)や[並び替え](../../../users-guide/table/record-authoring/data-analysis/table-record-sort.md)を設定する際に使用します。|
|3|「レコード」読み込み時|「レコード」読み込み後に項目の内容を変更する際に使用します。|
|4|計算式の前|計算式の実行前に項目の内容を変更する際に使用します。ポストバックで実行する際に使用します。|
|5|計算式の後|計算式の実行後に項目の内容を変更する際に使用します。ポストバックで実行する際に使用します。|
|6|作成前|「レコード」が作成される前に実行します。|
|7|作成後|「レコード」が作成された後に実行します。|
|8|更新前|「レコード」が更新される前に実行します。|
|9|更新後|「レコード」が更新された後に実行します。|
|10|削除前|「レコード」が削除される前に実行します。[一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)では実行しません。|
|11|削除後|「レコード」が削除された後に実行します。[一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)では実行しません。|
|12|一括削除前|「レコード」が一括削除される前に実行します。単一レコードの[削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)では実行しません。|
|13|一括削除後|「レコード」が一括削除された後に実行します。単一レコードの[削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)では実行しません。|
|14|画面表示の前|画面の表示内容を変更する際に使用します。プロセスボタンによる一括操作後の場合にも実行します。ポストバックで実行する際に使用します。|
|15|行表示の前|[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)で行やセルの[スタイル](../../style/index.md)や表示内容を設定する際に使用します。編集画面のリンクテーブルを表示する際にも実行します。|
|16|共有|[コードの共有](server-script-shared.md)として使用します。|

## [拡張サーバスクリプト](../../extended-features/extended-server-script.md)の条件

[拡張サーバスクリプト](../../extended-features/extended-server-script.md)では「共有」を除く条件について、[サーバスクリプト](../index.md)と同様に指定できます。

[拡張サーバスクリプト](../../extended-features/extended-server-script.md)で条件を指定する方法は[拡張サーバスクリプト](../../extended-features/extended-server-script.md)のマニュアルを参照してください。

## Pleasanter Code Assistの拡張サーバスクリプトの条件

Pleasanter Code Assistの拡張サーバスクリプトでは「共有」を除く条件について、[サーバスクリプト](../index.md)と同様に指定できます。

Pleasanter Code Assistの拡張サーバスクリプトで条件を指定する方法は[Pleasanter Code Assistの拡張機能](../../../products-info/pleasanter-extensions/pleasanter-code-assist/pleasanter-code-assist-how-to-use-extensions.md)のマニュアルを参照してください。

## 「一括削除前」、「一括削除後」の補足事項

### 使用例　一括削除したレコードIDを取得する方法

**・「一括削除前」のサーバスクリプト例**

``` javascript
let ids = [];
if (context.ApiRequestBody) {
  const apiJson = JSON.parse(context.ApiRequestBody);
  // APIやitems.BulkDeleteを使用しSelectedでIDを指定して一括削除する場合
  if (apiJson.Selected) {
    ids = apiJson.Selected.map(Number);
  }
  else {
    let data = {};
    // APIやitems.BulkDeleteを使用しAllで全レコードを一括削除する場合
    if (apiJson.All) {
      const all = apiJson.All;
      data = { All: all };
    }
    // APIやitems.BulkDeleteを使用しViewで条件を指定して一括削除する場合
    else if (apiJson.View) {
      const view = apiJson.View;
      data = { View: view };
    }
    const apiModels = items.Get(context.Id, JSON.stringify(data));
    for (let apiModel of apiModels) {
      // 記録テーブルの場合はapiModel.ResultId を追加
      // 期限付きテーブルの場合はapiModel.IssueId を追加
      ids.push(apiModel.ResultId);
    }
  }
}
// 画面から一括削除する場合
else {
  for (let id of grid.SelectedIds()) {
    ids.push(id);
  }
}
if (ids && ids.length > 0) {
  // 一括削除後のサーバスクリプトにID一覧を連携
  context.UserData.BulkDeleteIds = ids.join(',');  
}
```

**・「一括削除後」のサーバスクリプト例**

```
if (context.UserData.BulkDeleteIds && context.UserData.BulkDeleteIds != '') {
  // 一括削除前のサーバスクリプトから連携されたIDを取得
  const idsStr = context.UserData.BulkDeleteIds;  
  const ids = idsStr.split(',').map(Number);
  for (let id of ids) {
    // ブラウザの開発者ツールのコンソールログに、一括削除したレコードのIDを出力
    context.Log(id);
  }  
}
```

### [削除時に子レコードを同時に削除する](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-delete-with-links.md)設定との関係

テーブルの分類項目の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に[削除時に子レコードを同時に削除する](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-delete-with-links.md)設定を行っている場合、親レコードの削除と連動して子レコードが削除される際は、子レコードが登録されているテーブルに対して[一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)の処理が実行されます。したがって、子レコードが登録されているテーブルに、条件に「一括削除前」、「一括削除後」を指定したサーバスクリプトが登録されている場合、該当のサーバスクリプトが実行されます。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.16.0 以降|サーバスクリプトの条件に「一括削除前」、「一括削除後」を追加。|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブル機能：レコードの一括削除](../../../users-guide/table/record-authoring/edit-records/table-record-bulkdelete.md)
-   [テーブル機能：レコードの削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)
-   [テーブルの管理：一覧画面：既定のビュー](../../../managers-guide/manage-table/grid/table-management-default-view.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブル機能：レコードの並び替え（ソート）](../../../users-guide/table/record-authoring/data-analysis/table-record-sort.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [開発者ガイド：スタイル](../../style/index.md)
-   [開発者ガイド：サーバスクリプト：コードの共有](server-script-shared.md)
-   [開発者ガイド：拡張機能：拡張サーバスクリプト](../../extended-features/extended-server-script.md)
-   [Pleasanter Code Assist：使い方：拡張機能](../../../products-info/pleasanter-extensions/pleasanter-code-assist/pleasanter-code-assist-how-to-use-extensions.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：削除時に子レコードを同時に削除する](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-delete-with-links.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)