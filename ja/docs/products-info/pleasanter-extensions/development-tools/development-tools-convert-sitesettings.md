---
title: サイト設定の移行
category: 開発支援ツール
order: '7000'
status: ''
parts: ''
urlstring: development-tools-convert-sitesettings
translationKey: development-tools-convert-sitesettings
shortname: Pleasanter Extensions,Development Tools,サイト設定の移行
created: 2025-01-27
updated: 2025-02-14
---

## 概要

開発環境から本番環境への移行などサイト情報を移行します。同一サーバ内での移行、異なるサーバ間での移行、異なるDbms間での移行が可能です。移行時にサイトID、ユーザID、組織ID、グループIDの読み替えを行います。

![Development Tools の「サイト設定の移行」の画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/development-tools/assets/3591ba4de4434cfb8b62f165ff4f6f4a.png)

## 制限事項

1. レコードおよび添付ファイル、画像などは移行できません。
1. [組織](../../../managers-guide/department-administration/index.md)、[グループ](../../../managers-guide/group-administration/index.md)、[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)は移行できません。組織、グループ、ユーザに紐づくアクセス権は移行できます。
1. [横断検索を無効化](../../../managers-guide/manage-table/search/table-management-disable-cross-search.md)のチェックボックスの設定は移行できません。

## 操作手順

<div class="steps" markdown>

1. [Settings.json](development-tools-setup.md)をエディタで開きます。
1. Environments に移行先の環境の Environment を追加します。Name / Title / Dbms / ConnectionString を設定します。
1. 移行元の Environment の DestinationName に 移行先の環境の Environment の Name を指定します。
1. TargetSites に移行元の対象サイトの SiteId / DestinationId / Subtree を設定します。
1. Implem.PleasanterManagementStudio.exe を起動します。
1. 環境の一覧から対象の環境をクリックして選択します。
1. 画面上部のメニューから [Run]-[Sites]-[Convert SiteSettings]をクリックします。
1. ダイアログの確認事項をチェックし「はい(Y)」をクリックします。
1. 画面上部のメニューから [File]-[Open log folder] をクリックしてログフォルダを開きます。
1. ログフォルダ内の [SiteSettingsConvertLog] フォルダを開き移行前と移行後のサイト設定を確認します。画面上部のメニューから[Sites]-[Open folder: SiteSettings convert log]をクリックして同フォルダを開くこともできます。

</div>

## 関連情報

-   [組織管理機能](../../../managers-guide/department-administration/index.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [テーブルの管理：検索：検索の設定：横断検索を無効化](../../../managers-guide/manage-table/search/table-management-disable-cross-search.md)
-   [Development Tools：セットアップ、起動方法](development-tools-setup.md)
