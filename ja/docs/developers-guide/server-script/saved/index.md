---
title: saved
icon: material/alpha-o-box
category: サーバスクリプト
order: '9000'
status: ''
parts: ''
urlstring: server-script-saved
translationKey: server-script-saved
shortname: saved
created: 2022-10-18
updated: 2023-01-05
---

## 概要

[サーバスクリプト](../index.md)で使用可能な更新前の「レコード」の情報をもつオブジェクトです。プロパティを使用し[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の値の読み取りが行えます。

## 制限事項

1. 「更新前」の条件で意味を持ちます。その他の条件では、参照できても model と同等となります。
1. [添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)、[コメント項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)は使用できません。
1. [項目のアクセス制御](../../../managers-guide/manage-table/column-access-control/index.md)で「読み取り権限」の無い[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)は取得できません。
1. [項目のアクセス制御](../../../managers-guide/manage-table/column-access-control/index.md)で「更新権限」の無い[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)は値を代入しても画面の表示を変更できません。
1. 画面上に存在しない[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)は取得できません。画面上にない[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を取得するには「AlwaysGetColumnsオブジェクト」を使用してください。

## プロパティ

|No|プロパティ名|type|説明|
|:----|:----|:----|:----|
|1|IssueId / ResultId|long|[ID項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-id.md)|
|2|SiteId|long|「サイトID項目」|
|3|Creator|int|[作成者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-creator.md)|
|4|CreatedTime|DateTime|[作成日時項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-created-time.md)|
|5|Updator|int|[更新者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updator.md)|
|6|UpdatedTime|DateTime|[更新日時項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-updated-time.md)|
|7|Ver|int|[バージョン項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-ver.md)|
|8|Title|string|[タイトル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)|
|9|Body|string|[内容項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)|
|10|StartTime|DateTime|[開始項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-start-time.md)|
|11|CompletionTime|DateTime|[完了項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)|
|12|WorkValue|decimal|[作業量項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-work-value.md)|
|13|ProgressRate|decimal|[進捗率項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-progress-rate.md)|
|14|RemainingWorkValue|decimal|[残作業量項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-remaining-work-value.md)|
|15|Status|int|[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)|
|16|Manager|int|[管理者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)|
|17|Owner|int|[担当者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)|
|18|Locked|bool|[ロック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-lock.md)|
|19|ClassA～|string|[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)|
|20|NumA～|decimal|[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)|
|21|DateA～|DateTime|[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)|
|22|DescriptionA～|string|[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)|
|23|CheckA～|bool|[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)|

## メソッド

メソッドはありません。

## 使用例

「更新前」であっても model には、画面や CSV から送信されたデータで変更された値(これからデータベースに保持される値)が保持されています。
このため、model.Status が何であるかを判定するサーバスクリプトでは、ある状態に変更されたときだけ動作させたい処理を実現することが難しいです。
下記の例では[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)が変化したかを saved を使って判定しています。

##### JavaScript（サーバスクリプト）

```
const prevStatus = saved.Status;
const currentStatus = model.Status;
if(prevStatus !== currentStatus) {
  context.Log(`Status just has been changed.`);
}
```

同様にして、特定のデータ項目の変更前後の監視を実現することができます。

また、更新後に同様の判定を行いたい場合には [context.UserData](../context/server-script-context-user-data.md) に変更があったことを検知する共有変数を保持することで実現できる可能性があります。

ステータスに対して羃等(idempotent)な処理については、このような対応をする必要はありません。

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [テーブルの管理：項目：コメント](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [項目のアクセス制御](../../../managers-guide/manage-table/column-access-control/index.md)
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
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [開発者ガイド：サーバスクリプト：context.UserData](../context/server-script-context-user-data.md)