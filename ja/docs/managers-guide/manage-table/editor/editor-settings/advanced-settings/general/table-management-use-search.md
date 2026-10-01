---
title: 検索機能を使う
category: エディタ
order: '11000'
status: ''
parts: ''
urlstring: table-management-use-search
translationKey: table-management-use-search
shortname: 検索機能を使う
created: 2021-05-02
updated: 2026-02-12
---

## 概要

「検索機能を使う」は、以下の項目の「詳細設定」画面で設定できます。

1.  [分類項目](../../columns/table-management-class.md)
1.  [状況項目](../../columns/table-management-status.md)
1.  [担当者項目](../../columns/table-management-owner.md)
1.  [管理者項目](../../columns/table-management-manager.md)

「検索機能を使う」を有効化すると、キーワード検索を使用して[選択肢一覧](option-list/table-management-choices-text-depts.md)から目的のデータを探すためのダイアログが表示されます。[選択肢一覧](option-list/table-management-choices-text-depts.md)に設定されたデータ数が多い場合に使用してください。

表示されるダイアログは、[複数選択](table-management-multiple-selections.md)が**無効**か**有効**かで変わります。

1.  [複数選択](table-management-multiple-selections.md)が無効の場合の検索ダイアログ  

    ![検索ダイアログ。複数選択が無効なので、キーワードで絞り込んで選択肢を1つ選ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/1f3f0c01fe754d9ca6b1c18981cf7664.png)

1.  [複数選択](table-management-multiple-selections.md)が有効の場合の検索ダイアログ  

    ![検索ダイアログ。複数選択が有効なので、キーワードで絞り込んで選択肢を複数選ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/95f79b6c981f4e65bcbb8149b5b92d53.png)

また、いくつかの場面では、本機能の有効化が必須となります。以下の制限事項を確認してください。

## 制限事項

1.  [選択肢一覧](option-list/table-management-choices-text-depts.md)で他のサイトを[リンク](../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)している場合、パフォーマンスの悪化を防止するために、ドロップダウンリストへ表示する項目数に上限を設けています。上限値は設定ファイル[General.json](../../../../../../setup/parameters/general.json.md)のパラメータDropDownSearchPageSizeで設定されています。既定値は500です。500件より多いレコードを持つサイトをリンクする場合は、本機能を有効化してください。
1.  [一覧](../../../../grid/index.md)画面で2階層以上先のリンクしているテーブルの値で[フィルタ](../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)を設定する場合は、本機能を有効化してください。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

### 複数選択が無効の場合

[複数選択](table-management-multiple-selections.md)が**無効**の場合、以下の画面が表示されます。

1.  テキストボックスへキーワードを入力し、[検索](../../../../search/index.md)ボタンをクリックしてください。
1.  目的のデータをクリックしてください。
1.  ダイアログ下部の「選択」ボタンをクリックしてください。  

    ![複数選択が無効のときに検索してデータを選ぶ操作](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/53ab3d5032904039a9229c2d3c451a9c.png)

#### ダブルクリック操作

目的のデータをダブルクリックすると、「選択」ボタンのクリックを省略できます。

### 複数選択が有効の場合

[複数選択](table-management-multiple-selections.md)が**有効**な場合、以下の画面が表示されます。ダイアログ右側のリストには、[選択肢一覧](option-list/table-management-choices-text-depts.md)に設定されたデータが並んでいます。右側のリストでデータをクリックし有効化することで、画面左側のリストへ移動させることができます。ダイアログ左側のリストへデータを並べた状態で、「選択」ボタンをクリックすると、複数項目を選択できます。

1.  ダイアログ右上のテキストボックスへキーワードを入力し、[検索](../../../../search/index.md)ボタンをクリックしてください。
1.  目的のデータをクリックしてください。
1.  「有効化」ボタンをクリックすると、クリックしたデータを画面左側へ移動します。  

    ![複数選択が有効のときに検索したデータを左側へ移す操作](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/fe19648d17ae45f09967566fee3f6a72.png)

1.  ダイアログ下部の「選択」ボタンをクリックしてください。  

    ![検索ダイアログで「選択」ボタンを押した後の画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/b0927308fa1b433b8a5629ea8b7cc681.png)

#### 複数のデータを選択する

| データの位置         | 選択操作                                                                                              |
| :------------------- | :---------------------------------------------------------------------------------------------------- |
| リストの連続した場所 | ドラッグ&ドロップして選択                                                                             |
| リストの離れた場所   | Windowsの場合：++ctrl++ キーを押しながらクリック<br>macOSの場合：++command++ キーを押しながらクリック |

#### ダブルクリック操作

1.  右側のリストのデータをダブルクリックすると、「有効化」ボタンのクリックを省略できます。
1.  左側のリストのデータをダブルクリックすると、「無効化」ボタンのクリックを省略できます。

リスト中の複数のデータを選択した状態でダブルクリックした場合、「有効化」または「無効化」できるのはカーソルがあたったデータのみとなります。また、複数選択は解除されます。

#### すべてのデータを一度に有効化・無効化する

1.  「すべて有効」は画面右側のリストから、画面左側のリストへ、すべてのデータを一括移動します。
1.  「すべて無効」は画面左側のリストから、画面右側のリストへ、すべてのデータを一括移動します。

## 対応バージョン

| 対応バージョン | 内容                     |
| :------------- | :----------------------- |
| 1.5.1.0 以降   | ダブルクリック操作を追加 |

## 関連情報

[テーブルの管理：項目：分類](../../columns/table-management-class.md)  
[テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：リンク](option-list/table-management-choices-text-link.md)
