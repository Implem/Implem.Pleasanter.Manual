---
title: 項目連携
category: エディタ
order: '22700'
status: ''
parts: ''
urlstring: table-management-column-relations
translationKey: table-management-column-relations
shortname: 項目連携
created: 2019-12-26
updated: 2024-12-19
---

## 概要

[エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)の[分類項目](../editor-settings/columns/table-management-class.md)に親子関係を設定することができます。親の分類項目を選択した場合に子の分類項目の選択肢が自動で親の分類項目の選択した値に対応したものに切り替わるように設定できます。

## 注意事項

1.  項目の連携を行う項目数や階層に制限はありません。
1.  項目連携を多用すると、編集画面を開いた際のパフォーマンスが悪化する恐れがあります。

## 制限事項

1.  「項目連携」を設定している[テーブル](../../../../users-guide/table/index.md)で[インポート](../../../../users-guide/table/record-authoring/create-records/table-record-import.md)を行うと親子関係が正しく登録できない場合があります。[インポート](../../../../users-guide/table/record-authoring/create-records/table-record-import.md)では表示名に重複がある場合、「項目連携」の設定に関わらず最初に見つかったデータを紐づけます。「項目連携」の子[項目](../editor-settings/columns/index.md)の[表示名](../editor-settings/advanced-settings/general/table-management-label-text.md)に重複がある場合、親[項目](../editor-settings/columns/index.md)の値と関連のない子[項目](../editor-settings/columns/index.md)の値がセットされる可能性があります。親[項目](../editor-settings/columns/index.md)の値と関連のない子[項目](../editor-settings/columns/index.md)の値がセットされた場合、[エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)を開くと子[項目](../editor-settings/columns/index.md)の値がクリアされ未入力の状態となります。
1.  読み取り専用の項目では動作しません。
1.  [一覧編集](../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)では動作しません。

## 前提条件

1.  サイトの管理権限が必要です。
1.  連携する項目は並び順の上下間で親子関係となります。親子関係となる項目の分類の選択肢一覧には[リンク](../../../../users-guide/hands-on/advanced/advanced-operations-link.md)により親子関係に設定されたサイトが指定されている必要があります。
1.  連携可能な項目はエディタ画面に表示する分類項目です。

## 操作手順

### 1.  テーブルの作成とマスタデータの作成

まずは以下の3つの記録テーブルを作成します。

-   住所録テーブルは、都道府県マスタ、市区町村マスタとリンクします。
-   市区町村マスタは、都道府県マスタとリンクします。

![住所録・都道府県マスタ・市区町村マスタの3テーブルの関係図](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/7db4d12ebf3542da9a9120315dcd38c7.png)

#### 「都道府県マスタ」テーブル

![「都道府県マスタ」テーブルの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/5889b5aaa1f147d9929e0f92e22b065f.png)

「都道府県」がタイトル項目です。

「都道府県」が「東京都」、「神奈川県」の2レコードを作成します。

#### 「市区町村マスタ」テーブル

![「市区町村マスタ」テーブルの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/165c0ef1729c4917bc985f599133fd4b.png)

「市区町村」がタイトル項目です。

以下の通り6レコードを作成します。都道府県は「都道府県」項目で選択してください。

| 都道府県 | 市区町村 |
| :------- | :------- |
| 東京都   | 中野区   |
| 東京都   | 新宿区   |
| 東京都   | 渋谷区   |
| 神奈川県 | 横浜市   |
| 神奈川県 | 鎌倉市   |
| 神奈川県 | 川崎市   |

「市区町村マスタ」テーブルと「都道府県マスタ」テーブルをリンクさせます。
[リンク項目](../../links/index.md)は「都道府県」を選択します。

レコードを新規作成し、「都道府県」項目で「東京都」、「神奈川県」のいずれかを選択してから該当する市区町村を「市区町村」項目に入力します。  

### 2.リンクの設定

![「市区町村マスタ」と「都道府県マスタ」のリンクの設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/d483c054a37a45b7b5c86fef999487f2.png)

-   「住所録」テーブルを「都道府県マスタ」テーブルとリンクさせます。  
    [リンク項目](../../links/index.md)は「都道府県」を選択します。

-   「住所録」テーブルを「市区町村マスタ」テーブルとリンクさせます。  
    [リンク項目](../../links/index.md)は「市区町村」を選択します。

### 3.項目連携の設定

1.  「住所録」テーブルの[テーブルの管理](../../index.md)を開き[エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブから「項目連携の設定」の「新規作成」をクリックしてください。

    ![「項目連携の設定」で「新規作成」をクリックする画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/1cd231f94f0b4c2997da968d1f66ca05.png)

1.  「選択肢一覧」にはリンク設定された項目が表示されるので「都道府県」、「市区町村」を「有効化」します。  
    この時、上にある項目が大分類となり、子項目の絞り込みを行う項目となるため「都道府県」が「市区町村」よりも上に設定する必要があります。

    ![項目連携の設定で「都道府県」「市区町村」の順に有効化した状態](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/a7d2bd15c87e45a5a6b3aedcb11ae12e.png)

以上で項目連携の設定は完了です。

## 操作結果

「住所録」テーブルで「都道府県マスタ」項目を選択すると、選択した内容に応じて「市区町村マスタ」には絞り込まれたデータのみが表示されます。

![「住所録」テーブルで都道府県を選んだ編集画面（1/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/3d45907e780046279766aabbba1d3684.png)

![選んだ都道府県に応じて絞り込まれた市区町村の選択肢（2/2）](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/relating-column-settings/assets/8a5a79110ed6413cb1f063187024ab45.png)

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目：分類](../editor-settings/columns/table-management-class.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [組織管理機能：インポート](../../../department-administration/dept-import.md)
-   [テーブルの管理：項目](../editor-settings/columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../editor-settings/advanced-settings/general/table-management-label-text.md)
-   [テーブル機能：レコードの一覧編集](../../../../users-guide/table/record-authoring/edit-records/table-record-editongrid.md)
-   [応用編：リンク](../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：リンク](../../links/index.md)
-   [テーブルの管理](../../index.md)
