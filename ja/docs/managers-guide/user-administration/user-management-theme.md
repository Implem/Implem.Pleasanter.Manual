---
title: ユーザインターフェースのテーマをカスタマイズ
category: ユーザ管理機能
order: '70'
status: ''
parts: ''
urlstring: user-management-theme
translationKey: user-management-theme
shortname: ユーザインターフェースのテーマをカスタマイズ,ユーザインターフェースのテーマ
created: 2021-05-30
updated: 2025-07-08
---

## 概要

画面のカラーバリエーションを変更できます。全体で共通のテーマを設定でき、更にユーザは自分自身の画面に適用されるテーマを変更できます。

第2世代のテーマでは、カラーバリエーションが追加すると共に、ナビゲーションメニューをはじめ、第1世代と比較して全体的に使いやすさが向上しました。

## レイアウトの種類

ナビゲーションメニューの位置によって、2種類のレイアウトがあります。

### 第2世代ユーザインターフェースのレイアウト

ナビゲーションメニューが画面左側に表示されるレイアウトです。

![第2世代ユーザインターフェースの画面。ナビゲーションメニューが左側にある](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/42c03ecdd3c5429dae9d6c2698b5ec9d.png)

=== "cerulean"

    ![第2世代のテーマ「cerulean」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/26cerulean.png)

=== "green-tea"

    ![第2世代のテーマ「green-tea」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/27green-tea.png)

=== "mandarin"

    ![第2世代のテーマ「mandarin」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/28mandarin.png)

=== "midnight"

    ![第2世代のテーマ「midnight」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/29midnight.png)

### カスタムナビゲーションメニューによる追加メニュー

2世代ユーザインターフェースは、「NavigationMenu.json」により子メニューを最大3階層まで追加設定できます。

![NavigationMenu.jsonで子メニューを追加した第2世代のナビゲーションメニュー](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/8a6b35d4826643ca91ccbb10fcf39740.png)

### 第1世代ユーザインターフェースのレイアウト

ナビゲーションメニューが画面右上に表示されるレイアウトです。

![第1世代ユーザインターフェースの画面。ナビゲーションメニューが右上にある](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/ca68a5813fc347cdafbd77d48c2866b3.png)

選択可能な値は[jQuery UI](https://jqueryui.com/)のテーマ名です。

#### ライトテーマ

=== "base"

    ![第1世代のライトテーマ「base」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/01base.png)

=== "black"

    ![第1世代のライトテーマ「black」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/02black-tie.png)

=== "blitzer"

    ![第1世代のライトテーマ「blitzer」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/03blitzer.png)

=== "cupertino"

    ![第1世代のライトテーマ「cupertino」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/04cupertino.png)

=== "excite-bike"

    ![第1世代のライトテーマ「excite-bike」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/08excite-bike.png)

=== "flick"

    ![第1世代のライトテーマ「flick」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/09flick.png)

=== "hot-sneaks"

    ![第1世代のライトテーマ「hot-sneaks」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/10hot-sneaks.png)

=== "humanity"

    ![第1世代のライトテーマ「humanity」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/11humanity.png)

=== "overcast"

    ![第1世代のライトテーマ「overcast」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/14overcast.png)

=== "pepper-grinder"

    ![第1世代のライトテーマ「pepper-grinder」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/15pepper-grinder.png)

=== "redmond"

    ![第1世代のライトテーマ「redmond」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/16redmond.png)

=== "smoothness"

    ![第1世代のライトテーマ「smoothness」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/17smoothness.png)

=== "south-street"

    ![第1世代のライトテーマ「south-street」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/18south-street.png)

=== "start"

    ![第1世代のライトテーマ「start」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/19start.png)

=== "sunny"

    ![第1世代のライトテーマ「sunny」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/20sunny.png)

=== "ui-lightness"

    ![第1世代のライトテーマ「ui-lightness」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/24ui-lightness.png)

#### ダークテーマ

=== "dark-hive"

    ![第1世代のダークテーマ「dark-hive」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/05dark-hive.png)

=== "dot-luv"

    ![第1世代のダークテーマ「dot-luv」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/06dot-luv.png)

=== "eggplant"

    ![第1世代のダークテーマ「eggplant」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/07eggplant.png)

=== "le-frog"

    ![第1世代のダークテーマ「le-frog」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/12le-frog.png)

=== "mint-choc"

    ![第1世代のダークテーマ「mint-choc」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/13mint-choc.png)

=== "swanky-purse"

    ![第1世代のダークテーマ「swanky-purse」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/21swanky-purse.png)

=== "trontastic"

    ![第1世代のダークテーマ「trontastic」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/22trontastic.png)

=== "ui-darkness"

    ![第1世代のダークテーマ「ui-darkness」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/23ui-darkness.png)

=== "vander"

    ![第1世代のダークテーマ「vander」を適用した画面](https://pleasanter.org/files/images/ja/managers-guide/user-administration/assets/25vander.png)

## 操作手順

### ユーザが自分自身の画面のテーマを変更する

1.  「ナビゲーションメニュー」の「[ユーザ](index.md)」－「[プロファイル編集](../../users-guide/common/profile.md)」をクリックします。
1.  「テーマ」を選択します。
1.  画面下部の「更新」ボタンをクリックします。

## その他のテーマ設定項目

プロファイル編集以外に、次の項目でテーマを設定できます。

| 優先順位 | 設定場所                                                    | 規定値   |
| -------- | ----------------------------------------------------------- | -------- |
| 1        | 「ユーザ管理機能」の「テーマ」                              | 指定なし |
| 2        | 「テナント管理機能」の「テーマ」                            | 指定なし |
| 3        | [User.json](../../setup/parameters/user-json.md)の「Theme」 | cerulean |

-   [User.json](../../setup/parameters/user-json.md)の「Theme」の既定値である「cerulean」は、第2世代ユーザインターフェースに所属するテーマです。

### 子メニューの追加

-   第2世代ユーザインターフェースのテーマは、[NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)または[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)により、子メニューを最大3階層まで追加できます。

### 旧世代テーマの適用

既定以外の旧世代ユーザインターフェースのテーマを適用できます。前述のその他のテーマ設定項目を参考に「ユーザ管理機能」、「テナント管理機能」または[User.json](../../setup/parameters/user-json.md)の設定を修正し、旧世代のテーマが適用されるように項目値を選択してください。

## 制限事項

1.  最新のOSおよびブラウザのご利用を推奨します。一部の古いOSおよびブラウザでは、正常に動作しない場合があります。
1.  第2世代ユーザインターフェースのテーマは、「NavigationMenu.json」または[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)によるIconの指定には対応していません。

## 対応バージョン

| 対応バージョン | 内容                               |
| :------------- | :--------------------------------- |
| 1.1.27.0以降   | ユーザ単位のテーマ選択機能を追加   |
| 1.4.3.0以降    | テーマの既定値を「cerulean」に変更 |

## 関連情報

-   [jQuery UI](https://jqueryui.com/)
-   [User.json](../../setup/parameters/user-json.md)
-   [NavigationMenus.json](../../setup/parameters/navigation-menus-json.md)
-   [拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)
