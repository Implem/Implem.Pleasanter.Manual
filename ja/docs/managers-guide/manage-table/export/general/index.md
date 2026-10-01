---
title: 全般タブ
category: エクスポート
order: '0'
status: ''
parts: ''
urlstring: export-create-new
translationKey: export-create-new
shortname: エクスポート：全般
created: 2026-02-12
updated: 2026-07-14
---

## 概要

[テーブルの管理](../../index.md)画面の[エクスポート](../index.md)タブにある「新規作成」ボタンをクリックすると、[エクスポート](../index.md)が開き、「全般」タブが表示されます。ここではエクスポート時の書式を作成・追加できます。

[テーブルの管理]: ../../index.md
[エクスポート]: ../index.md

また、[テーブルの管理](../../index.md)画面の[エクスポート](../index.md)タブにある一覧で、追加済みの書式をクリックした場合も、この画面が開き、追加済みの書式を編集できます。

![エクスポートの書式の詳細設定の「全般」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/general/assets/53e7bee97dc34dbc978050bbea3ecf54.png)

|項目名|説明|設定方法|
|:---|:---|:---|
|名称|作成するエクスポート設定に付与する名前。|任意の名称を入力してください。|
|エクスポートの種類|エクスポート時のファイル形式。|「CSV」または「JSON」を選択してください。<br>既定値は「CSV」です。|
|区切り文字|エクスポートされる各項目の区切り文字。|「カンマ」または「タブ」を選択します。<br>既定値は「カンマ」です。|
|ダブルクォートで囲う|エクスポートされる各項目をダブルクォートで囲う・囲わない。|有効化するとダブルクォートで囲います。<br>既定値は有効です。|
|エクスポート方式|直接ダウンロードする・ダウンロードリンクをメール通知する。|「ダイレクト」または「URLを自分にメール」を選択します。<br>既定値は「ダイレクト」です。|
|ヘッダを出力する|項目名をエクスポートデータに含める・含めない。|有効化すると、項目名をエクスポートデータに含めます。<br>既定値は有効です。|
|[コメントをJSON形式でエクスポートする](../../../../developers-guide/json-data-layout/api-comment.md)|コメント項目をJSON形式でエクスポートする・しない。|有効化するとコメントをJSON形式でエクスポートします。<br>既定値は有効です。|
|エクスポートする項目|以下の説明を確認してください。|以下の説明を確認してください。|

[コメントをJSON形式でエクスポートする]: ../../../../developers-guide/json-data-layout/api-comment.md

## エクスポートする項目

画面右側のリストから説明します。

### 選択肢一覧

[選択肢一覧][]には、現在開いているテーブルで使用可能な項目の一覧が表示されます。現在開いているテーブルとリンクしたテーブルがある場合は、リンクしたテーブル内の項目をエクスポートすることもできます。

[選択肢一覧]: ../../editor/editor-settings/advanced-settings/general/option-list/index.md

![エクスポートする項目の「選択肢一覧」](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/general/assets/9739aaa62e0d4eecac674e1fda082364.png)

エクスポートしたい項目を選択後、「有効化」ボタンをクリックしてください。有効化されると、選択した項目が「現在の設定」へ移動します。

選択肢一覧での選択時には、ドラッグ＆ドロップによる隣り合う項目の一括選択や、++ctrl++（macOSでは ++command++ ）＋クリックによる複数選択が可能です。

### 現在の設定

「現在の設定」では、エクスポートしたい項目を意図した順番に並べ替えたり、エクスポート時に簡易なデータ加工を施したりすることができます。

![エクスポートする項目の「現在の設定」](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/general/assets/f057b6d12cc34c4491b64d7499b92c04.png)

|No|ボタン名|機能|
|:-:|:-:|:--|
|<span class="pl-callout">❶</span>|上|選択した項目を1つ上に移動します。|
|<span class="pl-callout">➋</span>|下|選択した項目を1つ下に移動します。|
|<span class="pl-callout">❸</span>|無効化|選択した項目を選択肢一覧へ移動します。|

「エクスポートする項目」の「現在の設定」で項目を選択し、<span class="pl-callout">➍</span>「詳細設定」ボタンをクリックすると以下の画面が表示されます。

![エクスポートする項目の詳細設定の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/export/general/assets/b48b2547a92040099e635541406ff700.png)

|項目名|説明|設定方法|
|:---|:---|:---|
|表示名|エクスポート時のカラム名を設定できます。|変更したい場合は、任意の名称を入力してください。<br>既定値は[表示名](../../editor/editor-settings/advanced-settings/general/table-management-label-text.md)です。|
|出力|エクスポートする出力内容を設定できます。|以下の3つから1つを選択してください。<br><br>表示名：画面表示している内容<br>短い表示名：一覧画面での表示する内容<br>値：レコードID<br><br>既定値は[表示名](../../editor/editor-settings/advanced-settings/general/table-management-label-text.md)です。|
|分類を列に出力|複数選択項目の出力方式を設定できます。|有効化した場合、選択肢すべてを列として出力し、選択した項目に"1"をつける形式で出力します。詳細は「[複数選択](../../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)」を参照してください。|
|エクスポートの書式|エクスポートする際の日付の書式を設定できます。|日付項目のみ設定可能です。<br>既定値は「年月日」です。|

[表示名]: ../../editor/editor-settings/advanced-settings/general/table-management-label-text.md
[複数選択]: ../../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md

## テーブルの管理：エクスポート：アクセス制御タブ

アクセス制御タブについては、[エクスポート：アクセス制御](../access-controls/index.md)を参照してください。

[エクスポート：アクセス制御]: ../access-controls/index.md

## 関連情報

-   [テーブルの管理](../../index.md)
-   [エクスポート](../index.md)
-   [コメントをJSON形式でエクスポートする](../../../../developers-guide/json-data-layout/api-comment.md)
-   [選択肢一覧](../../editor/editor-settings/advanced-settings/general/option-list/index.md)
-   [表示名](../../editor/editor-settings/advanced-settings/general/table-management-label-text.md)
-   [複数選択](../../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [エクスポート：アクセス制御](../access-controls/index.md)
