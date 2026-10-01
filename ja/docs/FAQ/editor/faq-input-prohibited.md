---
title: ユーザ入力操作によって別の項目を入力禁止にしたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-input-prohibited
translationKey: faq-input-prohibited
shortname: サンプルコード
created: 2019-01-31
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

---

## 概要

分類Aに"1"を入力すると、分類Bが読取専用とするような機能は[スクリプト](../../managers-guide/manage-table/scripts/index.md)による実装が必要です。サンプルコードを以下に記載します。

### 操作手順

1. テーブルを作成し、分類A、分類Bを有効にします。    
1. [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、下記のスクリプトの内容を記載してください。出力先には「新規作成」と「編集」をチェックして変更、更新します。  
1. レコードの編集画面を開き、分類Aに'1'を入力してください。

## サンプルコード

##### JavaScript

```
$(document).on('change', '#' + $p.getControl('ClassA')[0].id', function () {
    if ($p.getControl('ClassA').val() === '1') {
        $p.getControl('ClassB').attr('readonly', true);
        $p.getControl('ClassB').css('background', '#f5f5f5');
    }
});
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)