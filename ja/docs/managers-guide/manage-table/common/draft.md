---
title: ドラフト機能
category: 共通機能
order: '0'
status: ''
parts: ''
urlstring: draft
translationKey: draft
shortname: ドラフト機能
created: 2026-07-29
updated: 2026-08-12
---

## 概要

スタイル・スクリプト・HTMLの各設定に対して、ドラフト表示時にのみ出力する、またはドラフト表示時のみ出力しない、といった出力の切り替えを行うことができる機能です。本番公開中の画面には反映させずに動作確認を行いたい場合などに利用します。ドラフト表示は、事前にドラフトキーを設定し、表示確認を行う際にURLの末尾にドラフトキーを追加することで確認を行います。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。
1.  本機能はスタイル・スクリプト・HTMLのそれぞれに個別に設定します。

## 操作手順

### 設定方法

<div class="steps" markdown>

1.  テーブルの管理でスタイル・スクリプト・HTMLタブのいずれかを選択します。
    このマニュアルではHTMLの設定を例に挙げ、設定方法を説明します。

    ![テーブルの管理のHTMLタブ](https://pleasanter.org/files/images/ja/developers-guide/assets/c8100adc7239424893030dbb292c8d7a.png)

1.  新規作成またはHTMLの一覧から登録済みの項目をクリックすると、編集ダイアログが表示されます。「ドラフト出力」「ドラフトキー」の項目を使用します。

    ![HTMLの編集ダイアログ。「ドラフト出力」と「ドラフトキー」の項目がある](https://pleasanter.org/files/images/ja/developers-guide/assets/7e33e594e2a747848d7a69da2795202e.png)

1.  HTMLを記述後、「ドラフト出力」で出力タイミングを選択します。設定可能な内容は以下の通りです。

    | 選択肢                 | 説明                                                                                                 |
    | :--------------------- | :--------------------------------------------------------------------------------------------------- |
    | 通常出力（常に）       | ドラフト表示かどうかに関わらず、常に出力します。（既定値）                                           |
    | ドラフト時のみ出力     | ドラフト表示時（URLに`?Draft=`パラメータが付与され、値がドラフトキーと一致する場合）のみ出力します。 |
    | ドラフト時は出力しない | ドラフト表示時は出力せず、それ以外の場合（通常表示時）に出力します。                                 |

    ここでは、ドラフト表示の動作を確認するために、「ドラフト時のみ出力」を選択してください。

1.  「ドラフトキー」にドラフト表示を判定するための任意の文字列（例：`mydraftkey`）を入力します。省略した場合は既定値「1」が使用されます。

    ![「ドラフトキー」に文字列を入力したところ](https://pleasanter.org/files/images/ja/developers-guide/assets/7d955ef146a54aab9fbae5ccb9bcbd91.png)

1.  画面下部のコマンドボタンエリアにある追加ボタンまたは変更ボタンをクリックします。

    ![画面下部のコマンドボタンエリアにある追加ボタンと変更ボタン](https://pleasanter.org/files/images/ja/developers-guide/assets/cee8bbd09a394d4eac6ea426b819596b.png)

1.  「更新」ボタンをクリックします。
1.  作成したHTMLが保存されます。

    ![作成したHTMLが保存された状態](https://pleasanter.org/files/images/ja/developers-guide/assets/f524704caf434770b719094c671a94aa.png)

</div>

### 表示の確認

#### 動作イメージ

| 設定内容               | 通常表示     | ドラフト表示（?Draft=付与） |
| :--------------------- | :----------- | :-------------------------- |
| ドラフト時のみ出力     | 出力されない | 出力される                  |
| ドラフト時は出力しない | 出力される   | 出力されない                |

#### 表示の確認（一覧画面）

1.  テーブルの一覧の表示を確認します。はじめに、ドラフトキーを付与しない通常の表示でHTMLが表示されないことを確認します。

    ``` text
    http://{サーバ名}/items/{サイトID}/index
    ```

    ![ドラフトキーを付けない通常のURLで表示した一覧画面](https://pleasanter.org/files/images/ja/developers-guide/assets/aa0034bf318d4208b6d25ef5e304616f.png)

1.  ドラフトモードのテーブルの一覧の表示を確認します。一覧画面でドラフトキーを付与したURLを表示します。

    ``` text
    http://{サーバ名}/items/{サイトID}/index?Draft=mydraftkey
    ```

1.  一覧画面でドラフト表示が有効となるため、HTMLが表示されます。

    ![ドラフトキーを付けたURLで表示し、HTMLが表示された一覧画面](https://pleasanter.org/files/images/ja/developers-guide/assets/88e4612f0d5f4f9bb569dd6e63086fd7.png)

## APIでの設定

本機能はAPI（サイト設定の更新）からも設定できます。詳細は[サイト設定の更新（部分追加/更新/削除）](../../../developers-guide/api/site-operations/api-update-sitesettings.md)を参照ください。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.7.0 以降   | 機能追加 |

## 関連情報

-   [テーブルの管理：HTML](../html/index.md)
-   [テーブルの管理：スタイル](../styles/index.md)
-   [テーブルの管理：スクリプト](../scripts/index.md)
-   [サイト設定の更新（部分追加/更新/削除）](../../../developers-guide/api/site-operations/api-update-sitesettings.md)
