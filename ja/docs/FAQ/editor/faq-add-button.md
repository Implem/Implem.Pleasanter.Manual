---
title: フォームにボタンを追加したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-add-button
translationKey: faq-add-button
shortname: サンプルコード
created: 2019-02-01
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使うと、ボタンを追加できます。

---

## 概要

任意の項目の後ろや、コマンドボタンエリアにボタンを追加するには、[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

## 操作方法

1.  対象のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  [テーブルの管理](../../managers-guide/manage-table/index.md)をクリックしてください。
1.  「[エディタ](../../managers-guide/manage-table/editor/index.md)」タブをクリックしてください。
1.  「[エディタの設定](../../managers-guide/manage-table/editor/editor-settings/index.md)」で「分類A」を有効化してください。
1.  [スクリプト](../../managers-guide/manage-table/scripts/index.md)タブをクリックしてください。
1.  「新規作成」ボタンをクリックしてください。
1.  「タイトル」に任意のタイトルを入力し、「[スクリプト](../../managers-guide/manage-table/scripts/index.md)」に下記のスクリプトを入力します。
1.  「出力先」は以下を参考に設定してください。
1.  「変更」ボタンをクリックしてください。
1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。
1.  任意のレコードを開くか、レコードを新規作成してください。

## サンプルコード

=== "分類Aの後ろにボタンを追加"

    ``` js title="「出力先」　「新規作成」または「編集」（または両方）" linenums="1"
    $p.events.on_editor_load = function () {
        const field = $('#' + $p.getField('ClassA')[0].id);
        const btn = '<button type="button" style="float: left;">ボタン</button>';
        field.after(btn);
    };
    ```

    ボタンデザインはHTMLのbuttonタグ標準で追加します。

    ![分類Aの後ろにHTMLのbuttonタグ標準デザインのボタンを追加](https://pleasanter.org/files/images/ja/FAQ/editor/assets/faq-add-button-01.png)

=== "コマンドボタンエリアにボタンを追加"

    ``` js title="「出力先」　「新規作成」または「編集」（または両方）" linenums="1"
    $p.events.on_editor_load = function () {
      const btn = $('<button id="NewButton">ボタン</button>')
        .button({ icon: 'ui-icon-gear' }); // (1)!
      $('#MainCommands').append(btn);
    };
    ```

    1.  ボタンのアイコンは`'ui-icon-○○'`の形式で設定します。指定文字列は以下のページを参照してください。  
        [Icons | jQuery UI API Documentation](https://api.jqueryui.com/theming/icons/)

    ボタンデザインはプリザンター準拠で追加します。

    ![コマンドボタンエリアにプリザンター準拠デザインのボタンを追加](https://pleasanter.org/files/images/ja/FAQ/editor/assets/faq-add-button-02.png)

!!! tip "「出力先」を変更したい場合"
    「出力先」を「一覧」に設定したい場合は、イベント発火スクリプトを`$p.events.on_grid_load`に変更してください。「カレンダー」や「クロス集計」を設定したい場合も、同様にイベント発火スクリプトを設定した画面のものに変更してください。

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../managers-guide/tenant-administration/tenant-logo.md)
-   [Icons \| jQuery UI API Documentation](https://api.jqueryui.com/theming/icons/)
