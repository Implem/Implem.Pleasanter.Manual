---
title: 項目のアクセス制御
category: アクセス制御
order: '800'
status: ''
parts: ''
urlstring: table-management-column-access-control
translationKey: table-management-column-access-control
shortname: 項目のアクセス制御
created: 2019-05-02
updated: 2026-03-10
---

## 概要

[テーブルの管理](../index.md)画面の「項目のアクセス制御」タブでは、設定により各[項目](../editor/editor-settings/columns/index.md)のアクセス制御（「作成権限」、「読取り権限」、「更新権限」の編集）を行えます。

![テーブルの管理の「項目のアクセス制御」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/column-access-control/assets/9e5a0e1c8849453c8de875884c3acd61.png)

#### 項目のアクセス制御の種類

|No|選択肢|アクセス制御設定時の動作|
|:-:|:----|:----|
|<span class="pl-callout">➊</span>|作成時のアクセス制御|アクセス権を持たない利用者が「レコード」の新規作成を行うと、[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)上で該当の[項目](../editor/editor-settings/columns/index.md)が読取専用となります。<br>「項目の詳細設定」で[既定値](../editor/editor-settings/advanced-settings/general/table-management-default-input.md)を設定している場合、既定値がセットされます。|
|<span class="pl-callout">➋</span>|読取り時のアクセス制御|アクセス権を持たない利用者が「レコード」の[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)や[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)を開いた際に、対象の項目が非表示となります。|
|<span class="pl-callout">➌</span>|更新時のアクセス制御|アクセス権を持たない利用者が「レコード」の[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)を開いた際に、対象の項目が読取専用となります。<br>「サイトの管理」と「権限の管理」など複数のチェックを入れた場合には、全てに該当した場合にアクセスを許可します。|

#### <span class="pl-callout">➍</span>使用中の項目のみ表示

バージョン1.5.2.0以降では、「使用中の項目のみ表示」が有効化された状態で「項目のアクセス制御」が開きます。

|使用中の項目のみ表示|各アクセス制御の表示|
|:-:|:--|
|有効|一覧画面または編集画面に表示されている項目のみが表示されます。|
|無効|選択可能なすべての項目が表示されます（バージョン1.5.1.0以前と同じ挙動）。|

![項目のアクセス制御の画面にある「使用中の項目のみ表示」](https://pleasanter.org/files/images/ja/managers-guide/manage-table/column-access-control/assets/f46d3e59c9124f4e8cd2397f60f9494d.png)

#### <span class="pl-callout">➎</span>詳細設定

「詳細設定」ボタンをクリックすると、以下の画面が開きます。

##### 「基本」タブ

アクセスを許可する[組織](../../department-administration/index.md)、[グループ](../../group-administration/index.md)、[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)に権限を追加します。

![項目のアクセス制御の詳細設定の「基本」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/column-access-control/assets/1a7e8a17b3184f8b9e4dd57c264967a5.png)

##### 「その他」タブの設定

![項目のアクセス制御の詳細設定の「その他」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/column-access-control/assets/da15f30dcd9345d58631ca944f33eb95.png)

|No|選択肢|説明|
|:----|:----|:----|
|<span style="color:green">➊</span>|必要なアクセス許可|対象の「レコード」に対してチェックした権限を持っている[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)にアクセスを許可します。<br>例えば「読取り時のアクセス制御」のその他タブで「サイトの管理」にチェックした場合、「サイトの管理権限」をもっているユーザにのみ[項目](../editor/editor-settings/columns/index.md)を表示します。|
|<span style="color:green">➋</span>|許可するユーザ|対象の「レコード」のチェックした[項目](../editor/editor-settings/columns/index.md)にログインユーザが設定されている場合にアクセスを許可します。<br>例えば「更新時のアクセス制御」のその他タブで「担当者」にチェックした場合、ログインユーザが「担当者」にセットされているレコードのみ[項目](../editor/editor-settings/columns/index.md)が更新可能になります。それ以外の場合には読取専用で表示します。「管理者」と「担当者」など複数のチェックを入れた場合には、何れかに該当した場合にアクセスを許可します。|

「基本」タブと「その他」タブの「必要なアクセス許可」、「許可するユーザ」の何れかに許可の設定が行われているユーザはアクセスが許可されます。それぞれの設定は競合しません。

## 注意事項

1. 「読取り時のアクセス制御」を設定した項目を[タイトル結合](../editor/editor-settings/advanced-settings/general/table-management-title-combination.md)に指定した場合、タイトル上ではアクセス制御が行われません。特定のユーザに閲覧させたくない項目を[タイトル結合](../editor/editor-settings/advanced-settings/general/table-management-title-combination.md)に指定しないでください。

## 前提条件

1. 操作を行うには「サイトの管理権限」と「権限の管理権限」が必要です。

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)に移動してください。
1. ナビゲーションメニューの「管理」をクリックしてください。
1. [テーブルの管理](../index.md)をクリックしてください。
1. 「項目のアクセス制御」タブをクリックしてください。
1. 「作成時のアクセス制御」、「読取り時のアクセス制御」、「更新時のアクセス制御」から対象の[項目](../editor/editor-settings/columns/index.md)を選択し「詳細設定」ボタンをクリックしてください。
1. [選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)から対象の[組織](../../department-administration/index.md)、[グループ](../../group-administration/index.md)、[ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)を選択し「権限追加」ボタンをクリックしてください。
1. 必要に応じて「その他」タブを開き「必要なアクセス許可」、「許可するユーザ」にチェックを入れてください。
1. ダイアログ下部の「変更」ボタンをクリックしてください。
1. 画面下部の「更新」ボタンをクリックしてください。

## 対応バージョン

|対応バージョン|内容|
|---|---|
|バージョン1.5.2.0 以降|「使用中の項目のみ表示」を追加|

## 関連情報

-   [テーブルの管理](../index.md)
-   [テーブルの管理：項目](../editor/editor-settings/columns/index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：既定値](../editor/editor-settings/advanced-settings/general/table-management-default-input.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [組織管理機能](../../department-administration/index.md)
-   [グループ管理機能](../../group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [テーブルの管理：エディタ：項目の詳細設定：タイトル結合](../editor/editor-settings/advanced-settings/general/table-management-title-combination.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
