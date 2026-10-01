---
title: サイト設定表示
category: Pleasanter Site Visualizer
order: '3000'
status: ''
parts: ''
urlstring: pleasanter-site-visualizer-how-to-use-sites
translationKey: pleasanter-site-visualizer-how-to-use-sites
shortname: Pleasanter Site Visualizer
created: 2025-08-04
updated: 2026-05-18
---

## 概要

[Pleasanter Site Visualizer](index.md)のサイトの設定情報表示機能について説明します。ログイン中のプリザンターのサイトの設定情報表示を行います。

## 前提条件

1. 「サイトの管理権限」が必要です。

## 1. 操作手順（共通 画面を表示・ファイルをDL）

1.  サイトの管理者権限のあるユーザでログインします。
1.  設定情報表示したいサイトに遷移します。
1.  [Pleasanter Site Visualizer](index.md)ブラウザ拡張アイコンをクリックします。

    | アイコン状態                                     | 説明                                                                                                                             |
    | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
    | ![操作可能なことを示す青色の Pleasanter Site Visualizer 拡張アイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/f417493d09ea4674b479cda8e83c9722.png) | 青色アイコン時は操作が可能です。                                                                                                 |
    | ![操作できないことを示す灰色の Pleasanter Site Visualizer 拡張アイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/55a1df21737a4939ae762886e842144f.png) | 灰色アイコン時は操作が不可能です。（ログインしていない、またはサイト管理が開けないページを開いている場合にこの状態となります。） |

1. 「Pleasanter Site Visualizer」の操作画面が表示されます。

    ![Pleasanter Site Visualizer の操作画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/fea63184d4644eba9e53dba40d1a420f.png)

## 2. 操作手順（画面を表示）

1.  「サイト設定を確認する」の「画面を表示」をクリックします。

    ![操作画面の「サイト設定を確認する」にある「画面を表示」ボタン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/80c7f5d28b184cf3ad2304713db2b164.png)

1.  別ウィンドウにサイト設定情報が表示されます。

    ![別ウィンドウに表示されたサイト設定情報の画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/8acb538adf8c42fd9d9752ec382abd5b.png)

    オプション項目でサイトID、サイトグループ名を指定した場合は画面右上のドロップダウンリストで表示するサイトを切り替えることができます。

    ![サイト設定情報画面の右上にある、表示するサイトを切り替えるドロップダウンリスト](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/37ee16d39870451db07f22b96b243b16.png)

1.  画面上部のボタン操作により、下部表示を切り替えられます。

    ![サイト設定情報画面。上部のボタンで下部の表示内容を切り替える](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/023c9d80a58448d8a6a7d33ae6c0c3c6.png)

## 3. 操作手順（ファイルをDL）

1. 「サイト設定を確認する」の「ファイルをDL」をクリックします。

    ![操作画面の「サイト設定を確認する」にある「ファイルをDL」ボタン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/edcab6ec42da41eb92ffdac0a92daa64.png)

1. zip形式で圧縮されたExcelファイルがダウンロードされます。サイト毎にExcelファイルが生成されます。オプション項目でサイトID、サイトグループ名を指定した場合はzipファイル内に複数のExcelファイルが格納されます。

    ![サイト設定のExcelファイルを含むzipファイルがダウンロードされた状態](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/748ba19e08c840a3be89c0cca1657fa7.png)

### オプション項目の説明

#### 新しいウィンドウで開く

2回目以降の「画面を表示」を行った際の設定情報表示画面を新しいウィンドウで開きます。チェックOFFの場合は既に開いているウィンドウの内容が変更します。

#### サイトID

指定したサイトIDの設定情報を表示します。指定方法は以下の表を参照してください。複数のサイトを指定する場合はカンマ（,）区切りで入力します。「サイトグループ名」との併用はできません。

| 指定例  | 表示対象のデータ                                                     |
| :------ | :------------------------------------------------------------------- |
| 213     | サイトIDが213のサイトのバージョン1                                   |
| 543-21  | サイトIDが543のサイトのバージョン21                                  |
| 5,4     | サイトIDが5のサイトのバージョン1と、サイトIDが4のサイトのバージョン1 |
| 5-4,3-2 | サイトIDが5のサイトのバージョン4と、サイトIDが3のサイトのバージョン2 |

![操作画面のオプション項目「サイトID」の入力欄](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/fa3535121eee41d8a4c23f42c895e390.png)

### サイトグループ名

指定したグループ名を持つサイトの設定情報を表示します。複数指定はできません。「サイトID」との併用はできません。

## 対応バージョン

| 対応バージョン            | 内容     |
| :------------------------ | :------- |
| プリザンター1.4.19.0 以降 | 機能追加 |
