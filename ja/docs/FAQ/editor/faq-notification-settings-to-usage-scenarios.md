---
title: 利用シーンにあわせた通知設定をしたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-notification-settings-to-usage-scenarios
translationKey: faq-notification-settings-to-usage-scenarios
shortname: ''
created: 2024-02-29
updated: 2025-01-30
---

## 回答

目的の要件に応じて[通知](../../users-guide/hands-on/advanced/advanced-operations-notification.md)や[プロセス](../../users-guide/hands-on/advanced/advanced-operations-process.md)の通知機能を利用します。

---

## 概要

日々の業務の中で想定される利用シーンでの通知設定例を説明します。

## 目次

1. [レコード更新の都度、任意の担当者に通知したい](#case01)
2. [承認ワークフローで、申請時に承認担当者グループのメンバー宛に通知したい](#case02)

<a id="case01"></a>
<br/>

## 1. レコード更新の都度、任意の担当者に通知したい

### 想定の利用要件

1. レコード更新の都度、通知する
1. 通知先はレコードごとに違う
1. 通知先の担当者はレコードに設定する

### 画面イメージ

![通知対象者を選択する項目を配置した編集画面のイメージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/e823fbb556494df9a42250bcf4fd3555.png)
通知対象者を選択する項目を設定します。

### テーブル設定

#### 1. [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)の設定

##### 任意の項目を有効化し、以下の設定を行います。

  1. 表示名を任意で設定
  1. 選択肢に「Users」を設定
  1. 複数選択にチェック（※）

※通知対象者が複数であることを想定

#### 2. [通知](../../users-guide/hands-on/advanced/advanced-operations-notification.md)の設定

![通知の設定画面。アドレス欄に通知先の項目名を指定する](https://pleasanter.org/files/images/ja/FAQ/editor/assets/21d9757f6aa14ce89128f590a654da9b.png)

##### 以下のように通知設定を行います。

   1. アドレス欄に、エディタで設定した通知先の項目名を設定
   1. その他の通知要件は任意で設定

### 利用イメージ

![通知対象者を選んでレコードを作成・更新したときの利用イメージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/3698939e42e94668939ef41873ebf2b9.png)

通知対象者を選択し、レコードを作成・更新すると、選択したユーザ宛に通知されます。

<a id="case02"></a>
<br/>

## 2. 承認ワークフローで、申請時に承認担当者グループのメンバー宛に通知したい

### 想定の利用要件

1. 起票→申請→承認のような単純なワークフローを設定
1. 起票者が申請した際に、承認権限のあるメンバー（＝承認担当者グループ）宛に通知する

ワークフローイメージ
![起票から申請、承認へと進むワークフローのイメージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/56ab013de93e498381fb9aed39e363fc.png)

### グループ設定

1. 承認担当者グループを用意します。
![承認担当者グループの設定画面。グループIDが確認できる](https://pleasanter.org/files/images/ja/FAQ/editor/assets/77ccf424a8024a2cbf1c268913a90bd3.png)
※グループIDが後で必要になるので、メモしておきます。

### テーブル設定

#### [プロセス](../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定

1. 申請と承認のプロセスを作成します。
![申請と承認の2つのプロセスを登録した状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/6f4fbdbc21594f219f072d73922ea86b.png)

2. 申請のプロセスに通知を設定します。
![申請のプロセスに通知を設定する画面](https://pleasanter.org/files/images/ja/FAQ/editor/assets/ec5cf1f12f3c46e19149b6ec375e2974.png)
![通知の詳細設定。承認担当者グループのグループIDを指定する](https://pleasanter.org/files/images/ja/FAQ/editor/assets/d1a46525feb34fe7be842e198b30e297.png)
通知の詳細設定に、事前に用意した承認担当者のグループIDを指定します。

### 利用イメージ

![申請時に承認担当者グループのメンバー宛へ通知が届く利用イメージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/65358a56410646db91b873d59c8a743a.png)
設定後、申請を実施するタイミングで、承認担当者グループに所属するメンバー宛に通知されます。

## 関連情報

-   [応用編：通知、リマインダー](../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [応用編：プロセスと状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)