---
title: 親テーブルの項目の値を子テーブルの項目に転記したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-lookup-posting
translationKey: faq-lookup-posting
shortname: リンク
created: 2019-02-18
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用します。
**NET Framework版 0.50.251 以降、.NET Core版 1.1.27 以降のバージョンでは[ルックアップ](../../users-guide/hands-on/advanced/advanced-operations-link.md)機能で実現できます。**

---

## 概要

[リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)機能で親子関係を結んでいるテーブルにおいて、親テーブルで入力された項目の値を子テーブルの項目に転記します。  
例として、[Aテーブル（親）] [Bテーブル（子）]の時、Bテーブルの「分類A」をリンク項目として、Bテーブルの「分類B」にAテーブルの「分類A」の値をセットする場合のサンプルコードを以下に記載します。（この例では、Bテーブルにスクリプトを設定します）
プリザンターでは[$p.apiGet](../../developers-guide/script/script-api/script-api-get.md)を使用すると、レコードIDを指定するだけでajaxのPOSTリクエストによる値の取得が可能です。  
※バージョン1.3.12.0以前をお使いの場合は、一部の記述内容が異なります。サンプルコード内のコメントを確認してください。

## 操作方法

1. スクリプトを設定したいテーブルを選択してレコード一覧画面を表示する
1. ナビゲーションメニューより[管理]-[テーブルの管理]を選択し、テーブルの管理画面を表示する
1. [スクリプト]タブを選択後「新規作成」ボタンを押下し、スクリプトの設定を行う
1. [タイトル](../../managers-guide/tenant-administration/tenant-logo.md)、[スクリプト](../../managers-guide/manage-table/scripts/index.md)を記述したら、「出力先」で"新規作成","編集"にチェックを付ける  
    ※[ダイアログで編集]の設定をしている場合、"一覧"にもチェックが必要です

## サンプルコード

##### JavaScript

```
//編集画面読込時のイベント
$p.events.on_editor_load = function () {
    getParentData();
}

//Bテーブルの「分類A」の値が変更されるたびに呼び出されるイベント
$(document).on('change', '#' + $p.getControl('ClassA')[0].id, function () {
    getParentData();
});

getParentData = function() {
    //Bテーブルの「分類A」に値がセットされている場合のみ、Aテーブルの指定したレコードの値を取得する
    if ($p.getControl('ClassA').val()) {
        $p.apiGet({
            //Bテーブルの「分類A」の値（レコードID）を指定
            'id': $p.getControl('ClassA').val(),
            'done': function (data) {
                //Bテーブルの「分類B」にAテーブルから取得した「分類A」の値をセット
                //※バージョン1.3.12.0以前をお使いの場合は、以下のコメント行の行頭にある//を外し、その次の行を削除してください。
                //$p.set($p.getControl('ClassB'), data.Response.Data[0].ClassA);
                $p.set($p.getControl('ClassB'), data.Response.Data[0].ClassHash.ClassA);
            },
            'fail': function (data) {
                console.log(data);
            }
        });
    } else {
        //Bテーブルの「分類A」に値がセットされていない場合、Bテーブルの「分類B」に空文字をセット
        $p.set($p.getControl('ClassB'), '');
    }
}
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [$p.apiGet](../../developers-guide/script/script-api/script-api-get.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../managers-guide/tenant-administration/tenant-logo.md)