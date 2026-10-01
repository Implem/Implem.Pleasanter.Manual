---
title: 標準
category: テーブル機能
order: '30'
status: ''
parts: ''
urlstring: table-calendar-type-standard
translationKey: table-calendar-type-standard
shortname: カレンダータイプ：標準
created: 2026-04-01
updated: 2026-04-14
---

## 概要

「[テーブルの管理](../../../../managers-guide/manage-table/index.md)」→「[カレンダー](../../../../managers-guide/manage-table/calendar/index.md)」タブの「カレンダータイプ」で「標準」を選択した場合の表示と操作方法について説明します。

[カレンダータイプ：FullCalendar](table-calendar-type-fullcalendar.md)とは、週表示や操作方法に違いがあります。

## 表示のカスタマイズ

「標準」カレンダータイプの表示は、以下の設定項目を用いてカスタマイズできます。

![標準カレンダーの表示を切り替える設定項目の並び](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/1429599ad3bb4b37a8c3cb0b4bffa5be.png)

|項目名|説明|
|:--:|:---|
|**分類**|「[選択肢一覧](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/index.md)」を設定した「[分類項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)」を指定すると、選択肢ごとにカレンダーを表示します。<br>「[複数選択](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)」を有効化している分類項目は選択できません。|
|**期間**|カレンダーの表示期間を「年」「月」または「週」に切り替えます。|
|**項目**|レコードをカレンダーに表示する際に基準とする「日付」項目を指定します。<br>期限付きテーブルでは、レコードの「開始」から「完了」までを結合した状態で表示可能です。|
|**日付**|指定した日付を含む期間をカレンダー表示します。|
|**状況を表示**|有効化すると、レコードの「[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)」を省略名で表示します。|
|**前・次**|前の期間または次の期間をカレンダー表示します。|
|**今日**|今日を含む期間をカレンダー表示します。|

#### 「分類」による表示の違い

「分類」を切り替えることで、レコードを複数の視点から確認できます。

![「分類」を切り替えて表示した標準カレンダー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/a9b56e88530845e5a4e8cf0c855e4e6e.png)

#### 「期間」による表示の違い

**「年」の場合**  
![「期間」を「年」にした標準カレンダーの表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/f32dbb2c4e4b41b3afba300215efd001.png)

**「月」の場合**　今日（4月1日 水曜日）の「1」が強調表示されます。  
![「期間」を「月」にした標準カレンダー。今日の日付が強調される](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/15dcb7b0e8414f84beb0d12a4d322149.png)

**「週」の場合**　今日（4月1日 水曜日）の背景が強調表示されます。  
![「期間」を「週」にした標準カレンダー。今日の背景が強調される](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/d07584c03f5f4ab883d420b2568aab57.png)

#### 「項目 」による表示の違い

「項目 」ドロップダウンの初期値は「開始 - 完了」です。任意の「日付」項目へ切り替えられます。

![「項目」ドロップダウンで日付項目を切り替えるカレンダー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/8f7742a7dde94cbf8e95d97a53ddabbb.png)

## レコードの操作

#### レコードの日付変更

カレンダー上でレコードをドラッグ＆ドロップすることで、日付の変更が可能です。  
「期間」で「年」を選択している場合、この操作は無効です。

![カレンダー上でレコードをドラッグして日付を変える様子](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/29b45c3b37fc4f13bf0bec7d8d92ab63.png)

#### 分類項目の選択肢変更

「分類」を選択したカレンダー上で、レコードをドラッグ＆ドロップすることで、分類の選択肢を変更できます。  
「期間」で「年」を選択している場合、この操作は無効です。

![カレンダー上でレコードをドラッグして分類の選択肢を変える様子](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/e8428a6020934014ba1daae1d4e0a4fa.png)

#### 状況を表示する場合の設定

カレンダーに「[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)」を表示したい場合は、「状況を表示」のチェックをオンにしてください。「[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)」は、たとえば「実施中」であれば「<span style="background:green;color:white">実</span>」のような省略名で表示されます。

![レコードに状況の省略名を表示したカレンダー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/d6270e57444d430cbfaf0298072ae98e.png)

#### レコードの新規作成

カレンダーの空白部分をダブルクリックすると、「[レコードの新規作成](../create-records/table-record-new.md)」画面を表示できます。  
「期間」で「年」を選択している場合、この操作は無効です。

![カレンダーの空白部分から開いたレコードの新規作成画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/8c70da7864fd4b05bb93dacf5a52a9ce.png)

#### レコードの編集

以下のいずれかの操作で、カレンダー画面からレコードの[エディタ](../edit-records/table-editor.md)画面を表示できます。

1. 鉛筆マークをクリックする
1. レコードをダブルクリックする

![鉛筆マークからエディタを開くカレンダーの表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/6bdf68873d9c4c2aaf701383a2e75f68.png)

## 関連情報

-   [テーブル機能：レコードのカレンダー表示：FullCalendar](table-calendar-type-fullcalendar.md)
-   [テーブル機能：レコードのエディタ画面](../edit-records/table-editor.md)