---
title: ビュー
category: ビュー
order: '1'
status: ''
parts: ''
urlstring: table-management-view-old
translationKey: table-management-view
shortname: ビュー
created: 2019-12-05
updated: 2024-05-24
---

![ナビゲーションメニューの「管理」から「テーブルの管理」を選ぶところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/3fbe8ff097b44651a42a4412f99b333b.png)
該当のテーブルを開いた状態でナビゲーションメニューより「管理」－[テーブルの管理](../index.md)をクリックしてください。  
※サイトの管理権限がないユーザには表示されません。  

---

![テーブルの管理のビュータブ。作成済みのビューが一覧表示される](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/aeb9b855a16f490d9edc43ea0c64ba2e.png)

[ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)の保存種別を設定できます。  
![ビューの「保存種別」を設定する欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/d66e6abac031453b992f486a80daf09f.png)

保存種別 | 説明
--- | --- 
セッション | 次の条件で保持されます。(1)プリザンターからログアウトするまで (2)Session.jsonのRetentionPeriodの値の期限内 (3)全てのブラウザを閉じるまで
ユーザ | データベースに保存し、次回も適用されます
保存しない | 常に初期状態で表示します

### ビューの新規作成/詳細設定

ビューを新規に作成するには[新規作成](table-management-create-view.md)ボタンをクリックします。既存のビューの設定変更をする場合は[詳細設定](table-management-view-list.md)ボタンをクリックします。  
新規作成および詳細設定画面では下表のタブが表示されます。

|タブ名|説明|
|:---|:---|
|一覧|表示項目の選択、[フィルタと集計の設定](table-management-view-filter-totaling.md)、[コマンドボタンの設定](table-management-view-command-button.md)。|
|フィルタ|ビューに表示されるレコードの検索（フィルタ）の設定|
|ソータ|ビューに表示されるレコードの並び替え（ソート）の設定。|
|エディタ|レコードのエディタ画面に表示されるボタンの設定。|
|カレンダー|ビューをカレンダー表示した場合の設定。|
|クロス集計|ビューをクロス集計表示した場合の設定。|
|ガントチャート|ビューをガントチャート表示した場合の設定。|
|時系列チャート|ビューを時系列チャート表示した場合の設定。|
|カンバン|ビューをカンバン表示した場合の設定。|
|アクセス制御|ビューに対する[アクセス制御の設定](table-management-view-permissions.md)|

---

## ビューの設定例

1. 一覧の設定項目を多くした場合、行ごとの情報量は多い分1画面で表示できる行数は少なくなります。 
![一覧の設定項目を多くしたビューの設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/0104abba75cc470eb3e24a47f58bc374.png)
一覧画面表示例
![設定項目を多くしたビューの一覧画面の表示例。1画面に表示できる行数が少ない](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/1d955a618f9f4205a18c6a0e338aa028.png)

1. 一覧の設定項目を必要な情報のみに絞った場合、1画面に表示できる行数を多くすることができます。  
![一覧の設定項目を必要な情報のみに絞ったビューの設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/5929f18024af4f2b89e177112ca7009d.png)
一覧画面表示例
![設定項目を絞ったビューの一覧画面の表示例。1画面に表示できる行数が多い](https://pleasanter.org/files/images/ja/managers-guide/manage-table/view/assets/457e7ebeeeed408aa60b55b1b1e3031a.png)

## 関連情報

-   [テーブルの管理](../index.md)
-   [応用編：ビュー](../../../users-guide/hands-on/advanced/advanced-operations-view.md)
-   [テーブルの管理：ビュー：新規作成](table-management-create-view.md)
-   [テーブルの管理：ビュー：詳細設定：一覧タブ：一覧の設定](table-management-view-list.md)
-   [テーブルの管理：ビュー：詳細設定：一覧タブ：コマンドボタンの設定](table-management-view-command-button.md)
-   [テーブルの管理：ビュー：詳細設定：アクセス制御タブ](table-management-view-permissions.md)