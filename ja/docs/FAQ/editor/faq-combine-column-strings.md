---
title: 複数の項目の値を結合し1つの項目に自動入力したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-combine-column-strings
translationKey: faq-combine-column-strings
shortname: ''
created: 2019-01-30
updated: 2024-11-14
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

---

## 概要

任意の複数項目に設定された同じ型の値を結合(数値の場合は足し算)を行い、その値を指定項目に入力したい場合は[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用します。

## 操作方法

1. 記録テーブルを作成します。
1. 分類A、分類B、分類Cを有効にします
1. 以下のスクリプトを[スクリプト](../../managers-guide/manage-table/scripts/index.md)の新規作成で、出力先を「新規作成」、「編集」にチェックを付けて更新してください。  

## サンプルコード

##### JavaScript

```　
$(document).on('change', '#' + $p.getControl('ClassA')[0].id + ', #' + $p.getControl('ClassB')[0].id, function () {
    const A = $p.getControl('ClassA').val();
    const B = $p.getControl('ClassB').val();

    $p.set($p.getControl('ClassC'), A + B);
})
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)