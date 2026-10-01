---
title: エディタの設定
category: エディタ
order: '130'
status: ''
parts: ''
urlstring: table-management-editor-columns
translationKey: table-management-editor-columns
shortname: エディタ,エディタの設定
ee_notice: columns
created: 2021-05-09
updated: 2026-04-27
---

## 概要

「エディタの設定」では、レコードの編集画面に配置する項目や、その配置場所を決めることができます。項目をレコードの編集画面に配置するには、項目の有効化が必要です。有効化した項目は、[エディタの項目の詳細設定](advanced-settings/index.md)で更に細かな設定を行えます。また、[タブ](../tab-settings/index.md)や[見出し](advanced-settings/general/table-management-section.md)を新規作成して、項目を整理することができます。なお、[スマートデザイン](../../../../users-guide/smart-design/editor/smart-design-editor.md)を使うと、項目の追加と配置をドラッグ操作で直感的に行えます。

## 制限事項

1.  項目を無効化しても、項目の詳細設定の設定は保持されます。再度「有効化」した際には、保持された設定が戻ります。
1.  項目を無効化しても、その項目に登録済みのデータは保持されます。再度「有効化」した際には、登録済みのデータが戻ります。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

### 1. エディタの設定を開く

1.  対象のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」→[テーブルの管理](../../index.md)を選択してください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  エディタの設定が表示されます。

### 2. 項目の有効化

![エディタの設定の画面。選択肢一覧と「現在の設定」が並ぶ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/924118fb778e4027a9f8965f12f4fb82.png)

1.  「選択肢」ドロップダウンリストで、項目が選択されていることを確認してください。
1.  [タブ](../tab-settings/index.md)ドロップダウンリストから、項目の配置先となるタブを選択してください。  
    -   この操作は、タブを作成済みの場合のみ必要です。
    -   タブを作成していない場合は、「全般」タブのみを選択可能です。
1.  選択肢一覧の「項目リスト」から、有効化したい項目を選択してください。  
    -   フィルタ機能を使うことで、「項目リスト」の表示を絞り込めます。
1.  「有効化」ボタンをクリックしてください。  
    -   有効化した項目が「現在の設定」の一番下に追加され、項目設定エリアが表示されます。
1.  「上」ボタンまたは「下」ボタンを使用して表示する位置を調整してください。  
    -   「項目リスト」での表示順が、レコードの編集画面での表示順となります。  
    -   ++ctrl++ キーを押しながら「上」ボタンをクリックすると、選択中の項目を「項目リスト」の一番上へ移動できます。  
    -   ++ctrl++ キーを押しながら「下」ボタンをクリックすると、選択中の項目を「項目リスト」の一番下へ移動できます。  
    -   「上」ボタン、「下」ボタンは、「現在の設定」でフィルタ機能を使っていると表示されません。  
    -   選択中の項目を再度クリックすると、選択を解除できます。
1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

#### 2.1. フィルタ

[フィルタ](../../../../users-guide/hands-on/advanced/advanced-operations-link.md)を使うことで、「項目リスト」の表示を絞り込めます。また、複数のフィルタを同時に指定できます。

|                   アクティブ時                   |                  非アクティブ時                  | 名称                     | 説明                                                                                                                   |
| :----------------------------------------------: | :----------------------------------------------: | :----------------------- | :--------------------------------------------------------------------------------------------------------------------- |
| ![アクティブ時の「基本」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/b10551cf8d694fb3bef291306c759083.png) | ![非アクティブ時の「基本」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/30a61edc446144c7bfd7d958c642eac1.png) | 基本ボタン               | クリックすると[基本項目](columns/table-management-column.md)を表示します。                                                     |
| ![アクティブ時の「分類」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/1ea3153375034ef7823a62ea5ffd8414.png) | ![非アクティブ時の「分類」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/fcc1c8f831a74b389f8c846470f58a1b.png) | 分類ボタン               | クリックすると[分類項目](columns/table-management-class.md)を表示します。                                                      |
| ![アクティブ時の「数値」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/d982be49e39e4911a3f0ca32b013caa1.png) | ![非アクティブ時の「数値」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/85c96cfe796a4f419acf28869171db5d.png) | 数値ボタン               | クリックすると[数値項目](columns/table-management-num.md)を表示します。                                                        |
| ![アクティブ時の「日付」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/9aa5b297e247464580fa124b7f764f29.png) | ![非アクティブ時の「日付」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/bd19addba3f24bb3bba47470c020875c.png) | 日付ボタン               | クリックすると[日付項目](columns/table-management-date.md)を表示します。                                                       |
| ![アクティブ時の「説明」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/864ce3807e1441e798ffe99c2c9f695b.png) | ![非アクティブ時の「説明」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/e4b2cadd37d646bcbc46cc2aa49f19ce.png) | 説明ボタン               | クリックすると[説明項目](columns/table-management-description.md)を表示します。                                                |
| ![アクティブ時の「チェック」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/7118c9f417e147cfb863ce0e7ea28eea.png) | ![非アクティブ時の「チェック」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/17aa5f6bde46440aa23f815132a56995.png) | チェックボタン           | クリックすると[チェック項目](columns/table-management-check.md)を表示します。                                                  |
| ![アクティブ時の「添付ファイル」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/de47da6476d14492ad980dafba7a28b2.png) | ![非アクティブ時の「添付ファイル」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/c5ee6de384534ff4b552a3fe12b11be1.png) | 添付ファイルボタン       | クリックすると[添付ファイル項目](columns/table-management-attachments.md)を表示します。                                        |
| ![アクティブ時のフィルタテキストボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/4d73408578514ccca37a008691fc03eb.png) | ![非アクティブ時のフィルタテキストボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/d28b9764b1264e97baa81de3ac11dcfc.png) | フィルタテキストボックス | 選択肢一覧リスト、現在の設定リストの表示を[表示名](advanced-settings/general/table-management-label-text.md)またはその部分文字列で絞り込めます。 |

