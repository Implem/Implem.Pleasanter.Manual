---
title: 項目の値の一部を切り取り、同レコードの別項目に転記したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-slice-posting
translationKey: faq-slice-posting
shortname: 項目の転記,転記
created: 2021-05-11
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用します。

---

## 概要

[項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の値が変更したときに、別の[項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)に値を転記したい場合は[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用します。

## 操作手順

1.  テーブルを作成してください。
1.  [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載してください。  
    出力先には「新規作成」、「編集」をチェックして更新します。
1.  [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)から、以下のサンプルコードにあわせて、分類Aと説明Aを有効化してください。
1.  分類Aの選択肢に任意の文字列を入力して更新ボタンを押してください。
1.  [+新規作成]ボタンから新たにレコードを作成してください。
1.  分類Aで任意の値を選択し、説明Aに先頭一文字が転記されることを確認してください。

## サンプルコード

``` js title="JavaScript" linenums="1"
$(document).on('change', '#' + $p.getControl('ClassA')[0].id, function(){
    // 分類Aの値を取得
    const myClassA = $p.getControl('ClassA').val();
    // 分類Aが変更されると説明Aに分類Aの先頭1文字を転記する
    // 0文字目(先頭)から1文字目を切り取る
    $p.set($p.getControl('DescriptionA'), myClassA.slice(0,1));    
});
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [テーブルの管理：項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
