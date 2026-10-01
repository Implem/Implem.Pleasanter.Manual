---
title: 情報公開機能
category: 公開
order: '0'
status: ''
parts: ''
urlstring: table-management-publish
translationKey: table-management-publish
shortname: 情報公開機能
created: 2019-12-17
updated: 2026-06-30
---

## 概要

ログインしていないユーザでも、プリザンターのテーブルを閲覧できるようにする機能です。公開時は以下の制約が付加されます。
   1. ナビゲーションメニュー使用不可
   1. 横断検索使用不可
   1. パンくずリスト非表示
   1. レコードの操作不可（新規登録、更新、削除、インポート、エクスポート）
   1. 変更履歴閲覧不可

## 制限事項

1. 公開時「[項目連携](../editor/relating-column-settings/index.md)」機能は使用できませんので、設定を解除してください。項目連携機能を設定したままで公開すると、以下のようなエラーメッセージが表示されます。
![項目連携を設定したまま公開したときに表示されるエラーメッセージ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/d787c6d13c8d45d09d8064f91edb21a4.png)
2. 公開テーブルにリンクしているテーブルの情報は表示できません。

## 前提条件

1. Pleasanter.netをご利用の方は、スタンダードプランのご契約と合わせてオプション機能である「情報公開機能」を契約してください。

## 情報公開機能の設定方法

以下の手順でプリザンターの情報公開機能を設定します。  
1. 対象テナントの情報公開機能を有効化する  
1. 対象サイトの情報公開機能を有効化する      

### 1. 対象テナントの情報公開機能を有効化する  

SQL Server Management StudioやAzure Data Studioを開いて(※1)  
「データベース」→ 「Implem.Pleasanter」→ 「テーブル」→「dbo.Tenants」を選択し上位200行の編集」をクリック。該当のサイトの行を選択し「ContractSettings」カラムに以下内容を入力します。  

##### json

```
{"Extensions":{"Publish":true}}
```

(※1)PostgreSQLの場合はPgAdmin等を使用してください。

![dbo.TenantsのContractSettingsカラムを編集しているデータベースの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/66331de0cb084161a8febdf0c4e94d74.png)  

#### 対象レコードが存在しない場合

dbo.Tenantsにレコードが存在しない場合、ナビゲーションメニューの「管理」→「[テナントの管理](../../tenant-administration/index.md)」で更新ボタンをクリックしてください。
![テナントの管理画面。更新ボタンがある](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/6007d5978fb240c39651c9f409b4e8a2.png)

### 2. 対象サイトの情報公開機能を有効化する  

公開したいテーブルを開き、テーブルの管理画面を開きます。下記の赤枠部分の「公開」タブをクリックし、「匿名ユーザに公開する」チェックをオンにします。
![テーブルの管理の「公開」タブ。「匿名ユーザに公開する」チェックがある](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/8d3995d3acc443dfbcf14f552c561958.png)

## 公開したテーブルの表示

以下のURLで公開テーブルにアクセスします。  
https://サーバ名/publishes/xxx/index   
※xxx は公開テーブルのサイトIDです。  

![公開URLでアクセスした公開テーブルの画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/9711d479ec824bc3b42125c2f9b64cab.png)

画面の赤帯をクリックするたびに公開/非公開が切り替わると共に、URLも下記の例の様にアドレスの一部が切り替わります。

例) 公開：https://サーバ名/publishes/xxx/index  
例) 非公開：https://サーバ名/items/xxx/index

公開時
![公開時の画面。URLがpublishesを含む](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/71308698845d4c43a64fedfc31a808b9.png)
非公開時
![非公開時の画面。URLがitemsを含む](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/3eb95e28cfbb4929a4d1d2fca611a584.png)

### サイトIDの調べ方

公開対象のテーブルを開き、ナビゲーションメニューの「管理」→「[テーブルの管理](../index.md)」を開き、「全般」タブの「サイトID」を確認してください。
![テーブルの管理の「全般」タブ。「サイトID」が表示されている](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/5a8e153789ce436bbdbafa4b22cd86e1.png)

公開対象のテーブルを開いた状態でブラウザのアドレスバーでも確認できます。
![ブラウザのアドレスバーでサイトIDを確認する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/publish/assets/ecdf14da6b6e4237aca8efa1af43a539.png)
