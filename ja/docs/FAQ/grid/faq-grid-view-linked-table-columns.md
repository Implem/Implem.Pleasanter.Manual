---
title: 親テーブル、子テーブルの項目を一覧画面に表示したい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-grid-view-linked-table-columns
translationKey: faq-grid-view-linked-table-columns
shortname: ''
created: 2021-03-09
updated: 2024-07-08
---

## 回答

[テーブルの管理](../../managers-guide/manage-table/index.md)－[一覧](../../managers-guide/manage-table/grid/index.md)タブで設定します。

---

## 概要

テーブルのリンク機能を使って紐付けたテーブルは、それぞれの一覧表示でタイトル以外の項目を表示することができます。 ここでは、チーム管理(親テーブル)、プロジェクト管理(子テーブル)が紐付いているものとして説明します。

## 構成

-   チーム管理、プロジェクト管理という2つの記録テーブルを作成します。  
-   プロジェクト管理(子テーブル)をチーム管理(親テーブル)にリンクします。

![プロジェクト管理をチーム管理にリンクする設定](https://pleasanter.org/files/images/ja/FAQ/grid/assets/2610394a64be4c88985e4a3eb4cad996.png)
チーム名がチーム管理のタイトルとなります。  

![チーム管理の画面。チーム名がタイトルになっている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/9b0636d3fd624a47aab3824cd890a36e.png)
プロジェクト管理では、下図のように担当チームという表示名でチーム管理のタイトル(チーム名)が選択肢として表示されます。  
![プロジェクト管理の「担当チーム」にチーム名が選択肢として表示されている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/7f617c0ab37d4a06bd794477069729bb.png)

## 使用例

通常、プロジェクト管理では親テーブルであるチーム管理のタイトル(チーム名)のみが表示されます。
![プロジェクト管理の一覧画面。チーム管理はタイトルだけが表示されている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/850c26fdb57a4d8cb8bb43eb4aca2488.png)
プロジェクト管理を開いて、テーブルの管理から一覧タブを開き、選択肢欄の上部にあるドロップダウンリストを開くと、リンクしたテーブルが表示されますので、チーム管理を選択し、窓口担当と内線番号を有効化します。  
![一覧タブでチーム管理を選び、窓口担当と内線番号を有効化するところ](https://pleasanter.org/files/images/ja/FAQ/grid/assets/b7f3000014aa40549c344e0b45500885.png)
更新ボタンをクリックして一覧画面に戻ると、チーム管理の項目である窓口担当と内線番号が表示されます。
![プロジェクト管理の一覧画面に窓口担当と内線番号が表示された状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/6b4ab2979fcb4d83888828750aaffd6d.png)
続いて同じように、親テーブルであるチーム管理を開き、一覧タブで子テーブルであるプロジェクト管理を選択し、タイトルを有効化します。
![チーム管理の一覧タブでプロジェクト管理のタイトルを有効化するところ](https://pleasanter.org/files/images/ja/FAQ/grid/assets/141841a4fa6942b783128b3e61709317.png)
チーム管理は、もともと4レコードしかありませんでしたが、子テーブルであるプロジェクト管理のタイトルを有効化したことで表示内容が変化します。
![子テーブルの項目を有効化して表示内容が変わったチーム管理の一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/4fac47d14dc44c2293d318d24fef7e7e.png)
チーム管理のそれぞれのレコードと紐付いた子レコードの項目を表示しているため、もともとのチーム管理のレコードが重複して表示されます。

![チーム管理のレコードが子レコードの数だけ重複して表示されている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/40107adef92d4b608f6f8a4e119d42f9.png)
紐付いたレコードが存在しない場合は「タイトル無し」と表示されます。  
![紐付いたレコードがない行に「タイトル無し」と表示されている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/ccd58bc2f06f4f6fbead4d480dd26f6f.png)

## 注意事項

親テーブルの一覧表示で子テーブルの項目を表示している場合、誤操作によるレコードの意図しない削除などを防ぐため、各行の左側に表示されているチェックボックスが非表示となりますので、一括更新および一括削除は使用できません。

## 関連情報

-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
