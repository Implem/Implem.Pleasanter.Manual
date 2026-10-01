---
title: 親レコードからの子レコード作成時に特定の項目にのみ親レコードの値を設定する
category: エディタ
order: '10700'
status: ''
parts: ''
urlstring: table-management-select-new-link
translationKey: table-management-select-new-link
shortname: ''
created: 2023-04-26
updated: 2024-04-09
---

## 概要

`SelectNewLink`の設定により、同じ親を持つ「[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)」を設定している親レコードの「リンクしたアイテムの作成」から子レコードを新規作成した際に、特定の項目にのみ親レコードの値を設定することができます。

## 制限事項

-   [分類項目](../../../columns/table-management-class.md)のみ使用できます。

## 前提条件

-   設定を行うには「サイトの管理権限」が必要です。

## 操作手順

「[エディタ](../../../../index.md)」タブで「[分類項目](../../../columns/table-management-class.md)」の「詳細設定」を開き、「[選択肢一覧](index.md)」にJSON形式でリンク設定を記述します。

## 設定内容

|No|パラメータ|設定値|
|:----|:----|:----|
|1|SelectNewLink|true/false|

## 設定例

以下の例では、子テーブルの消耗品①（分類A）、消耗品②（分類B）の「[選択肢一覧](index.md)」に親テーブル（サイトID 123）へのリンクを設定しています。`SelectNewLink`の設定で、親レコードの「リンクしたアイテムの作成」の作成ボタンをクリックした後の新規作成画面で表示される消耗品①（分類A）、消耗品②（分類B）の値の自動設定が切り替わります。

### 通常のリンク設定の場合

消耗品①、②の「[選択肢一覧](index.md)」に対して、`"[[123]]"`のように`SelectNewLink`が未設定または無効の場合は、以下のように表示されます。

``` text title="選択肢一覧"
[[123]]
```

#### 親レコードの作成ボタンをクリックした後の新規作成画面

![SelectNewLink が未設定のとき、親レコードから開いた新規作成画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/970335f0dfd04638b85b49e9b0d0b441.png)

### `SelectNewLink`が有効の場合

消耗品②のみ`SelectNewLink`を有効化した場合は以下のように表示されます。

``` json title="選択肢一覧" linenums="1"
[
    {
        "SiteId": 123,
        "SelectNewLink": true
    }
]
```

#### 親レコードの作成ボタンをクリックした後の新規作成画面

![消耗品②のみ SelectNewLink を有効にしたときの新規作成画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/assets/36574abfb6ae478b93c98bc826decf76.png)

## 関連情報

-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
