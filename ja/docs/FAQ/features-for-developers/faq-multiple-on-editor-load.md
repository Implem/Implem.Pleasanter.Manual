---
title: $p.events.on_editor_loadを複数設定できるようにしたい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-multiple-on-editor-load
translationKey: faq-multiple-on-editor-load
shortname: ''
created: 2020-03-02
updated: 2024-07-08
---

## 回答

以下いずれかの方法で実現できます。
1. 実行したい処理を配列に追加し、$p.events.on_editor_loadで配列に格納した処理を順次呼び出す。
1. 実行したい処理を1つのファンクションとして定義し、$p.events.on_editor_loadで順次ファンクションを呼び出す。

---

## 概要

複数のスクリプトファイルに渡って$p.events.on_editor_loadを複数書くとスクリプトが上書きされてしまい、一番最新のものしか動作しなくなります。回避策として以下の２つの方法があります。
1. 実行したい処理を配列に追加し、$p.events.on_editor_loadで配列に格納した処理を順次呼び出す。
1. 実行したい処理を1つのファンクションとして定義し、$p.events.on_editor_loadで順次ファンクションを呼び出す。

なお、$p.events.on_editor_loadの他、$p.events.on_grid_loadやその他[イベント発火スクリプト](../../developers-guide/script/events/script-events-after-send.md)について同様の現象が発生しますので、本内容で回避可能です。

### 1. 実行したい処理を配列に追加し、$p.events.on_editor_loadで配列に格納した処理を順次呼び出す

## サンプルコード

##### JavaScript

```
//配列を定義
$p.events.on_editor_load_arr = [];
```

##### JavaScript

```
//処理1を追加
$p.events.on_editor_load_arr.push(function() {
    alert("test1");    //任意の処理
});
```

##### JavaScript

```
//処理2を追加
$p.events.on_editor_load_arr.push(function() {
    alert("test2");    //任意の処理
});
```

##### JavaScript

```
//実行
$p.events.on_editor_load = function() {
    for (let i = 0; i < $p.events.on_editor_load_arr.length; i++) {
        $p.events.on_editor_load_arr[i] ();
    }
}
```

プリザンターの[スクリプト](../../managers-guide/manage-table/scripts/index.md)には以下のように登録します。
![スクリプトの一覧。ID=1 から ID=4 まで登録した状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/8707ed5134484092867fa573d007c21d.png)
ID=1で「配列の定義」のスクリプト、ID=4に「実行」のスクリプトを登録します。ID=2、ID=3には実行したい処理を追加するスクリプトをそれぞれ登録します。この例では2つの処理を追加していますが、ID=1、ID=4の間に記載することでいくつでも処理を追加することができます。

### 2. 実行したい処理を1つのファンクションとして定義し、$p.events.on_editor_loadで順次ファンクションを呼び出す

## サンプル

##### JavaScript

```
//処理1を定義
$p.ex.myFunc1 = function() {
    alert("test1");    //任意の処理
}
```

##### JavaScript

```
//処理2を定義
$p.ex.myFunc2 = function() {
    alert("test2");    //任意の処理
}
```

##### JavaScript

```
//実行
$p.events.on_editor_load = function() {
    $p.ex.myFunc1();
    $p.ex.myFunc2();
}
```

プリザンターの[スクリプト](../../managers-guide/manage-table/scripts/index.md)には以下のように登録します。
![スクリプトの一覧。ID=1 から ID=3 まで登録した状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/716cc574030545e38267d38edcb6b825.png)
ID=1,2で定義したファンクションのスクリプトを登録し、ID=3で「実行」のスクリプトを登録します。この例では2つの処理を追加していますが、ID=3の前に記載することでいくつでも処理を追加することができます。

