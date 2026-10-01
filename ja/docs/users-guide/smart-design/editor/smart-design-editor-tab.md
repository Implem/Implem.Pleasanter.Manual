---
title: タブ
category: スマートデザイン：エディタ
order: '0'
status: ''
parts: ''
urlstring: smart-design-editor-tab
translationKey: smart-design-editor-tab
shortname: ''
created: 2026-03-16
updated: 2026-04-14
---

## 概要

[スマートデザイン](smart-design-editor.md)のタブでは、以下の操作をドラッグ＆ドロップで直感的に実行できます。

　**【1】タブの新規作成**  
　**【2】タブの並べ替え**  
　**【3】タブの表示名変更**
　**【4】タブの削除**
　**【5】各タブでの項目の有効化と無効化**  
　**【6】タブ間の項目移動**

本ページでは上記**【1】**～**【4】**について説明します。**【5】**～**【6】**については「スマートデザイン：エディタ：操作方法」を確認してください。
上記の**【1】**～**【6】**は、[テーブルの管理](../../../managers-guide/manage-table/index.md)の[エディタ](../../table/record-authoring/edit-records/table-editor.md)でも操作できます。

![スマートデザインのタブ領域。表示名や項目数など6か所に番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/66969e607cfb4d6ebf8af9c881a7161e.png)

<table>
<tr>
    <th>No.</th>
    <th>情報</th>
    <th>説明</th>
</tr>
<tr>
    <th class="pl-callout">➊</th>
    <td>表示名</td>
    <td>タブの表示名です。</td>
</tr>
<tr>
    <th class="pl-callout">➋</th>
    <td>項目数</td>
    <td>タブに配置した項目の数を表示します。</td>
</tr>
<tr>
    <th class="pl-callout">➌</th>
    <td>タブの編集ボタン</td>
    <td>タブをポイントしたときに表示される歯車型のボタンです。<br>クリックすると「タブの編集」画面が開きます。</td>
</tr>
<tr>
    <th class="pl-callout">➍</th>
    <td>タブハンドル</td>
    <td>タブをドラッグ＆ドロップ操作で移動・削除可能なタブに表示されます。<br>「全般」タブには表示されず、移動も削除もできません。</td>
</tr>
<tr>
    <th class="pl-callout">➎</th>
    <td>タブの新規作成ボタン</td>
    <td rowspan="2">「＋」表示のときにクリックすると、タブを追加できます。<br>追加したタブをドラッグすると「－」表示に変わります。<br>「－」表示のときに削除したいタブをドロップすると削除できます。</td>
</tr>
<tr>
    <th class="pl-callout">➏</th>
    <td>タブの削除ボタン</td>
</tr>
</table>

## 制限事項

1. 「テーブルの管理：エディタ：タブ」の[制限事項](../../../products-info/limitations-database.md)を確認してください。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作手順

#### 【1】タブの新規作成

タブを新規作成できます。新規作成できるタブの数に制限はありません。

![タブを新規作成する操作を示した画面](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/1abfc76a23e8428ca6150e7dbb37019a.png)

1. 「タブの新規作成」ボタンをクリックしてください。
1. [表示名](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)を入力し、「追加」ボタンをクリックしてください。
1. 既存のタブの右端（「変更履歴の一覧」タブの左側）に、新規作成したタブが追加されます。

タブの数が増え、表示がウィンドウ幅に収まらなくなると、タブの下に横スクロールバーが表示されます。  
隠れたタブを表示したい場合や、タブの新規作成ボタンを利用したい場合は、横スクロールバーを使ってください。

![タブが増えてタブの下に横スクロールバーが表示された状態](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/47f3381d7eb8415985d4abf9258159a6.png)

1つのタブの最大表示幅は300ピクセルです。  
この幅に入りきらないタブ名は、以下のように省略表示されます。

![幅に収まらないタブ名が省略表示された例](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/8a5659701af24457ae42eea6298f3af2.png)

※レコードの編集画面では、タブ名を省略せずに表示します。長すぎるタブ名を付けると、ウィンドウ幅を狭くした場合に表示が切れて見えることがあります。

#### 【2】タブの並べ替え

タブハンドル付きのタブはドラッグ＆ドロップで並べ替えることができます。

![タブをドラッグ＆ドロップで並べ替える操作](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/af9510b4e18a4183bbd30bd406c6b185.png)

-   「全般」タブより左へは移動できません。  
-   「全般」タブは移動できません。

#### 【3】タブの表示名変更

「全般」タブ、新規作成したタブの表示名を変更できます。複数のタブに同じ表示名を付与できます。

1. タブの編集ボタン（歯車アイコン）をクリックするか、タブをダブルクリックしてください。  
   ![タブに表示された歯車型のタブの編集ボタン](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/6408601dea754f96beac388c8baae8c7.png)
1. タブの編集画面が開きます。[表示名](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)を任意の文字列に変更し、「更新」ボタンをクリックしてください。  
   ![タブの編集画面。表示名を変更して更新できる](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/86dc5fbb26dd408cae9a772923ff9e29.png)
1. コマンドボタンエリアの「更新」ボタンをクリックしてください。

#### 【4】タブの削除

##### ①タブの編集画面を使う方法

タブハンドル付きのタブは削除することができます。削除したタブは元に戻せません。

1. タブの編集ボタン（歯車アイコン）をクリックするか、タブをダブルクリックしてください。  
   ![削除するタブに表示された歯車型のタブの編集ボタン](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/fefb34ba65ef4bc191b2b62770eec531.png)
1. タブの編集画面が開きます。「 削除」ボタンをクリックしてください。
   ![タブの編集画面の「削除」ボタン](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/1f88d5fc5bf24b12924f50c308f3ad50.png)
1. 「 項目」を配置しているタブを削除しようとすると、以下のような画面が表示されます。削除して構わなければ「 削除」ボタンをクリックしてください。配置済みの項目はタブの削除時にリセットされるため注意してください。  
   ![項目を配置したタブを削除するときの確認画面](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/fe802a889aba419fbbfef8611adc91e8.png)  
   「 項目」を配置していないタブを削除しようとすると、以下のような画面が表示されます。  削除して構わなければ「 削除」ボタンをクリックしてください。  
   ![項目を配置していないタブを削除するときの確認画面](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/229dedf5aabc4c938e0d59c20797f106.png)
1. コマンドボタンエリアの「更新」ボタンをクリックしてください。

##### ②タブの削除ボタンへドラッグ＆ドロップする方法

タブハンドル付きのタブを「タブの削除」ボタンへドラッグ＆ドロップすることでもタブを削除できます。

1. タブハンドル付きのタブを「タブの削除」ボタンへドラッグ＆ドロップしてください。  
1. 「 項目」を配置している場合は、削除の確認画面が表示されます。削除して構わなければ「 削除」ボタンをクリックしてください。配置済みの項目はタブの削除時にリセットされるため注意してください。  
   「 項目」を配置していない場合は、確認ダイアログは表示されず、そのまま削除されます。
1. コマンドボタンエリアの「更新」ボタンをクリックしてください。  

   ![タブを「タブの削除」ボタンへドラッグ＆ドロップする操作](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/f59840c52c244126851c11ae1fc9d476.png)

## 対応バージョン

| 対応バージョン | 内容     |
| -------------- | -------- |
| 1.5.3.0 以降   | 機能追加 |

## 関連情報

-   [スマートデザイン：エディタ：操作方法](smart-design-editor.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [データベースによる制限事項](../../../products-info/limitations-database.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)