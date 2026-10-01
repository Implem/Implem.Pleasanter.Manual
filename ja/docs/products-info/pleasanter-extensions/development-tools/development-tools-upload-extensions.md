---
title: Extensionsテーブルへソースコードをアップロードする
category: 開発支援ツール
order: '6000'
status: ''
parts: ''
urlstring: development-tools-upload-extensions
translationKey: development-tools-upload-extensions
shortname: Pleasanter Extensions,Development Tools,Extensionsテーブルへソースコードをアップロード
created: 2025-01-27
updated: 2026-08-14
---

## 概要

ローカルPC内に格納されている拡張スクリプト、拡張サーバスクリプト、拡張SQL、拡張CSSなどのソースコードおよびJSON設定データをプリザンターのExtensionsテーブルにアップロードします。

![Development Tools の「Extensionsテーブルへソースコードをアップロード」の画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/aa0b12ec282149e49d4402125e61d205.png)

## 操作手順

<div class="steps" markdown>

1. [Settings.json](development-tools-setup.md)をエディタで開きます。
1. Environments にアップロードする環境の Environment を追加します。Name / Title / Dbms / ConnectionString を設定します。
1. BasePathにはソースコードの格納先の上位のディレクトリパスを指定します。
1. Extensions に ExtensionId / ExtensionName / ExtensionType / Path を指定します。
1. Implem.PleasanterManagementStudio.exe を起動します。
1. 環境の一覧から対象の環境をクリックして選択します。
1. 画面上部のメニューから [Run]-[Extensions]-[Upload Extensions] をクリックします。
1. ダイアログの確認事項をチェックし「はい(Y)」をクリックします。
1. 画面上部のメニューから [File]-[Open log folder] をクリックしてログフォルダを開きます。
1. ログフォルダ内の [UploadExtensions] フォルダを開き変更前と変更後のソースコードを確認します。画面上部のメニューから[Extensions]-[Open folder: Upload Extensions]をクリックして同フォルダを開くこともできます。

</div>

## 関連情報

-   [Development Tools：セットアップ、起動方法](development-tools-setup.md)
