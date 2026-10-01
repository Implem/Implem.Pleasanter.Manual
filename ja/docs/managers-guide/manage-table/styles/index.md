---
title: スタイル
category: 開発者ガイド
order: '1'
status: ''
parts: ''
urlstring: table-management-style
translationKey: table-management-style
shortname: スタイル
created: 2019-12-05
updated: 2026-08-12
---

## 概要

「[テーブルの管理](../index.md)」画面の「スタイル」タブでは、テーブルに対してスタイル（CSS）を追加できます。

### 「スタイル」タブでできること

-   コードエディタでCSSを作成・編集・登録できる
-   CSSの出力先を設定できる
-   CSSの有効化・無効化を切り替えられる
-   ユーザのCSS編集を支援する「コードエディタ」を利用できる（第2世代[ユーザインターフェースのテーマ](../../user-administration/user-management-theme.md)を利用している場合）
-   ドラフト機能でCSSの動作をテストできる

!!! note "Pleasanter Code Assist"

    [Pleasanter Code Assist](../../../products-info/pleasanter-extensions/pleasanter-code-assist/index.md)を導入すると、Visual Studio Codeの高度な編集機能を用いてCSSを作成、編集、追加できます。

## 前提条件

1.  設定を行うには「サイトの管理」権限が必要です。

## 操作手順

### 「スタイル」タブの表示

1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  「[テーブルの管理](../index.md)」をクリックしてください。
1.  「スタイル」タブをクリックしてください。

### スタイル一覧

「[テーブルの管理](../index.md)」画面の「スタイル」タブには、スタイル一覧が表示されます。

![テーブルの管理の「スタイル」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/75195ac0da5c4f44812450df2e05c0f1.png)

一覧の左端に表示されたチェックボックスでスタイルを選択することで、以下の操作を行えます。

|                No                 | ボタン名 | 機能                                                                                                                                                         |
| :-------------------------------: | :------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span class="pl-callout">1</span> |    上    | 選択したスタイルを1つ上に移動します。                                                                                                                        |
| <span class="pl-callout">2</span> |    下    | 選択したスタイルを1つ下に移動します。                                                                                                                        |
| <span class="pl-callout">3</span> |  コピー  | 選択したスタイルを複製します。<br>複製されたスタイルはスタイル一覧の一番下へ追加されます。                                                                   |
| <span class="pl-callout">4</span> |   削除   | 選択したスタイルを一覧から削除します。<br>「削除」ボタンをクリックすると、ダイアログが表示されます。<br>「OK」ボタンをクリックすると、一覧から削除されます。 |

### スタイルの新規作成・編集・追加

<div class="steps" markdown>

1.  「新規作成」ボタンまたはスタイル一覧に追加済みのスタイルをクリックしてください。
1.  スタイルの編集画面が表示されます。
1.  以下の各項目を設定してください。

    | 項目名       | 説明                                                   | 設定方法                                                     |
    | :----------- | :----------------------------------------------------- | :----------------------------------------------------------- |
    | タイトル     | スタイルのタイトルを入力します。                       | 任意のタイトルを入力してください。                           |
    | スタイル     | スタイルを入力します。                                 | 任意のCSSを入力してください。                                |
    | 無効         | スタイルの有効化・無効化を切り替えます。               | 無効化するときオンに、有効化するときオフに設定してください。 |
    | ドラフト出力 | [ドラフト機能](../common/draft.md)を参照してください。 | [ドラフト機能](../common/draft.md)を参照してください。       |
    | ドラフトキー | [ドラフト機能](../common/draft.md)を参照してください。 | [ドラフト機能](../common/draft.md)を参照してください。       |
    | 出力先       | 出力先の画面を選択します。                             | 以下の「出力先の設定方法」を参照してください。               |

    !!! tip "コードエディタとは"

        第2世代[ユーザインターフェースのテーマ](../../user-administration/user-management-theme.md)を利用している場合、ユーザのCSS編集を支援する「コードエディタ」を利用できます。

        ![コードエディタでCSSを編集している画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/17db6e67d6d645bba8ed096baca569b9.png)

        コードエディタが提供する主な編集支援機能は、以下の通りです。

        -   シンタックスハイライト
        -   コードヒントの表示
        -   タブキーでのインデント入力　など

        コードエディタを利用するには、[`General.json`](../../../setup/parameters/general.json.md)のパラメータ`EnableCodeEditor`を`true`に設定してください。

    !!! note "出力先の設定方法"

        「出力先」は、既定で「全て」のチェックがオンになっています。

        ![出力先は既定で「全て」がオンになっている](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/423f78e8e7154a4889edeb4fea7f5e84.png)

        「全て」のチェックをオフにすると、他の出力先が表示されます。任意の出力先を選択してください。

        ![「全て」のチェックをオフにすると他の出力先が表示される](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/796274a797724b4d93b6b4368f08bd21.png)

1.  新規にスタイルを作成した場合は「追加」ボタンを、既存のスタイルを編集した場合は「更新」ボタンをクリックしてください。

1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

</div>

### 全て無効化

スタイル一覧の上部にある「全て無効化」をオンにすると、既存のスタイルを全て無効化できます。

![スタイル一覧の上部にある「全て無効化」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/c53f95e425bf48de8dede409bbb19543.png)

!!! warning

    「全て無効化」をオンにしても、個々のスタイルの「無効」チェックボックスの状態は変わりません。

### レスポンシブ

「レスポンシブ」チェックボックスをオンにしている場合、モバイルデバイス向けにレスポンシブデザインのスタイルシートを出力します。

![スタイル一覧の下部にある「レスポンシブ」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/f1c7a545e0cb4f20a260fbd0594e2bcd.png)

|トップページ|一覧表示画面|編集画面|
|:-:|:-:|:-:|
|![トップページをモバイルで表示したところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/cbe5edc2f7ac42109efa1849750da878.png)|![一覧画面をモバイルで表示したところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/3f93bcffe92a4a3fb16a6d54085dbdff.png)|![編集画面をモバイルで表示したところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/styles/assets/a2fa380067b74d25be44e71d423235d1.png)|

## 対応バージョン

| 対応バージョン | 内容                       |
| :------------- | :------------------------- |
| 1.4.14.0 以降  | 「全て無効化」機能を追加   |
| 1.5.7.0 以降   | 「ドラフト出力」機能を追加 |

## 関連情報

-   [テーブルの管理](../index.md)
-   [ユーザインターフェースのテーマをカスタマイズ](../../user-administration/user-management-theme.md)
-   [スタイル](../../../developers-guide/style/index.md)
