---
title: 選択された内容によって入力項目の色を変える
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-change-the-color-according-to-the-selected-value
translationKey: faq-change-the-color-according-to-the-selected-value
shortname: ''
created: 2020-04-07
updated: 2024-07-08
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

---

## 概要

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用すると、分類項目で選択した内容に応じて、入力項目の色を変更できます。

## 操作手順

1.  「記録テーブル」を作成してください。
1.  「[テーブルの管理](../../managers-guide/manage-table/index.md)」画面で「分類A」「数値A」「数値B」を有効化してください。
1.  [スクリプト](../../managers-guide/manage-table/scripts/index.md)を「新規作成」し、以下のサンプルコードを入力してください。  
    「出力先」には「新規作成」と「編集」選択してください。

    ``` js title="出力先は「新規作成」と「編集」" linenums="1"
    $(document).on(
        'change',
        '#' + $p.getControl('ClassA')[0].id,
        function () {
            const myClassA = $p.getControl('ClassA').val();
            const myCssBlue = {
                'borderColor': 'blue',
                'background': '#f0f8ff'
            };
            const myCssDefault = {
                'borderColor': '#c0c0c0',
                'background': 'white'
            };
            switch (myClassA) {
                case 'A':
                    // 数値Aに対する処理
                    $p.getControl('NumA').css(myCssBlue);
                    // 数値Bに対する処理
                    $p.getControl('NumB').css(myCssDefault);
                    break;
                case 'B':
                    // 数値Bに対する処理
                    $p.getControl('NumB').css(myCssBlue);
                    // 数値Aに対する処理
                    $p.getControl('NumA').css(myCssDefault);
                    break;
                default:
                    // 数値Aに対する処理
                    $p.getControl('NumA').css(myCssDefault);
                    // 数値Bに対する処理
                    $p.getControl('NumB').css(myCssDefault);
                    break;
            }
        }
    );
    ```

1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

## 実行結果

分類Aの選択により、数値Aと数値Bの色が以下のように変わります。

=== "「A」を選択した場合"

    数値Aの色が青に変わります。

    ![分類Aで「A」を選び、数値Aの色が青に変わった状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/77abc85fcb004ac4a277a65799f39ba2.png)

=== "「B」を選択した場合"

    数値Bの色が青に変わります。

    ![分類Aで「B」を選び、数値Bの色が青に変わった状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/d300108703e64bb4999c31a5b233dd2b.png)

=== "「A」または「B」以外を選択した場合"

    数値Aと数値Bの色が元に戻ります。

    ![「A」「B」以外を選び、数値Aと数値Bの色が元に戻った状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/cb031599e1dc4075abc9d5747ceeb2f2.png)

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
