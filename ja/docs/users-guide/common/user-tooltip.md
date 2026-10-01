---
title: ユーザ、組織選択時のツールチップ表示
category: 共通機能
order: '0'
status: ''
parts: ''
urlstring: user-tooltip
translationKey: user-tooltip
shortname: ツールチップ
created: 2022-04-08
updated: 2024-07-01
---

## 概要

「[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)」および「[グループメンバー追加](../hands-on/basics/basic-operations-group-member.md)」の設定で、「ユーザ」、「組織」の選択肢にマウスカーソルを合わせると表示されるツールチップについて説明します。

## ユーザのツールチップ

「[ユーザ](../../managers-guide/user-administration/index.md)」に設定した内容が下記フォーマットでツールチップに表示されます。
ログインID、メールアドレスのどちらが表示されるかは[User.json](../../setup/parameters/user-json.md)の"SelectorToolTip"の設定に従います。

`{ログインID または メールアドレス} {ユーザコード} {説明}`

## 組織のツールチップ

「[組織](../../managers-guide/department-administration/index.md)」に設定した内容が下記フォーマットでツールチップに表示されます。

`{組織コード} {説明}`

## 例：グループメンバー追加画面

下記ユーザのツールチップを表示

|項目名|値|
|:--|:--|
|ログインID|y-satou|
|ユーザコード|A002|
|説明|経理部|

![グループメンバー追加画面で、ユーザの選択肢に表示されたツールチップ](https://pleasanter.org/files/images/ja/users-guide/common/assets/067bba3417024293bac9ba15903c72c9.png)

## 例：「サイトのアクセス制御」の「組織」のツールチップ

下記組織のツールチップを表示

|項目名|値|
|:--|:--|
|組織コード|Imp001|
|説明|中野事業所|

![グループメンバー追加画面で、組織の選択肢に表示されたツールチップ](https://pleasanter.org/files/images/ja/users-guide/common/assets/8b09083e724a4f53ae4ab4c880173814.png)
