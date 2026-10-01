---
title: スクリプトでテキストボックスの値を設定して更新ボタンを押しても保存できない
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-set-value
translationKey: faq-set-value
shortname: ''
created: 2019-01-30
updated: 2024-07-01
---

## 回答

以下のいずれかを実施してください。

1.  [$p.set](../../developers-guide/script/update-site-info/script-set.md)を使用して値を設定する。
1.  [コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)に「always-send」と指定する。

---

## 概要

スクリプトでテキストボックスの値を$('ClassA').val('変更後の値');として変更した場合、更新ボタン（登録ボタン）をクリックしても値は登録されません。これはプリザンターは画面上のすべての項目のうち、値が変更された項目のみをサーバに送信する仕組みを採用しているためであり、valメソッドで値を変更した場合は画面の見た目上は変更しますが、サーバに送信する項目とは判断されないことに由来します。ここでは、前述のようなスクリプトで画面表示の値を変更した場合でも、レコードに値を保存する方法を示します。

## 制限事項

1.  新規作成時は常に全ての画面項目が送信対象となります。
1.  always-sendを設定し一覧画面編集を行った場合、一覧表示の全てのレコードが更新対象となるため、想定していない大量レコードの更新を行う恐れがあります。

## 操作手順

以下いずれかの方法でデータを登録することができます。

1.  [$p.set](../../developers-guide/script/update-site-info/script-set.md)関数を利用する。  
    $p.set()を利用すると画面上の値変更と合わせてサーバに送信する項目として判定されます。

1.  always-sendを利用する。  
    テーブルの管理→エディタから、対象項目の[コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)に「always-send」と設定します。

    ![項目の詳細設定でコントロールCSSに always-send を設定した状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/e9ec9f701e4d43509c64828735833046.png)

    always-sendを設定した項目は、常にサーバへ送信されるため、前述のようにvalメソッドで画面表示を変更した場合でもレコードへ値を保存することが可能です。

## 関連情報

-   [$p.set](../../developers-guide/script/update-site-info/script-set.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)
