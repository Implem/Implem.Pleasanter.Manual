---
title: 一覧画面を開いた時にビューを使わずにフィルタを有効にしたい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-set-default-filter
translationKey: faq-set-default-filter
shortname: ''
created: 2020-04-22
updated: 2024-07-01
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

---

## 概要

ビューを使用せず、フィルタの検索条件を入力した状態で一覧画面を表示したい場合は、[スクリプト](../../managers-guide/manage-table/scripts/index.md)で実現可能です。

## 操作手順

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトを記載してください。  出力先には[一覧](../../managers-guide/manage-table/grid/index.md)をチェックして更新します。  

### 例1.「未完了」で絞り込む場合

##### JavaScript

```javascript
$(function () {
    // フィルタ「未完了」のidは”ViewFilters_Incomplete”
    $p.set($('#ViewFilters_Incomplete'),'1');
    $p.send($('#ViewFilters_Incomplete'));
});
```

#### 結果

![スクリプトにより「未完了」で絞り込まれた状態で開いた一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/837821f05bfc479cbaf702cbf749282b.png)

### 例2.[状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を「未着手(100)」、「実施中(200)」で絞り込む場合

##### JavaScript

```javascript
$(function () {
    // フィルタ「状況」のidは”ViewFilters__Status”
    $p.set($('#ViewFilters__Status'),'["100","200"]');
    $p.send($('#ViewFilters__Status'));
});
```

#### 結果

![状況が「未着手」と「実施中」で絞り込まれた状態で開いた一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/a5c26a39955c49f697527413b1a5a745.png)

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
-   [テーブルの管理：項目：状況](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)