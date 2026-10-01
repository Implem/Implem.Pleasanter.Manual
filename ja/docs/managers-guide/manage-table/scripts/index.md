---
title: スクリプト
category: 開発者ガイド
order: '2'
status: ''
parts: ''
urlstring: table-management-script
translationKey: table-management-script
shortname: スクリプト
created: 2019-12-05
updated: 2026-08-12
---

## 概要

「[テーブルの管理](../index.md)」画面の「スクリプト」タブでは、テーブルに対して[スクリプト](../../../developers-guide/script/index.md)を追加できます。

### 「スクリプト」タブでできること

-   コードエディタで[スクリプト](../../../developers-guide/script/index.md)を作成・編集・登録できる
-   [スクリプト](../../../developers-guide/script/index.md)の出力先を設定できる
-   [スクリプト](../../../developers-guide/script/index.md)の有効化・無効化を切り替えられる
-   ユーザのスクリプト編集を支援する「コードエディタ」を利用できる（第2世代[ユーザインターフェースのテーマ](../../user-administration/user-management-theme.md)を利用している場合）
-   ドラフト機能で[スクリプト](../../../developers-guide/script/index.md)の動作をテストできる

!!! note "Pleasanter Code Assist"

    [Pleasanter Code Assist](../../../products-info/pleasanter-extensions/pleasanter-code-assist/index.md)を導入すると、Visual Studio Codeの高度な編集機能を用いてスクリプトを作成、編集、追加できます。

## 前提条件

1.  設定を行うには「サイトの管理」権限が必要です。

## 操作手順

### 「スクリプト」タブの表示

1.  ナビゲーションメニューの「管理」をクリックしてください。
1.  「[テーブルの管理](../index.md)」をクリックしてください。
1.  「スクリプト」タブをクリックしてください。

### スクリプト一覧

「[テーブルの管理](../index.md)」画面の「スクリプト」タブには、スクリプト一覧が表示されます。

![テーブルの管理の「スクリプト」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/scripts/assets/8d26f3999432414980fbb585448a9bf7.png)

一覧の左端に表示されたチェックボックスでスクリプトを選択することで、以下の操作を行えます。

|                No                 | ボタン名 | 機能                                                                                                                                                           |
| :-------------------------------: | :------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span class="pl-callout">1</span> |    上    | 選択したスクリプトを1つ上に移動します。                                                                                                                        |
| <span class="pl-callout">2</span> |    下    | 選択したスクリプトを1つ下に移動します。                                                                                                                        |
| <span class="pl-callout">3</span> |  コピー  | 選択したスクリプトを複製します。<br>複製されたスクリプトはスクリプト一覧の一番下へ追加されます。                                                               |
| <span class="pl-callout">4</span> |   削除   | 選択したスクリプトを一覧から削除します。<br>「削除」ボタンをクリックすると、ダイアログが表示されます。<br>「OK」ボタンをクリックすると、一覧から削除されます。 |

### スクリプトの新規作成・編集・追加

<div class="steps" markdown>

1.  「新規作成」ボタンまたはスクリプト一覧に追加済みのスクリプトをクリックしてください。
1.  スクリプトの編集画面が表示されます。
1.  以下の各項目を設定してください。

    | 項目名       | 説明                                                                   | 設定方法                                                               |
    | :----------- | :--------------------------------------------------------------------- | :--------------------------------------------------------------------- |
    | タイトル     | スクリプトのタイトルを入力します。                                     | 任意のタイトルを入力してください。                                     |
    | スクリプト   | スクリプトを入力します。                                               | 任意のスクリプトを入力してください。                                   |
    | 無効         | スクリプトの有効化・無効化を切り替えます。                             | 無効化するときオンに、有効化するときオフに設定してください。           |
    | ドラフト出力 | [ドラフト機能](../common/draft.md)を参照してください。 | [ドラフト機能](../common/draft.md)を参照してください。 |
    | ドラフトキー | [ドラフト機能](../common/draft.md)を参照してください。 | [ドラフト機能](../common/draft.md)を参照してください。 |
    | 出力先       | 出力先の画面を選択します。                                             | 以下の「出力先の設定方法」を参照してください。                         |

    !!! tip "コードエディタとは"

        第2世代[ユーザインターフェースのテーマ](../../user-administration/user-management-theme.md)を利用している場合、ユーザのスクリプト編集を支援する「コードエディタ」を利用できます。

        ![コードエディタでスクリプトを編集している画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/scripts/assets/fc3189b1be52490287e3ccf497385ec0.png)

        コードエディタが提供する主な編集支援機能は、以下の通りです。

        -   シンタックスハイライト
        -   コードヒントの表示
        -   タブキーでのインデント入力　など

        コードエディタを利用するには、[`General.json`](../../../setup/parameters/general.json.md)のパラメータ`EnableCodeEditor`を`true`に設定してください。

    !!! note "出力先の設定方法"

        「出力先」は、既定で「全て」のチェックがオンになっています。

        ![出力先は既定で「全て」がオンになっている](https://pleasanter.org/files/images/ja/managers-guide/manage-table/scripts/assets/0bd9e0882b7948348b74fd635dae79fb.png)

        「全て」のチェックをオフにすると、他の出力先が表示されます。任意の出力先を選択してください。

        ![「全て」のチェックをオフにすると他の出力先が表示される](https://pleasanter.org/files/images/ja/managers-guide/manage-table/scripts/assets/a220cf7f4dbd438a8deab70dea2a1d32.png)

1.  新規にスクリプトを作成した場合は「追加」ボタンを、既存のスクリプトを編集した場合は「更新」ボタンをクリックしてください。

1.  コマンドボタンエリアの「更新」ボタンをクリックしてください。

</div>

### 全て無効化

スクリプト一覧の上部にある「全て無効化」をオンにすると、既存のスクリプトを全て無効化できます。

![スクリプト一覧の上部にある「全て無効化」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/scripts/assets/35198b1124b84cef8e83af1700fcc7a3.png)

!!! warning

    「全て無効化」をオンにしても、個々のスクリプトの「無効」チェックボックスの状態は変わりません。

## 対応バージョン

| 対応バージョン | 内容                       |
| :------------- | :------------------------- |
| 1.4.14.0 以降  | 「全て無効化」機能を追加   |
| 1.5.7.0 以降   | 「ドラフト出力」機能を追加 |

## 関連情報

-   [テーブルの管理](../index.md)
-   [ユーザインターフェースのテーマをカスタマイズ](../../user-administration/user-management-theme.md)
-   [スクリプト](../../../developers-guide/script/index.md)
