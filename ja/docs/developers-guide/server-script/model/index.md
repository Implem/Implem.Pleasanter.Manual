---
title: model
icon: material/alpha-o-box
category: サーバスクリプト
order: '8000'
status: ''
parts: ''
urlstring: server-script-model
translationKey: server-script-model
shortname: model
created: 2021-01-22
updated: 2025-09-19
---

## 概要

[サーバスクリプト](../index.md)で使用可能な現在の「レコード」の情報をもつオブジェクトです。プロパティを使用し[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の値の読み取りが行えます。プロパティに値を代入すると[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)や[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)の項目の表示を変更できますが「レコード」の更新を行うことはできません。他のテーブルの「レコード」の取得や「レコード」の更新を行う場合は[itemsオブジェクト](../items/index.md)を使用してください。

## 制限事項

1. 「サイト設定読み込み時」、「ビュー処理時」の条件では使用できません。
1. [一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)では「行表示の前」の条件を指定した場合のみ使用できます。
1. [項目のアクセス制御](../../../managers-guide/manage-table/column-access-control/index.md)で「読み取り権限」の無い[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)は取得できません。
1. [項目のアクセス制御](../../../managers-guide/manage-table/column-access-control/index.md)で「更新権限」の無い[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)は値を代入しても画面の表示を変更できません。
1. 画面上に存在しない[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)は取得できません。画面上にない[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を取得するには「AlwaysGetColumnsオブジェクト」を使用してください。
1. [添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)はファイルそのものを取得できません。添付ファイルに関するメタデータ(JSON)のみ取得可能です。

## プロパティ

|No|プロパティ名|get|set|type|説明|
|:----|:----|:----|:----|:----|:----|
|1|IssueId / ResultId|○| |long|[ID項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)|
|2|SiteId|○| |long|「サイトID項目」|
|3|Creator|○| |int|[作成者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-creator.md)|
|4|CreatedTime|○| |DateTime|[作成日時項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-created-time.md)|
|5|Updator|○| |int|[更新者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updator.md)|
|6|UpdatedTime|○| |DateTime|[更新日時項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updated-time.md)|
|7|Ver|○| |int|[バージョン項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-ver.md)|
|8|Title|○|○|string|[タイトル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)|
|9|Body|○|○|string|[内容項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)|
|10|StartTime|○|○|DateTime|[開始項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)|
|11|CompletionTime|○|○|DateTime|[完了項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)|
|12|WorkValue|○|○|decimal|[作業量項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-work-value.md)|
|13|ProgressRate|○|○|decimal|[進捗率項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)|
|14|RemainingWorkValue|○| |decimal|[残作業量項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-remaining-work-value.md)|
|15|Status|○|○|int|[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)|
|16|Manager|○|○|int|[管理者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)|
|17|Owner|○|○|int|[担当者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)|
|18|Locked|○|○|bool|[ロック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-lock.md)|
|19|Comments|○| |string|[コメント項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)|
|20|ClassA～|○|○|string|[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)|
|21|NumA～|○|○|decimal|[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)|
|22|DateA～|○|○|DateTime|[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)|
|23|DescriptionA～|○|○|string|[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)|
|24|CheckA～|○|○|bool|[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)|
|25|AttachmentsA～|○| |string|[添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)|
|26|ExtendedRowCss|○|○|string|「行CSS」|
|27|ExtendedRowData|○|○|string|「行データ属性」|
|28|UpdateOnExit| |○|bool|サーバスクリプト終了後にレコードを更新|
|29|ReadOnly|○|○|bool|レコードを読取専用|

## メソッド

メソッドはありません。

## 使用例①

下記の例では[更新日時項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updated-time.md)を取得します。時刻はUTCで取得されますので、必要に応じてJST等に変換してください。

##### JavaScript

```
let updatedTime = model.UpdatedTime;
```

## 使用例②

下記の例では[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を取得します。表示名ではなく値を取得します。

##### JavaScript

```
let status = model.Status;
```

## 使用例③

下記の例では[タイトル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)に'新しいレコードタイトル'を設定します。

##### JavaScript

```
model.Title = '新しいレコードタイトル';
```

## 使用例④

下記の例では[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)に300（レビュー）を設定します。表示名ではなく値を代入します。

##### JavaScript

```
model.Status = 300;
```

## 使用例⑤

下記の例では[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)に「東京都」を設定します。

##### JavaScript

```
model.ClassB = '東京都';
```

## 使用例⑥

下記の例では[複数選択](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)をオンにした[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の値を取得します。取得した値は以下のように配列に置き換えて処理する必要があります。※下記は選択肢一覧に[[Groups*]]を設定

##### JavaScript

```
let groupIdList = JSON.parse(model.ClassA);
for (let groupId of groupIdList) {
    context.Log(groupId);
}
```

## 使用例⑦

下記の例では[複数選択](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)をオンにした[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)に「設計」と「構築」を代入します。[複数選択](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)をオンにした[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)ではJSON形式の文字列で代入する必要があります。

##### JavaScript

```
let data = [];
data.push('設計');
data.push('構築');
model.ClassA = JSON.stringify(data);
```

## 使用例⑧

下記の例では[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)で[管理者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)または[担当者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)がログインユーザのレコードに黄色の背景色のCSSをセットします。条件は「行表示の前」を使用します。[サーバスクリプト](../index.md)と[スタイル](../../style/index.md)を組み合わせて使用します。

##### JavaScript

```
if (model.Manager === context.UserId || model.Owner === context.UserId) {
    model.ExtendedRowCss = 'own';
}
```

##### CSS

```
/* ver1.4.19.2までは .own {～} と要素を指定してください */
.grid .own td{
    background-color: yellow;
}
```

## 使用例⑨

下記の例では[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)のレコードにデータ属性「data-extension」を追加します。※属性名は「extension」固定です。複数のデータ属性を付与したい場合はJSONオブジェクトに格納してセットしてください。

##### JavaScript

```
model.ExtendedRowData = JSON.stringify({ timeout: limit });
```
生成されるHTMLです。

##### HTML

```
<tr class="grid-row" data-extension="'{"timeout":300}'"> ...
```
スクリプトで参照してみます。jQueryのdata()でアクセスします。

##### JavaScript

```
const handler = function () {
    $('table tr').each(function (i, e) {
        var ext = $(e).data('extension');   // var extはJSON object
        if (Date.now() > ext.timeout) {
            ...
        }
    });
};
```

## 使用例⑩

下記の例では[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)に当日の日付をセットし、サーバスクリプト終了後にレコードの更新を行います。

##### JavaScript

```
model.DateA = utilities.Today();
model.UpdateOnExit = true;
```

## 出力例

model.AttachmentsAの出力例(以下は出力された文字列を整形したものです)
```
[
    {
        "Guid": "18F34BCD594F4FF6A94D7C0F9C8AB5D4",
        "Name": "test.txt",
        "Size": 4,
        "HashCode": "n4bQgYhMfWWaL+qgxVrQFaO/TxsrC4Is0V1sFbDwCgg="
    }
]
```
model.Commentsの出力例(以下は出力された文字列を整形したものです)
```
[
    {
        "CommentId": 1,
        "CreatedTime": "2022-12-22T14:42:56.7963585+09:00",
        "Creator": 1,
        "Body": "ここにはコメントの本文が入ります"
    }
]
```

## 詳細情報

1. [一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)では条件に「行表示の前」を指定した場合のみ使用できます。行毎に[サーバスクリプト](../index.md)が実行され各行のレコードが「modelオブジェクト」に格納されます。
1. [エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)では現在、画面に表示されている「レコード」の情報が「modelオブジェクト」に格納されます。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.27.0 以降|Commentsを追加<br>Attachmentsを追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [開発者ガイド：サーバスクリプト：items](../items/index.md)
-   [項目のアクセス制御](../../../managers-guide/manage-table/column-access-control/index.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [テーブルの管理：項目：ID](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)
-   [テーブルの管理：項目：作成者](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-creator.md)
-   [テーブルの管理：項目：作成日時](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-created-time.md)
-   [テーブルの管理：項目：更新者](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updator.md)
-   [テーブルの管理：項目：更新日時](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updated-time.md)
-   [テーブルの管理：項目：バージョン](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-ver.md)
-   [テーブルの管理：項目：タイトル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)
-   [テーブルの管理：項目：内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：開始](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)
-   [テーブルの管理：項目：完了](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)
-   [テーブルの管理：項目：作業量](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-work-value.md)
-   [テーブルの管理：項目：進捗率](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)
-   [テーブルの管理：項目：残作業量](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-remaining-work-value.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理：項目：管理者](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)
-   [テーブルの管理：項目：ロック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-lock.md)
-   [テーブルの管理：項目：コメント](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [開発者ガイド：スタイル](../../style/index.md)