---
title: パラメータを手動で再設定する手順を知りたい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-merge-parameters
translationKey: faq-merge-parameters
shortname: パラメータを手動で再設定
created: 2024-08-30
updated: 2026-03-24
---

## 回答

パラメータファイルをバックアップしたのち、[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールのパラメータファイルとバックアップファイルのパラメータファイルを比較しながら最新バージョンモジュールのパラメータファイルに修正してください。

---

## 概要

パラメータファイルを手動で再設定する手順は以下の通りとなります。

## 1. パラメータファイルのバックアップ

1. パラメータファイルをバックアップします。このバックアップは手順3で使用します。パラメータファイルはマニュアル通りにセットアップした場合、C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\配下のjsonファイルとなります。
1. **拡張機能を利用していない場合は本手順は不要です。** 拡張機能で設定したパラメータファイルをバックアップします。このバックアップは手順4で使用します。拡張機能で設定したファイルはマニュアル通りにセットアップした場合、C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\配下にある以下サブフォルダ内のファイルとなります。

    |サブフォルダ名|拡張機能名|備考|
    |:---|:---|:---|
    |CustomDefinitions|[拡張項目](../../developers-guide/extended-features/extended-column.md)|組織、グループ、ユーザに項目を追加した際に生成されるフォルダ|
    |ExtendedFields|[拡張フィールド](../../developers-guide/extended-features/extended-fields.md)||
    |ExtendedHtmls|[拡張HTML](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)||
    |ExtendedNavigationMenus|[拡張ナビゲーションメニュー](../../developers-guide/extended-features/extended-navigationmenus.md)||
    |ExtendedScripts|[拡張スクリプト](../../developers-guide/extended-features/extended-script.md)||
    |ExtendedServerScripts|[拡張サーバスクリプト](../../developers-guide/extended-features/extended-server-script.md)||
    |ExtendedSqls|[拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)||
    |ExtendedStyles|[拡張スタイル](../../developers-guide/extended-features/extended-style.md)||

## 2. プリザンター最新バージョンの準備

1. [ダウンロードセンター](https://pleasanter.org/dlcenter)から、プリザンター最新バージョンをダウンロードします。
1. ダウンロードしたzipファイルを解凍します。

## 3. パラメータ再設定

手順1でダウンロードした最新バージョンモジュールのパラメータファイルに対して、現在設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールのパラメータファイルと手順2で取得したバックアップファイルのパラメータファイルを比較しながら最新バージョンモジュールのパラメータファイルを修正します。    
**Service.jsonのTimeZoneDefaultが正しい値か確認してください。TimeZoneDefaultにはPleasanterをインストールするサーバのOSで有効なタイムゾーンを設定してください。（Windowsなら"Tokyo Standard Time"など、Linuxなら"Asia/Tokyo"など）**  
[FAQ：プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい](faq-supported-language.md)  

## 4. 拡張機能の再設定

**拡張機能を利用していない場合は本手順は不要です。** 手順1.2で準備した最新バージョンモジュールの拡張機能用パラメータファイルに対して、現在設定済みの内容を反映します。[WinMerge](https://winmergejp.bitbucket.io/)などのファイル比較・マージツールを利用して最新バージョンモジュールの拡張機能用パラメータファイルと手順2で取得したバックアップファイルの拡張機能用パラメータファイルを比較しながら最新バージョンモジュールの拡張機能用パラメータファイルを修正します。