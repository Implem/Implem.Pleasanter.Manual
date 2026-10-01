---
title: 操作方法
category: スマートデザイン：一覧
order: '3000'
status: ''
parts: ''
urlstring: smart-design-grid
translationKey: smart-design-grid
shortname: スマートデザイン
created: 2025-03-28
updated: 2026-02-10
---

## 概要

[スマートデザイン](../editor/smart-design-editor.md)では一覧画面のレイアウトをドラッグ＆ドロップで簡単に編集することができます。
また、各項目の表示に関するオプションをダイアログで個別に変更することも可能です。
![スマートデザインで一覧画面のレイアウトを編集している画面](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/1b85259bfba844e5a12a5b5ada245035.png)

## 制限事項

1. スマートデザインの一覧画面で編集できる項目は【全般】で有効化されている項目のみです。 [追加したタブ](../../../managers-guide/manage-table/editor/tab-settings/index.md)で有効化している項目に関しては追加できません。
1. スマートデザインの一覧画面では、リンク先の項目を編集することはできません。スマートデザイン上では表示されませんが、設定は保持され、一覧で表示されている項目の配置のみが変更されます。
1. 「[スマートデザイン：概要](../smart-design-overview.md)」の制限事項も参照ください。

## 画面の説明

### ドラッガブルエリア

![一覧のドラッガブルエリア。左の項目一覧と右のレイアウトエリアに番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/ddf218323a1f46f59962025847ebc97c.png)

#### <span class="pl-callout">➊項目一覧</span>

画面左の項目を選択し右のレイアウトエリアにドラッグ＆ドロップすることで一覧に配置することが可能です。  
項目のグループ名はアコーディオンボタンになっており展開することで配置可能な項目が展開されます。  
各グループの詳細は以下の通りです。

|項目グループ名|説明|
|:--|:--|
|基本項目|サイトを構成する基本的な項目です。 |
|追加項目|分類/数値/日付/説明/チェック/添付ファイルなどA-Zで終わる項目です。|

####  <span class="pl-callout">➋レイアウトエリア</span>

画面右側には、一覧画面に配置されている項目がセル型のユニットでレイアウトされます。 
配置済みの項目セルはドラッグ＆ドロップで自由に並び替えることが可能です。

### 各種項目セル

![各種項目セルと、セル上の構成要素に番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/ef8808c15fd24107b69098c0c6ab25ce.png)

|No|セル項目|説明|
|:--:|:--|:--|
|<span class="pl-callout">➊</span>|表示名|配置された項目の表示名です。|
|<span class="pl-callout">➋</span>|編集ボタン|<a href="#cell-settings-editor">セルの設定編集画面</a>を開きます。|
|<span class="pl-callout">❸</span>|設定情報|[セルの横幅](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)、[左端でスクロール固定](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)、[セル幅で文字を折り返す](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-wordwrap.md)の設定値を表示します。|
|<span class="pl-callout">➍</span>|項目グループ名|上記の[基本項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-column.md)または「追加項目」が表示されます。|

<a id="cell-settings-editor"></a>

### セルの設定編集画面

![セルの設定編集画面。各部に番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/d6ae063ad57a4046af236aa67ce10522.png)

|No|設定画面項目|説明|
|:--:|:--|:--|
|<span class="pl-callout">➊</span>|ヘッダ|項目のオリジナルのカラム名を表示。|
|<span class="pl-callout">➋</span>|閉じるボタン|設定をキャンセルし、画面を閉じます。|
|<span class="pl-callout">❸</span>|設定エリア|[セルの横幅](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)、[左端でスクロール固定](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)、[セル幅で文字を折り返す](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-wordwrap.md)の設定値を編集できます。|
|<span class="pl-callout">➍</span>|更新ボタン|編集した内容で設定を更新します。サイト（テーブル）の更新にはコマンドボタンエリアの「更新」ボタンをクリックする必要があります。|
|<span class="pl-callout">➎</span>|削除ボタン|セル型のユニットをレイアウトエリアから削除します。クリックすると、削除の確認ダイアログが表示されます。|

#### 削除の確認ダイアログ

![セル削除の確認ダイアログ。キャンセルボタンと削除ボタン](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/bf7846b9d0fb4fc686fabbafe57ea92c.png)

|No|設定画面項目|説明|
|:--:|:--|:--|
|<span class="pl-callout">➊</span>|キャンセルボタン|削除を取り消します。|
|<span class="pl-callout">➋</span>|削除ボタン|削除します。削除時点の設定値は、[エディタ](../../table/record-authoring/edit-records/table-editor.md)でリセットするまで保持されます。|

## 操作方法

### 項目の配置・並び替え

スマートデザイン起動時に現在のテーブル管理 > [一覧](../../../managers-guide/manage-table/grid/index.md)画面の構成を表示します。
![スマートデザイン起動時に表示される現在の一覧画面の構成](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/6913a7e6a1b14b77ab1dca2f84ef3781.png)
画面左の項目一覧から必要な項目をドロップ操作で一覧に配置することができ、 配置済みの項目も自由に並び替えられるので直感的に一覧画面のレイアウトを設計することが可能です。 

### 項目をレイアウトから削除

項目セルをレイアウトから削除したい場合は、削除したい項目を、ドラッグ操作で項目一覧に表示される「一覧で使用しない項目はこちらにドラッグ」にドラッグします。
※「一覧で使用しない項目はこちらにドラッグ」の文字が赤くなるのを確認して項目を離してください。  
※本機能は<a href="#cell-settings-editor">セルの設定編集画面</a>で各種項目セルを削除した場合と同じ結果を得られます。

![項目セルを「一覧で使用しない項目はこちらにドラッグ」へドラッグする操作](https://pleasanter.org/files/images/ja/users-guide/smart-design/grid/assets/1c24d880d04345c9b84cfbc3e13634dd.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.15.0以降|機能追加|
|1.5.1.0以降|[セルの横幅](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)、[左端でスクロール固定](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)、[セル幅で文字を折り返す](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-wordwrap.md)の設定機能を追加|

## 関連情報

[テーブルの管理：一覧画面：一覧画面の項目の設定](../../../managers-guide/manage-table/grid/table-management-grid-columns.md)
-   [スマートデザイン：エディタ：操作方法](../editor/smart-design-editor.md)
-   [追加したタブ](../../../managers-guide/manage-table/editor/tab-settings/index.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：セルの横幅](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-cell-width.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：左端でスクロール固定](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-sticky-on-left-edge.md)
-   [テーブルの管理：一覧画面：項目の詳細設定：セル幅で文字を折り返す](../../../managers-guide/manage-table/grid/advanced-settings/table-management-grid-wordwrap.md)
-   [テーブルの管理：項目：基本](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-column.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：一覧画面](../../../managers-guide/manage-table/grid/index.md)
-   [テーブルの管理：一覧画面：一覧画面の項目の設定](../../../managers-guide/manage-table/grid/table-management-grid-columns.md)
