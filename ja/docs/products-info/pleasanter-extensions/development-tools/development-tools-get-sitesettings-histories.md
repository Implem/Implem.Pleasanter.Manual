---
title: サイト設定の変更履歴を取得する
category: 開発支援ツール
order: '8000'
status: ''
parts: ''
urlstring: development-tools-get-sitesettings-histories
translationKey: development-tools-get-sitesettings-histories
shortname: Pleasanter Extensions,Development Tools,サイト設定の変更履歴
created: 2025-01-27
updated: 2025-02-14
---

## 概要

対象のサイト設定の変更履歴をログフォルダに取得します。

![Development Tools の「サイト設定の変更履歴を取得」の画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/0fb552ac42b443b98a3427f35d53d3c1.png)

## 操作手順

<div class="steps" markdown>

1. [Settings.json](development-tools-setup.md)をエディタで開きます。
1. Environments に取得するサイトの環境の Environment を追加します。Name / Title / Dbms / ConnectionString を設定します。
1. TargetSites に取得する対象サイトの SiteId / Subtree を設定します。
1. Implem.PleasanterManagementStudio.exe を起動します。
1. 環境の一覧から対象の環境をクリックして選択します。
1. 画面上部のメニューから [Run]-[Sites]-[Get SiteSettings histories] をクリックします。
1. ダイアログの確認事項をチェックし「はい(Y)」をクリックします。
1. 画面上部のメニューから [File]-[Open log folder]をクリックしてログフォルダを開きます。
1. ログフォルダ内の [SiteSettingsHistories] フォルダを開き取得したサイト設定の変更履歴を確認します。画面上部のメニューから[Sites]-[Open folder: SiteSettings histories]をクリックして同フォルダを開くこともできます。

</div>

## 関連情報

-   [Development Tools：セットアップ、起動方法](development-tools-setup.md)
