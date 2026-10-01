---
title: HTML
category: HTML
order: '0'
status: ''
parts: ''
urlstring: insert-html
translationKey: insert-html
shortname: HTML
created: 2023-09-14
updated: 2026-08-12
---

## 概要

外部コンテンツ(JavaScriptやCSSライブラリ等)を読み込むためのHTMLを挿入する機能です。

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作方法

1.  [テーブルの管理](../index.md)または「ダッシュボードの管理」で「HTML」タブを選択してください。

    ![テーブルの管理の「HTML」タブ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/html/assets/5e94fb07cc164333b7dc9dc3d7fb8378.png)

1.  「新規作成」ボタンまたは「HTML一覧」から登録済みのHTMLをクリックしてください。
1.  以下のようなダイアログが表示されます。

    ![HTMLを登録するダイアログ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/html/assets/e69d8e7d83284afd8f9c7eca7b494002.png)

1.  以下の各項目を設定し、「追加」ボタンまたは「変更」ボタンをクリックしてください。
    設定可能な挿入位置は以下の通りです。

    | No. | 挿入位置           | 説明                                          |
    | :-- | :----------------- | :-------------------------------------------- |
    | 1   | Head top           | headタグ内のmetaタグの上にHTMLを挿入します。  |
    | 2   | Head bottom        | headタグ内のtitleタグの下にHTMLを挿入します。 |
    | 3   | Body script top    | scriptタグの上にHTMLを挿入します。            |
    | 4   | Body script bottom | scriptタグの下にHTMLを挿入します。            |

1.  コマンドボタンエリアにある「更新」ボタンをクリックしてください。

## 使用例

以下のようなHTMLを登録することで、外部コンテンツを読み込めます。

-   スタイル

    ``` html
    <link href="https://cdnjs.cloudflare.com/ajax/libs/pivottable/2.23.0/pivot.min.css" rel="stylesheet" />
    ```

-   スクリプト

    ``` html
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pivottable/2.23.0/pivot.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pivottable/2.23.0/pivot.jp.min.js"></script>
    <script src="https://cdn.plot.ly/plotly-basic-latest.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pivottable/2.23.0/plotly_renderers.min.js"></script>
    ```

## 全て無効化

HTML一覧の上部にある「全て無効化」チェックボックスにチェックを入れると、設定済みのすべてのHTMLを無効にすることができます。

![HTML一覧の上部にある「全て無効化」チェックボックス](https://pleasanter.org/files/images/ja/managers-guide/manage-table/html/assets/0cb91e122be941bfbcab680d4e3c08a4.png)

!!! warning
    この設定を行っても、個別のHTMLの「無効」チェックボックスの状態は変わりません。

## コードエディタの使用

第2世代[ユーザインターフェースのテーマ](../../user-administration/user-management-theme.md)の場合は、ハイライトやコードヒント・タブキーでのインデント入力などをサポートする便利なコードエディタ機能が利用できます。

[General.json](../../../setup/parameters/general.json.md)の"EnableCodeEditor"を有効化することで利用可能です。

![コードエディタでHTMLを編集している画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/html/assets/b5af456fd99448eb86552d822deb2ba6.png)

## 対応バージョン

| 対応バージョン | 内容                   |
| :------------- | :--------------------- |
| 1.4.14.0 以降  | 「全て無効化」機能追加 |

## 関連情報

-   [テーブルの管理](../index.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](../../user-administration/user-management-theme.md)
