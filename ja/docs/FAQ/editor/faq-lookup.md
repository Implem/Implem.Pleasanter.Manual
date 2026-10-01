---
title: ある項目の値を特定の値に変更したときに別の項目の値を変更する
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-lookup
translationKey: faq-lookup
shortname: ''
created: 2020-01-30
updated: 2026-04-13
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)で実現できます。

---

## 概要

プリザンターの編集画面上にて、ある項目を特定の値に変更したときに、別の項目の値を変更するサンプルコードを以下に示します。

## 操作方法

1.  テーブルを作成してください  
1. [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトのいづれかの内容を記載してください。出力先には「編集」をチェックして更新します。  
1. [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)から、以下のサンプルコードにあわせて、数値Aまたは分類A、チェックA項目を有効化してください。
1.  [+新規作成]ボタンから新たにレコードを作成してください。
1.  3で作成したレコードの変更画面を開き、[状況項目]を”完了”に設定、[分類A]を"終了"と入力し、[更新]ボタンを押下してください。

## スクリプト

### 1. 状況項目を「完了」に変更した際に数値A項目の値を「1」に設定する

##### JavaScript

```
$p.on('change', 'Status', function() {
    //状況項目が「完了」に変更されると数値A項目に1を自動入力する
    if ($p.getControl('Status').val() === '900') {
        $p.set($p.getControl('NumA'), 1);
    }
});
```

### 2. 分類A項目を「終了」に変更した際に数値A項目の値を「10」に設定する

##### JavaScript

```
$p.on('change', 'ClassA', function() {
    //分類A項目が「終了」に変更されると数値A項目に10を自動入力する
    if ($p.getControl('ClassA').val() === '終了') {
        $p.set($p.getControl('NumA'), 10);
    }
});
```

### 3. 分類A項目を「終了」に変更した際にチェックA項目をチェックONにする

##### JavaScript

```
$p.on('change', 'ClassA', function() {
    //分類A項目が「終了」に変更されるとチェックA項目をチェックONにする
    if ($p.getControl('ClassA').val() === '終了') {
        $p.set($p.getControl('CheckA'), true);
    }
});
```

### 4. ラジオボタン（分類A）が変更された際に分類Bに「ラジオボタンが変更されました」という文字列を設定する

##### JavaScript

```js
$(document).on('change', 'input[name="Results_ClassA"]', function () {
    // 分類Bに「ラジオボタンが変更されました」という文字列を設定する
    $p.set($p.getControl('ClassB'), 'ラジオボタンが変更されました')
});
```