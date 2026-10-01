---
title: ER図表示
category: Pleasanter Site Visualizer
order: '0'
status: ''
parts: ''
urlstring: pleasanter-site-visualizer-how-to-use-display-er-diagram
translationKey: pleasanter-site-visualizer-how-to-use-display-er-diagram
shortname: ER図表示
created: 2025-09-11
updated: 2026-07-01
---

## 概要

[Pleasanter Site Visualizer](pleasanter-site-visualizer-how-to-use-sites.md)のER図表示機能について説明します。ログイン中のプリザンターのサイトのER図表示を行います。

### Pleasanter Site VisualizerにおけるER図

ER図（Entity Relationship Diagram）は、テーブル同士の関連性やテーブルに含まれる項目を可視化する図です。ER図の記法にはいくつかの種類がありますが、Pleasanter Site Visualizerは以下のようなER図を表示します。サイトを構成するデータを、エンティティ（＝テーブル）、リレーションシップ（＝リンク）、属性（＝項目）の3要素でモデル化しています。

![Pleasanter Site Visualizer が表示するER図の例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/bad6ec03f14f47f597e99fe5700ad7eb.png)

リレーションシップ（＝**リンク**）を示す線上には外部キー（＝**リンク項目**）が、線の両端には多重度を示すカーディナリティが表示されます。多重度は、あるテーブルの1件あたりのデータが、他のテーブルのいくつのデータに関連するかを表したものです。Pleasanter Site Visualizerでは「0または1」と「0以上」のみが表示されます。

各エンティティ（＝テーブル）表示の意味は、以下の表のとおりです。

| No  | 意味               | 説明                                                                     |
| :-: | ------------------ | ------------------------------------------------------------------------ |
|  1  | タイトル(サイトID) | テーブルのタイトルとサイトIDです。                                       |
|  2  | カラム名           | 「ClassA」などデータベース上のカラム名称です。                           |
|  3  | 項目名             | 「分類A」などのデフォルト名称です。                                      |
|  4  | PKまたはFK         | PKはID項目を、FKはリンク項目を表します。                                 |
|  5  | 表示名             | 「テーブルの管理：エディタ：項目の詳細設定：表示名」で設定した名称です。 |

## 前提条件

1. 「サイトの管理権限」が必要です。

## 1. 操作手順（共通 画面を表示・ファイルをDL）

1.  サイトの管理者権限のあるユーザでログインします。
1.  設定情報表示したいサイトに遷移します。
1.  [Pleasanter Site Visualizer](pleasanter-site-visualizer-how-to-use-sites.md)ブラウザ拡張アイコンをクリックします。

    | アイコン状態                                     | 説明                                                                                                                              |
    | ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
    | ![操作可能なことを示す青色の Pleasanter Site Visualizer 拡張アイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/f417493d09ea4674b479cda8e83c9722.png) | 青色アイコン時は操作が可能です。                                                                                                  |
    | ![操作できないことを示す灰色の Pleasanter Site Visualizer 拡張アイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/55a1df21737a4939ae762886e842144f.png) | 灰色アイコン時は操作が不可能です。 （ログインしていない、またはサイト管理が開けないページを開いている場合にこの状態となります。） |

1.  [Pleasanter Site Visualizer](pleasanter-site-visualizer-how-to-use-sites.md)の操作画面が表示されます。

    ![Pleasanter Site Visualizer の操作画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/feae119135ec4e2d886d585342f8d519.png)

## 2. 操作手順（画面を表示）

1. 「ER図を確認する」の「画面を表示」をクリックします。

       ![操作画面の「ER図を確認する」にある「画面を表示」ボタン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/7bfe8f2fad7c4bc38f8464fdcae25658.png)

1. 「ER図画面」が開きます。ER図の部分は、カーソルキーまたはマウスドラッグによるスクロール操作が可能です。

       ![開いたER図画面。左上に5つの操作ボタンが並ぶ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/2aa6dc77d5134eeaba6930165e2bb87c.png)

   画面左上には5つのボタンが並んでいます。5つのボタンの機能は以下の通りです。

