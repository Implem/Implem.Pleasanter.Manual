---
title: Extensionsテーブルからソースコードを取得する
category: 開発支援ツール
order: '5000'
status: ''
parts: ''
urlstring: development-tools-get-extensions
translationKey: development-tools-get-extensions
shortname: Pleasanter Extensions,Development Tools,Extensionsテーブルからソースコードを取得
created: 2025-01-27
updated: 2025-02-14
---

## 概要

プリザンターのExtensionsテーブルから、拡張スクリプト、拡張サーバスクリプト、拡張SQL、拡張CSSなどのソースコードおよびJSON設定データを取得します。

![Development Tools の「Extensionsテーブルからソースコードを取得」の画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/7bb1cf370f78434ab4141ba0e55b7c6e.png)

## 操作手順

<div class="steps" markdown>

1. [Settings.json](development-tools-setup.md)をエディタで開きます。
1. Environments に取得する環境の Environment を追加します。Name / Title / Dbms / ConnectionString を設定します。
1. BasePathにはソースコードの格納先の上位のディレクトリパスを指定します。
1. Extensions に ExtensionId / ExtensionName / ExtensionType / Path を指定します。
1. Implem.PleasanterManagementStudio.exe を起動します。
1. 環境の一覧から対象の環境をクリックして選択します。
1. 画面上部のメニューから [Run]-[Extensions]-[Get Extensions] をクリックします。
1. ダイアログの確認事項をチェックし「はい(Y)」をクリックします。
1. 画面上部のメニューから [File]-[Open log folder] をクリックしてログフォルダを開きます。
1. ログフォルダ内の [GetExtensions] フォルダを開き変更前と変更後のソースコードを確認します。画面上部のメニューから[Extensions]-[Open folder: Get Extensions]をクリックして同フォルダを開くこともできます。

</div>

## 関連情報

-   [Development Tools：セットアップ、起動方法](development-tools-setup.md)