#### 2.2. 項目設定エリア

「現在の設定」の「項目リスト」で項目を選択すると、リスト下部に「項目設定エリア」が表示されます。

![「現在の設定」で項目を選んだときに表示される項目設定エリア](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/4e81b2040e804c0d92cbd07f9bba7664.png)

「項目設定エリア」には、以下の4つのボタンが表示されます。「上」ボタン、「下」ボタンは、「現在の設定」でフィルタ機能を使っていると表示されません。  

|                     アイコン                     | 名称           | 説明                                                                                                                                                              |
| :----------------------------------------------: | :------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![「上」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/efac02a63b214f8ebc3bb73df20b5b38.png) | 上ボタン       | クリックすると、選択中の項目と、1つ上の項目とを入れ替えます。Ctrlキーを押しながらクリックすると、リストの一番上へ移動します。フィルタ機能使用時は表示されません。 |
| ![「下」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/96ad14d5ba544d49bc09440b21421aff.png) | 下ボタン       | クリックすると、選択中の項目と、1つ下の項目とを入れ替えます。Ctrlキーを押しながらクリックすると、リストの一番下へ移動します。フィルタ機能使用時は表示されません。 |
| ![「詳細設定」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/8fe5babcd2554bc6950aa091f766a5b9.png) | 詳細設定ボタン | クリックすると、選択中の項目の「詳細設定」画面を表示します。                                                                                                      |
| ![「リセット」ボタンのアイコン](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/assets/dc12b607a8db4068a77b4f3dd0c28f54.png) | リセットボタン | クリックすると、「詳細設定」画面で行った変更をリセットし、無効化します。更新ボタンのクリック後も無効化します。                                                    |

### 3. 項目の無効化

1.  「現在の設定」の「項目リスト」で無効化したい項目を選択し、「無効化」ボタンをクリックしてください。
1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

### 4. 有効化した項目の整理

有効化した項目を整理するには、以下の方法があります。

1.  [タブ](../tab-settings/index.md)を使う方法
1.  [見出し](advanced-settings/general/table-management-section.md)を使う方法

詳細は、それぞれのリンク先をご覧ください。

## 対応バージョン

| 対応バージョン | 内容                                 |
| :------------- | :----------------------------------- |
| 1.1.21.0 以降  | 「エディタの設定」のデザインを変更。 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定](advanced-settings/index.md)
-   [テーブルの管理：エディタ：タブ](../tab-settings/index.md)
-   [テーブルの管理：エディタ：見出し](advanced-settings/general/table-management-section.md)
-   [スマートデザイン：エディタ：操作方法](../../../../users-guide/smart-design/editor/smart-design-editor.md)
-   [テーブルの管理](../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [応用編：リンク](../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：項目：基本](columns/table-management-column.md)
-   [テーブルの管理：項目：分類](columns/table-management-class.md)
-   [テーブルの管理：項目：数値](columns/table-management-num.md)
-   [テーブルの管理：項目：日付](columns/table-management-date.md)
-   [テーブルの管理：項目：説明](columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](columns/table-management-attachments.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](advanced-settings/general/table-management-label-text.md)
-   [Contact](https://implem.co.jp/contact)
