---
title: ロゴ、タイトル、ロゴ画像
category: テナント管理機能
order: '100'
status: ''
parts: ''
urlstring: tenant-logo
translationKey: tenant-logo
shortname: ロゴ、タイトル、ロゴ画像,ロゴ,タイトル,ロゴ画像,テナント名
created: 2024-04-04
updated: 2024-04-11
---

## 概要

画面左上の「テナント名」の表示内容を変更する機能です。

## 制限事項

1.  本機能ではログイン画面の表示内容は変更できません。ログイン画面の表示内容を変更したい場合は以下FAQを参照ください。  
    [FAQ：ロゴ画像やタイトルを変更したい \| Pleasanter](../../FAQ/others/faq-change-logo-and-title.md)

## 前提条件

1.  設定を行うには[テナント管理者](../user-administration/user-management-tenant-manager.md)権限が必要です。

## ロゴタイプ

ロゴタイプの設定で「画像のみ」か「画像とテキスト」の表示を切り替えます。

### 設定種別

| 設定           | 説明                                                                                                     |
| :------------- | :------------------------------------------------------------------------------------------------------- |
| 画像のみ       | 画像のみを表示します。デフォルト設定ではHAYATOアイコンと「Pleasanter」のロゴ画像です。                   |
| 画像とテキスト | 画像に加えて「タイトル」に入力した文字列を表示します。デフォルト設定で表示する画像はHAYATOアイコンです。 |

### 設定イメージ

=== "画像のみ"

    ![ロゴタイプ「画像のみ」を設定したときのロゴの表示](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/d305c44f243e47f78765b88ff43c4fbe.png)

=== "画像とテキスト（テキストには「プリザンター」と入力）"

    ![ロゴタイプ「画像とテキスト」でテキストに「プリザンター」を設定したときのロゴの表示](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/76f497951c7c44fcb200d5b7de760027.png)

## タイトル

ロゴタイプで「画像とテキスト」を選択した場合に画像とともに表示するテキストを入力します。なおロゴタイプで「画像のみ」を選択した場合はタイトルに文字列が入力してあっても表示しません。

![テナントの管理画面の「タイトル」欄](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/ba3d532b0748441c9dddc35318a88c07.png)

## ロゴ画像

デフォルトの画像をアップロードした画像に変更します。画像をアップロードした場合、ロゴタイプの設定にかかわらずアップロードした画像が表示されます。

### アップロードする画像

![ロゴ画像としてアップロードする画像の例](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/0f2ba633602c401e94cc056686fdf513.png)

### 設定イメージ

=== "画像のみ"

    ![アップロードした画像を「画像のみ」で表示したロゴ](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/f18c3b1927514b67b49db340302b95c2.png)

=== "画像とテキスト（テキストには「プリザンター」と入力）"

    ![アップロードした画像とテキスト「プリザンター」を表示したロゴ](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/226513e08c8a4b2582a855d867edf9e3.png)

画像をアップロードすると、アップロードボタンの右隣に削除ボタンが表示します。アップロードした画像を取り消したい場合は削除ボタンをクリックしてください。

![アップロードボタンの右隣に削除ボタンが表示された状態](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/ddba7354a91b4120a4e4529d55a98bdd.png)

## 関連情報

-   [FAQ：ロゴ画像やタイトルを変更したい \| Pleasanter](../../FAQ/others/faq-change-logo-and-title.md)
-   [ユーザ管理機能：テナント管理者の設定](../user-administration/user-management-tenant-manager.md)
