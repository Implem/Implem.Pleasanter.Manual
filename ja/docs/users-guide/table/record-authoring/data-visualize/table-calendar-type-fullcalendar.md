---
title: FullCalendar
category: テーブル機能
order: '40'
status: ''
parts: ''
urlstring: table-calendar-type-fullcalendar
translationKey: table-calendar-type-fullcalendar
shortname: カレンダータイプ：FullCalendar
created: 2026-04-01
updated: 2026-04-14
---

## 概要

「[テーブルの管理](../../../../managers-guide/manage-table/index.md)」→「[カレンダー](../../../../managers-guide/manage-table/calendar/index.md)」タブの「カレンダータイプ」で「FullCalendar」を選択した場合の表示と操作方法について説明します。

[カレンダータイプ：標準](table-calendar-type-standard.md)とは、週表示や操作方法に違いがあります。

## 表示のカスタマイズ

「FullCalendar」カレンダータイプの表示は、以下の設定項目を用いてカスタマイズできます。

![FullCalendarの表示を切り替える設定項目の並び](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/2de0f5c34fa7460a932e3927a4061a86.png)

|項目名|説明|
|:-:|:--|
|**項目**|レコードをカレンダーに表示する際に基準とする日付項目を指定します。<br>「期限付きテーブル」では、レコードの「開始」から「完了」までを結合した状態で表示可能です。|
|**状況を表示**|有効化すると、レコードの「[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)」を省略名で表示します。|
|<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">＜</span> <span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">＞</span>|現在表示している表示期間の前の表示期間、次の表示期間のカレンダーを表示します。|
|<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">today</span>|今日を含む表示期間で表示します。|
|<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">month</span>|表示期間を「月」に切り替えます。|
|<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">week</span>|表示期間を「週」に切り替え、時間割形式で表示します。|
|<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">day</span>|表示期間を「日」に切り替え、時間割形式で表示します。|
|<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">list</span>|表示期間を「月」に切り替え、日付ごとにリスト形式で表示します。|

#### 「項目 」による表示の違い

「項目 」ドロップダウンの初期値は「開始 - 完了」です。任意の「日付」項目へ切り替えられます。

![「項目」ドロップダウンで日付項目を切り替えるカレンダー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/a5192277c9754136bce462ac88ebd825.png)

#### 表示期間による表示の違い

<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">month</span>の場合  
![表示期間を「month」にしたFullCalendarの表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/d5cd5ff75b9548b8ac514e8a0d18ffd8.png)

<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">week</span>の場合  
![表示期間を「week」にしたFullCalendarの表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/9e223bbb31384167a0e290ae19b5e8f6.png)

<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">day</span>の場合  
![表示期間を「day」にしたFullCalendarの表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/332a7040872447479cff882c97c0c533.png)

<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">list</span>の場合  
![表示期間を「list」にしたFullCalendarの表示](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/02375b94596f4effaf565210a1706fca.png)

## レコードの操作

カレンダー表示画面から、レコードを新規作成したり、日付項目を編集したりできます。

#### レコードの日付変更

カレンダー上でレコードをドラッグ＆ドロップすることで、「日付」を変更できます。  
<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">list</span>表示中に限り、この操作は無効です。

![カレンダー上でレコードをドラッグして日付を変える様子](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/5a19a97bcc6b4a4ba25f1ca4ccf17ea4.png)

#### 状況を表示する場合の設定

カレンダーに「[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)」を表示したい場合は、「状況を表示」のチェックをオンにしてください。「[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)」は、たとえば「実施中」であれば「<span style="background:green;color:white">実</span>」のような省略名で表示されます。

![レコードに状況の省略名を表示したカレンダー](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/577367aca68f452caf9843302f87c006.png)

#### レコードの新規作成

カレンダーの空白部分をクリックすると、「[レコードの新規作成](../create-records/table-record-new.md)」画面を表示できます。  
また、開始と完了をドラッグ＆ドロップで指定できます。
<span style="background:#106EBE;color:white;padding-left:4px;padding-right:4px;">list</span>表示中に限り、この操作は無効です。

![カレンダーの空白部分から開いたレコードの新規作成画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/79e0edff738c4f4696b38f2b663ad665.png)

#### レコードの編集

既存のレコードをクリックすると、レコードの編集画面が開きます。

![カレンダーのレコードから開いた編集画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/edit-records/assets/cda2576984684faead243b1da891bcb2.png)

## 関連情報

-   [テーブル機能：レコードのカレンダー表示：標準](table-calendar-type-standard.md)