---
title: CodeDefiner実行したときに「Implem.CodeDefinerは動作を停止しました」というエラーが表示される
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-sql-server-delete-fulltext-indexes
translationKey: faq-sql-server-delete-fulltext-indexes
shortname: ''
created: 2020-08-13
updated: 2023-01-05
---

## 回答

Itemsテーブルのフルテキストインデックスを削除してください。

---

## 概要

プリザンターのバージョンアップ作業でCodeDefinerを実行した際に以下のエラーが発生した場合はItemsテーブルのフルテキストインデックスを削除した後で再度CodeFefinerを実行してください。

```
<ERROR> <>c.<Configure>b__0_0: [7613] インデックス  
 'Pk_3b080bff5d141a4f986ea165c2ac266b8843b41749ad8a162ea5310ff5c61ac3' を削除できません。このインデックスにより、テーブルまたはインデックス付きビュー 'Items' にフルテキスト キーが設定されています。  
制約を削除できませんでした。以前のエラーを調べてください。
```  

## 操作手順

SQL Server Management Studio (SSMS) を使って、Implem.Pleasanter内のitemsテーブルのフルテキストインデックスを削除します。  
1. データベースサーバ直下の「データベース」をクリック  
2. 「Implem.Pleasanter」をクリック  
3. テーブル内の「dbo.Items」を右クリックし、「フルテキストインデックス」→「フルテキストインデックスの削除」を選択  
4. フルテキストインデックスを削除しますか？→「OK」をクリック  

![SQL Server Management Studio でフルテキストインデックスを削除するところ](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/e736fc678b9c4adfb54c33b4cc7a743c.png)  

CodeDefinerを実行することでフルテキストインデックスが再構築されます。  