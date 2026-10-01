---
title: マークダウン記法を用いた記述方法を教えてほしい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-markdown
translationKey: faq-markdown
shortname: ''
created: 2020-09-09
updated: 2026-01-19
---

## 回答

以下の「記述方法」を参照してください。

---

## 概要

プリザンターでは、[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[コメント項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)や、サイトとテーブルの各[ガイド](../../users-guide/site/site-guide.md)、[Wiki](../../users-guide/wiki/index.md)の記載などでマークダウン記法を使用できます。

以下の「記述方法」の内容をコピーし、[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[コメント項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)などに貼り付けてください。  

### 記述方法

````md
[md]

# 見出し

# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6

見出し1
===

見出し2
----

# 改行と段落

## 改行

マークダウン記法を使用して、テキストのスタイリングを行うことができます。
コメント項目や内容項目、説明項目でマークダウンを使用することができ、エディタおよび一覧画面でスタイリングした結果を表示できます。

## 段落

マークダウン記法を使用して、テキストのスタイリングを行うことができます。

コメント項目や内容項目、説明項目でマークダウンを使用することができ、エディタおよび一覧画面でスタイリングした結果を表示できます。

# 引用

> 吾輩は猫である。名前はまだない。
> > 吾輩は猫である。名前はまだない。
> ```js
> alert("プリザンター");
> ```
> |Heading|Heading|
> |:--|:--|
> |Item|Item|

# リスト

## 順序なしリスト

* 順序なしリスト
    * 入れ子
    * 入れ子
        * さらに入れ子
* 順序なしリスト

## 順序付きリスト

1. 順序付きリスト
    1. 入れ子
    1. 入れ子
        1. さらに入れ子
1. 順序付きリスト

## チェックリスト

- [x] 企画・構想
- [ ] 選定・設計

# テーブル

|左揃え|中央揃え|右揃え|
|:--|:-:|--:|
|オープンソース・ローコード・プリザンター|ローコード・ローコード・プリザンター|プリザンター・ローコード・プリザンター|

# 画像

挿入したい箇所にカーソルを置き、コピー＆貼り付けしてください。

# コードブロック

```js
// 期限付きテーブルのスクリプト
let sampleApiModel = items.NewIssue();
sampleApiModel.Title = 'プリザンターの導入方法について';

items.Create(123, sampleApiModel);
// ブラウザのコンソールに作成したレコードのIDを出力
context.Log(sampleApiModel.IssueId);
```

```json
{
    "Enabled": false,
    "AttachmentExcludedExtensions": [
        ".exe",
        ".dll"
    ]
}
```

```diff
 {
-    "Enabled": false,
+    "Enabled": true,
     "AttachmentExcludedExtensions": [
         ".exe",
         ".dll"
     ]
 }
```

# 水平線

___

***

___

- - -

# インライン書式

***Bold italic***

**Bold**

*Italic*

~Strike~

`Inline Code`

[Google](https://www.google.com/)

[Google]

[Google]: https://www.google.com/

\\100
````

## 表示

![サンプルのマークダウン記法を表示した結果](https://pleasanter.org/files/images/ja/FAQ/others/assets/686a54602f0047bdab94c2e7c4140bcb.png)