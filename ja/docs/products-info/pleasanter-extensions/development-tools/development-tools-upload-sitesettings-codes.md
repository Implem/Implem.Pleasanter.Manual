---
title: 特定のサイトにソースコードをアップロードする
category: 開発支援ツール
order: '4000'
status: ''
parts: ''
urlstring: development-tools-upload-sitesettings-codes
translationKey: development-tools-upload-sitesettings-codes
shortname: Pleasanter Extensions,Development Tools,サイトにソースコードをアップロード
created: 2025-01-27
updated: 2025-02-14
---

## 概要

ローカルPC内に格納されているスクリプト、サーバスクリプト、CSSなどのソースコードをプリザンターの特定のサイトにアップロードします。

![Development Tools の「特定のサイトにソースコードをアップロード」の画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/6df8971d7c554e5aa6de25a00ff368ce.png)

## 制限事項

1. 条件の設定は行えません。条件はプリザンターのWEB画面から設定する必要があります。

## 操作手順

<div class="steps" markdown>

1. [Settings.json](development-tools-setup.md)をエディタで開きます。
1. Environments にアップロードする環境の Environment を追加します。Name / Title / Dbms / ConnectionString を設定します。
1. BasePathにはソースコードの格納先の上位のディレクトリパスを指定します。
1. Codes にアップロードする先の SiteId を設定します。またコードの Id / Title / Type / Path を指定します。
1. Implem.PleasanterManagementStudio.exe を起動します。
1. 環境の一覧から対象の環境をクリックして選択します。
1. 画面上部のメニューから [Run]-[Codes]-[Upload SiteSettings codes] をクリックします。
1. ダイアログの確認事項をチェックし「はい(Y)」をクリックします。
1. 画面上部のメニューから [File]-[Open log folder]をクリックしてログフォルダを開きます。
1. ログフォルダ内の [SiteSettingsConvertLog] フォルダを開き変更前と変更後のソースコードを確認します。画面上部のメニューから[Codes]-[Open folder: SiteSettings convert log]をクリックして同フォルダを開くこともできます。

</div>

## 関連情報

-   [Development Tools：セットアップ、起動方法](development-tools-setup.md)
