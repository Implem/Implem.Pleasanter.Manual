---
title: $p.set
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-set
translationKey: script-set
shortname: $p.set,AddResponse
created: 2019-08-10
updated: 2023-06-01
---

## 概要

画面上の値変更と$p.dataへの格納を同時に行うことができるメソッドの説明をします。スクリプトでテキストボックスなどの値を変更する場合は$('#Results_ClassA').val('変更後の値');のように値を変えても更新されません。これはプリザンターのクライアント側の変数である「$p.data」にユーザが変更した値のみが格納され、postする仕様となっている為です。

## 構文

##### JavaScript

```
$p.set($('変更したいフォームのid名'), '変更後の値')
```    

## 使用例

以下のサンプルコードをプリザンターのスクリプトへ設定すると、編集画面で「更新」ボタンをクリックしたときにタイトル項目に[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)の値が設定された上で更新されます。

##### JavaScript

```
$p.events.before_send_Update = function () {
    $p.set($p.getControl('Title'), 'タイトル')
}
```