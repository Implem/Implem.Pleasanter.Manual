---
title: 印刷時に画面下部のコマンドボタンを非表示にしたい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-hide-footer-when-printing
translationKey: faq-hide-footer-when-printing
shortname: ''
created: 2019-10-16
updated: 2024-04-29
---

## 回答

[スタイル](../../developers-guide/style/index.md)を使用してください。

---

## 概要

ブラウザの印刷機能で印刷すると、コマンドボタンエリア（画面下部のコマンドボタンとCopyright表記）が画面の途中に表示する場合があります。コマンドボタンエリアを非表示にしたい場合は[スタイル](../../developers-guide/style/index.md)で対応します。

## 操作手順

1. 対象のテーブルを開きます。  
1. 管理→テーブルの管理をクリックします。  
1. スタイルタブを開きます。  
1. 新規作成ボタンをクリックし、ダイアログを表示します。  
1. タイトルに「印刷時」等の任意のタイトルを入力します。  
1. スタイルに下記のCSSを入力します。  
1. ダイアログの変更ボタンをクリックします。  
1. 画面下部の更新ボタンをクリックします。  
1. 対象のテーブルの一覧画面等を開き、ブラウザ機能の印刷プレビューを表示し確認します。  

## サンプルコード

##### CSS  

```
@media print {
    #MainCommandsContainer {    /* コマンドボタン */
        display:none;
    }
    #Footer {   /* Copyrihgt表記 */
        display:none;
    }
}
```

## 関連情報

-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)