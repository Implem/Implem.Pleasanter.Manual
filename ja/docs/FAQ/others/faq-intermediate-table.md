---
title: 多対多の関係を表現したい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-intermediate-table
translationKey: faq-intermediate-table
shortname: ''
created: 2021-03-09
updated: 2024-07-08
---

## 回答

以下のどちらかの機能を利用してください。
1. [複数選択](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)を設定する
1. 中間テーブルを作成する

---

## 概要

[リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)機能を用いた場合、通常子テーブルからは親テーブルは１つしか選択できず、１（親）：N（子）のとなります。N（親）：N（子）の多対多の関係を表現したい場合は以下の設定を実施してください。

## 方法１ リンクの複数選択を利用する。

[複数選択](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)の設定をすることで、子テーブルから親テーブルを複数選択することができます。

## 方法２ 中間テーブルを用いて多対多の関係性を表現する。

複数のメンバーが複数のプロジェクトを担当している関係性を、中間テーブルを用いて紐付ける設定例を示します。

![中間テーブルを使って多対多の関係を表した図](https://pleasanter.org/files/images/ja/FAQ/others/assets/b8abc44ad3094dd59a79ba3fdf8368cc.png)

## 構成

-   メンバー、担当プロジェクト、プロジェクトの3つの記録テーブルを作成します。  
-   担当プロジェクト(子テーブル)を、メンバー(親テーブル)、プロジェクト(親テーブル)にリンクします。  

※担当プロジェクトが中間テーブルとなります。  
![担当プロジェクトをメンバーとプロジェクトにリンクした構成の図](https://pleasanter.org/files/images/ja/FAQ/others/assets/7f9db7b004784bcc90d37b9ba2da6e09.png)

## 使用例

担当プロジェクトでは、リンクされたメンバー、プロジェクトの両テーブルの項目を入力できます。  
![担当プロジェクトの編集画面。メンバーとプロジェクトの項目を入力できる](https://pleasanter.org/files/images/ja/FAQ/others/assets/01a02819461a4c4987a0b41f2ea2e582.png)
メンバーの誰がどのプロジェクトを担当しているか、対象のプロジェクトは誰が担当しているのか、を紐づけて登録することができます。  
![メンバーとプロジェクトの担当関係が登録されている画面](https://pleasanter.org/files/images/ja/FAQ/others/assets/9aaf5b432f3d4f9d87f9a6f8c51a2e55.png)

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
