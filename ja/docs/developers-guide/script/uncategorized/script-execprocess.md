---
title: $p.execProcess
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-execprocess
translationKey: script-execprocess
shortname: $p.execProcess
created: 2024-08-21
updated: 2024-08-22
---

## 概要

指定した[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)を実行するメソッドです。

## 制限事項

1.  このメソッドは編集画面でのみ実行可能です。一覧画面での「一括処理」では実行しません。

## 構文

##### JavaScript

```
$p.execProcess(ボタン要素);
```

## 各パラメータの説明

| パラメータ名 | 説明                                               |
| :----------- | :------------------------------------------------- |
| ボタン要素   | 実行したいプロセスを実行するボタンをHTML要素で指定 |

## 使用例

下図のようなプロセスが設定されている場合を例とします。

![使用例の前提となるプロセスの設定](https://pleasanter.org/files/images/ja/developers-guide/script/uncategorized/assets/013363adaf77491c98049e2f2a7ca9f5.png)

1.  実行種別が「追加したボタン」  
    実行したいプロセスのIDを元にプロセスボタンを指定します。

    ##### JavaScript

    ```
    // プロセスID：3のプロセスを実行
    $p.execProcess($('#Process_3'));
    ```

1.  実行種別が「作成または更新」
    実行したいプロセスの画面種別が「新規」の場合は「#CreateCommand」、「編集」の場合は「#UpdateCommand」と指定します。

    ##### JavaScript

    ```
    // プロセスID：2のプロセスを実行
    $p.execProcess($('#UpdateCommand'));
    ```

3.  プロセスの詳細設定－「OnClick」に直接記述
    「$(this)」と指定します。
    下図は独自実装のスクリプト（myFunc関数）を実行後にプロセスを実行する例です。

    ![プロセスの詳細設定の「OnClick」に記述した例](https://pleasanter.org/files/images/ja/developers-guide/script/uncategorized/assets/20dad673f9ce4c41baa98da2c65dbf43.png)

## プロセスの実行条件

本メソッドを使用する場合は対象のボタンがHTML要素上に存在していることが条件となります。したがって以下ケースの場合はスクリプトを実行してもプロセス処理は実行しません。

1.  プロセスの[条件](../../../FAQ/editor/faq-condition-mode-range.md)を満たさないボタンを指定した場合
1.  実行種別が「作成または更新」のプロセスに対して「 $p.execProcess($('#Process_1'))」のようにプロセスボタン要素を指定した場合
1.  サーバスクリプト[elements.DisplayType](../../server-script/elements/server-script-elements-display-type.md)で該当ボタンを「1:無し」にした場合（2:無効、3:非表示の場合はプロセス処理実行します）

## 関連情報

-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [開発者ガイド：サーバスクリプト：elements.DisplayType](../../server-script/elements/server-script-elements-display-type.md)