| アイコン                                         | ボタン名    | 機能                                                              |
| :----------------------------------------------- | :---------- | :---------------------------------------------------------------- |
| ![「Zoom-in」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/94d44294525f49248d7ef6469c88c6a1.png) | Zoom-in     | クリックすると、ER図を1段階拡大表示します。                       |
| ![「Zoom-out」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/927bc29975514f239c35eb8632c4db5d.png) | Zoom-out    | クリックすると、ER図を1段階縮小表示します。                       |
| ![「Zoom-Reset」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/2b54f10318944ee9819af07eb47ae861.png) | Zoom-Reset  | クリックすると、ER図をウィンドウサイズで最大化します。            |
| ![「Save PNG」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/565fcb5befcc4cbdb9aa776d0ea5fa79.png) | Save PNG    | クリックすると、「PNG画像出力」ダイアログ（下記参照）が開きます。 |
| ![「Text Search」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/ae27eb734abe4897a208d152e50f4643.png) | Text Search | クリックすると、「ER図検索」ダイアログ（下記参照）が開きます。    |

### 「PNG画像出力」ダイアログ

ER図をPNG形式の画像としてダウンロードできます。

![ER図の「PNG画像出力」ダイアログ。幅と高さを指定できる](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/8c1d02371b3f4e9c80cd73f4b3bdd9f7.png)

このダイアログでは、出力するPNG画像の縦横サイズを指定できます。

| オプションの選択   | 効果                                                                                                                         |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| 「幅優先」を選択   | ・「幅(px)」を変更すると、縦横比を固定して「高さ(px)」を自動計算します。<br>・「高さ(px)」を変更すると、縦横比を無視します。 |
| 「高さ優先」を選択 | ・「高さ(px)」を変更すると、縦横比を固定して「幅(px)」を自動計算します。<br>・「幅(px)」を変更すると、縦横比を無視します。   |

### 「ER図検索」ダイアログ

「Text Search」ボタンをクリックすると、「ER図検索」ダイアログが開きます。検索結果とこのダイアログが重なって見づらい場合には、ドラッグして移動できます。

![ER図画面の「ER図検索」ダイアログ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/21041a2ec4324570a56743f7f98a4cf8.png)

#### テーブル名で検索する

テーブル名で検索すると、テーブル名(ID)が黄色でハイライトされ、テーブルがウィンドウにフィットするように拡大表示されます。

![テーブル名で検索し、該当テーブルが拡大表示されたER図](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/9ccc4d46822f4e8ebba1b5c1341b88fe.png)

#### カラム名で検索する

カラム名の一部で検索して複数ヒットした場合、最初に選択したカラムを含むテーブルがウィンドウにフィットするように拡大表示されます。続けて別のカラムを選択しても、拡大率は変わりません。

![カラム名の一部で検索して複数ヒットしたときのER図](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/4a442373f9c94a0cafeb8d71104ed0bf.png)

#### その他の検索

文字列「PK」または「FK」を検索すると、IDまたはリンク項目を確認できます。

![「PK」または「FK」で検索したときのER図](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/21c5376faac04b8eb9a8c29e041f74c7.png)

## 3. 操作手順（ファイルをDL）

1.  「ファイルをDL」をクリックします。

    ![操作画面の「ER図を確認する」にある「ファイルをDL」ボタン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/4633f537d79d42268e18548923e5cb91.png)

ER図をMermaid形式のテキストファイルとしてダウンロードできます。

### ダウンロードしたMermaid形式（.mmd）ファイルの利用方法

ダウンロードしたファイルは、[Mermaid Live Editor](https://mermaid.live/)などでプレビューできるほか、Markdownドキュメントにコードブロックとして埋め込むなどして活用できます。

以下の図はVS Codeに拡張機能[Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid)をインストールして表示させています。

![ダウンロードした.mmdファイルをVS Codeでプレビューした画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/1a6a12117cf64b3183c37b65369cb7dc.png)

## 対応バージョン

| 対応バージョン           | 内容     |
| :----------------------- | :------- |
| プリザンター1.4.21.0以降 | 新規作成 |

## 関連情報

-   [Pleasanter Site Visualizer：使い方：サイト設定表示](pleasanter-site-visualizer-how-to-use-sites.md)
-   [Mermaid Live Editor](https://mermaid.live/)
-   [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid)
