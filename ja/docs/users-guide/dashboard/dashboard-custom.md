---
title: カスタム
category: ダッシュボード機能
order: '40'
status: ''
parts: ''
urlstring: dashboard-custom
translationKey: dashboard-custom
shortname: ダッシュボード,パーツ,カスタム
created: 2023-07-11
updated: 2024-06-21
---

## 概要

[ダッシュボード](dashboard-add-parts.md)にカスタムを追加します。使い方ガイドのような定型文などの表示に利用できます。

## 設定手順

### 全般タブ

![カスタムの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/97669fa3eba6494aa827549779db83b4.png)

| 項目名               | 説明                                                                                                                                                                                        |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| タイトル             | パーツの名称です。                                                                                                                                                                          |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                  |
| 内容                 | 表示したい内容を入力します。[マークダウン](../common/markdown.md)を使用した入力や[画像](../table/record-authoring/edit-records/table-record-upload-picture.md)の登録が可能です。            |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については「[ダッシュボード機能：パーツの追加](dashboard-add-parts.md)」を参照ください。    |
| CSS                  | タイムラインの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。 |

### アクセス制御タブ

![カスタムの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/61cfd55ee4da4d5a950d1830ac2a57a3.png)

タイムラインに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

## 表示内容

カスタムで入力した内容を表示します。

![カスタムに入力した内容がダッシュボードに表示された例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/af14eaef5d154187b845cdcc656edd54.png)

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [共通機能：マークダウン](../common/markdown.md)
-   [テーブル機能：レコードに画像を登録](../table/record-authoring/edit-records/table-record-upload-picture.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
