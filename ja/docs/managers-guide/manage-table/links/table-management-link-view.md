---
title: リンク
category: リンク
order: '0'
status: ''
parts: ''
urlstring: table-management-link-view
translationKey: table-management-link-view
shortname: リンクレコード一覧の設定,リンク
created: 2019-12-05
updated: 2025-07-08
---

## 概要

「[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)」機能を使用してリンクした「レコード」を「[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)」上に一覧表示する際の表示「[項目](../editor/editor-settings/columns/index.md)」を設定することができます。

## 制限事項

1. 「[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)」している他のテーブルの項目は設定できません。
1. 「有効化」した項目が１つもない場合は、リンクしているテーブルの編集画面上に表示しません。

## 前提条件

1. 「サイトの管理権限」が必要です。

## 操作手順

1. 「[リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)」している対象の「[テーブル](../../../users-guide/table/index.md)」を開いてください。
1. 「管理」メニューから「[テーブルの管理](../index.md)」をクリックしてください。
1. 「リンク」タブを開いてください。
1. 「選択肢一覧」のリストから対象の「[項目](../editor/editor-settings/columns/index.md)」を選択してください。
1. 「有効化」ボタンをクリックしてください。
1. 「有効化」した「項目」が「現在の設定」の一番下に追加されるので「上」、「下」ボタンを使用して、表示する位置を調整してください。Ctrlキーを押しながら「上」、「下」ボタンをクリックすると「項目」が最上段、最下段に移動します。
1. 不要な「項目」は「現在の設定」から選択して「無効化」ボタンをクリックしてください。
1. リンクテーブルに表示可能なレコードの最大件数を「表示件数」で指定してください。既定値の「0」とした場合、無制限となります。
1. 画面下部の「更新」ボタンをクリックしてください。

### 「表示件数」の設定可能範囲

「表示件数」の設定可能範囲は既定では「0～100」です。この範囲は[General.json](../../../setup/parameters/general.json.md)の"LinkPageSizeMin" および "LinkPageSizeMax" で変更が可能です。

## 動作イメージ

リンクしたレコードに表示する項目と「表示件数」を設定します。
![テーブルの管理の「リンク」タブの設定画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/links/assets/1d83bdbc08fb4491b57d27ebd8a8cc65.png)

リンクしているテーブルの編集画面で下図のように表示されます。
![設定した項目が表示された、リンクしているテーブルの編集画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/links/assets/9f26a4d796e5482c9b9d7649984eb35e.png)

## リンクテーブルにビューを割り当てる

「[既定のビュー](../grid/table-management-default-view.md)」にあらかじめ作成しておいたビューを設定することで、リンクテーブルに表示するレコードの並び替えや絞り込みができます。
![リンクテーブルの「既定のビュー」を設定する画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/links/assets/0a2603edcfc1455fab422920106497bf.png)

リンクテーブルに適用されるビューの設定内容

|タブ|設定項目|説明|
|-|-|-|
|一覧|一覧の設定|設定した内容で項目が表示されます。「[既定のビュー](../grid/table-management-default-view.md)」選択時は、「リンク」タブの「一覧の設定」よりもビューの設定が優先されます。|
|フィルタ|フィルタ条件|設定した内容でレコードがフィルタされます。|
|ソータ|ソート条件|指定した内容でレコードがソートされます。|

### 「既定のビュー」設定時の表示例

「[既定のビュー](../grid/table-management-default-view.md)」に下記のソート条件、フィルタ条件を設定したビューを選択した場合の表示例です。

- ソート条件：受注予定日(降順)
- フィルタ条件：状況「受注」

![「既定のビュー」でソートとフィルタを適用したリンクテーブルの表示例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/links/assets/668de19703a942c5b2bd8734a44b9990.png)
