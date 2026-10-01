---
title: 項目の文字制限は？
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-column-restriction
translationKey: faq-column-restriction
shortname: ''
created: 2023-04-28
updated: 2024-04-29
---

文字の扱いはUNICODEです。  

## 文字長の制限  

大文字、小文字に関係なく1文字としてカウントされます。

* [分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目は1024文字までとなります。
* [説明](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)項目は実質無制限となります。  
（HTTPのリクエストの上限が既定では500MByteとなっているためこれ以上投入することはできません。しかし、HTTPのリクエストの上限も文字数入力換算では膨大な容量となりますので、実質無制限と捉えることができます。）

## 文字種類の制限  

* [分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[説明](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)項目に入力できる文字種に制限はありません。  
