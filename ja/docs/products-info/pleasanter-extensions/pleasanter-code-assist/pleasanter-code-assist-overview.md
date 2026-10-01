---
title: 機能概要
category: Pleasanter Code Assist
order: '1000'
status: ''
parts: ''
urlstring: pleasanter-code-assist-overview
translationKey: pleasanter-code-assist-overview
shortname: Pleasanter Code Assist
created: 2025-02-17
updated: 2026-09-11
---

## 概要

Pleasanter Code Assistはプリザンターの開発者向けに快適な開発体験を提供するソフトウェアです。Visual Studio Codeでスクリプトなどのソースコードの保存と同時にプリザンターへの登録・更新ができます。

### 特徴

1.  Visual Studio Codeでソースコードを保存すると同時にプリザンターへ登録・更新

    プリザンターのカスタマイズ開発の中心となる[スクリプト](../../../developers-guide/script/index.md)や[サーバスクリプト](../../../developers-guide/server-script/index.md)、[スタイル](../../../developers-guide/style/index.md)、[HTML](../../../managers-guide/manage-table/html/index.md)の設定は、テーブルの管理を開いてスクリプトなどを入力し登録更新という手順ですが、Pleasanter Code AssistではVisual Studio Code上でソースコードの保存と同時に指定のテーブルへ登録・更新します。これにより、開発のたびにテーブルの管理を開くわずらわしさから解放され、また強力な機能を備えたVisual Studio Codeの利用でより快適に開発を行うことができます。また、[拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)や[拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)、[拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)、[拡張スタイル](../../../developers-guide/extended-features/extended-style.md)も登録・更新できます。

    ![Visual Studio Codeでの保存と同時にプリザンターへ登録・更新するイメージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/616b3156553e46b4939dc52af1913367.png)

2. Visual Studio Codeの拡張機能として提供

    Pleasanter Code AssistはVisual Studio Codeの拡張機能として提供します。これによりクライアントはWindows、Linux、MacいずれのOS端末でも開発可能です。またその他の拡張機能もそのまま利用可能ですので、現在お使いのVisual Studio Codeの環境をそのまま使用できます。合わせてVisual Studio CodeのGitHub連携機能も利用することでソースコードの管理もより容易に行えます。

## 動作環境

Pleasanter Code AssistはVisual Studio Codeの拡張機能として提供します。Visual Studio Codeが動作する環境でご利用できます。

## 制限事項

1.  Community Editionのプリザンターに対しては利用できません。（ただしPleasanter Extensionsの[トライアル](../../../developers-guide/index.md)実施中を除きます）
1.  Pleasanter.netに対しては利用できません。
1.  デモ環境に対してはサイトへの登録・更新が利用できます。拡張機能テーブルへの登録・更新は利用できません。
1.  Visual Studio Code for Webでは動作しません。

## 前提条件

1. 本ソフトウェアを使用するには、以下のいずれかの条件を満たしている必要があります。

    -   利用環境のプリザンターにEnterprise Edition[^1]が適用されている
    -   利用環境のプリザンターでPleasanter Extensionsの[トライアル](../../../developers-guide/index.md)を実施中である

1.  本ソフトウェアは利用環境のプリザンターのバージョンがver.1.4.13.0以降で動作します。プリザンターver.1.4.13.0より前のバージョンをご利用中の場合は、プリザンターをバージョンアップしてください。
1.  本ソフトウェアはVisual Studio Code ver1.95以降で動作します。Visual Studio Code ver1.95より前のバージョンをご利用中の場合は、Visual Studio Codeをバージョンアップしてください。  

[^1]: Enterprise Editionにつきましては「プリザンター年間サポートサービス」サービス仕様書を参照してください。

## セットアップ、事前準備

Pleasanter Code Assistのセットアップおよび事前準備は以下ページを参照ください。

-   [Pleasanter Code Assist：セットアップ、事前準備](pleasanter-code-assist-setup.md)

## 機能一覧

Pleasanter Code Assistは以下の機能を提供します。利用方法の詳細は以下ページを参照ください。

-   [Pleasanter Code Assist：使い方：サイト](pleasanter-code-assist-how-to-use-sites.md)  
-   [Pleasanter Code Assist：使い方：拡張機能](pleasanter-code-assist-how-to-use-extensions.md)

| 機能名                   | 概要                                                                                   |
| ------------------------ | -------------------------------------------------------------------------------------- |
| サイト：スクリプト       | 指定のサイトにスクリプトを登録・更新します。                                           |
| サイト：サーバスクリプト | 指定のテーブルにサーバスクリプトを登録・更新します。                                   |
| サイト：スタイル         | 指定のサイトにスタイルを登録・更新します。                                             |
| サイト：HTML             | 指定のサイトにHTMLを登録・更新します。                                                 |
| 拡張スクリプト           | 拡張機能テーブル（Extensionsテーブル）に設定情報とスクリプトを登録・更新します。       |
| 拡張サーバスクリプト     | 拡張機能テーブル（Extensionsテーブル）に設定情報とサーバスクリプトを登録・更新します。 |
| 拡張スタイル             | 拡張機能テーブル（Extensionsテーブル）に設定情報とスタイルを登録・更新します。         |
| 拡張SQL                  | 拡張機能テーブル（Extensionsテーブル）に設定情報とSQLを登録・更新します。              |

### 拡張機能テーブル（Extensionsテーブル）について

[拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)や[拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)などの拡張機能を利用する際は設定情報を含むJSONファイルやソースコードファイルを所定のフォルダに格納して利用する仕組みですが、拡張機能テーブル（Extensionsテーブル）へ設定情報とソースコードを登録することで拡張機能を利用することが可能です。Pleasanter Code Assistでは拡張スクリプト、拡張サーバスクリプト、拡張スタイル、拡張SQLの4種類を拡張機能テーブル（Extensionsテーブル）へアップロードすることができます。

![拡張機能テーブルに設定情報とソースコードを登録するイメージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/ad191aa2553a4d55bc3b6496cbfeee0b.png)

| 拡張機能名                                                | Pleasanter Code Assistで対応 |
| --------------------------------------------------------- | ---------------------------- |
| [拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)             | －                           |
| [拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)                                | ○                            |
| [拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)         | ○                            |
| [拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)                      | ○                            |
| [拡張スタイル](../../../developers-guide/extended-features/extended-style.md)                         | ○                            |
| [拡張ナビゲーションメニュー](../../../developers-guide/extended-features/extended-navigationmenus.md) | －                           |
| [拡張フィールド](../../../developers-guide/extended-features/extended-fields.md)                      | －                           |
| [拡張項目](../../../developers-guide/extended-features/extended-column.md)                            | －                           |

また、拡張スクリプト、拡張スタイルは所定のフォルダに格納する従来の拡張機能の設定では、フォルダに設定したスクリプト、スタイルがプリザンターの全ページに適用する仕様でしたが、Pleasanter Code Assistを利用すると、拡張SQLや拡張サーバスクリプトと同様に、適用するサイトや組織・グループ・ユーザなどをきめ細かく指定することができるようになります。

### 拡張機能テーブル（Extensionsテーブル）の制限事項

**プリザンターのバージョン1.4.16.0から、セキュリティ強化のため利用条件が変更されています。バージョン1.4.16.0以降にアップデートのうえ、必要なときのみ「Extensions APIを許可」チェックボックスをオンにして利用してください。**

### 利用条件

拡張機能テーブル（Extensionsテーブル）を利用するには、以下の条件を満たしている必要があります。

#### バージョン1.4.16.0 以降の利用条件

1.  特権ユーザでログイン後、[テナントの管理](../../../managers-guide/tenant-administration/index.md)画面で「Extensions APIを許可する」のチェックをオンにする
1.  特権ユーザのAPIキーを使用する

#### バージョン1.4.15.0以前の利用条件

1.  テナント管理者のAPIキーを使用する

## 動作イメージ

![Pleasanter Code Assist の動作イメージのアニメーション](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/d96af949d8a94e29b0a8506c8c71d90a.gif)

## 対応バージョン

| 対応バージョン            | 内容                                                   |
| :------------------------ | :----------------------------------------------------- |
| プリザンター1.4.16.0 以降 | 拡張機能テーブル（Extensionsテーブル）の制限事項を追加 |

## 関連情報

### Pleasanter Code Assist

-   [Pleasanter Code Assist：セットアップ、事前準備](pleasanter-code-assist-setup.md)
-   [Pleasanter Code Assist：使い方：サイト](pleasanter-code-assist-how-to-use-sites.md)
-   [Pleasanter Code Assist：使い方：拡張機能](pleasanter-code-assist-how-to-use-extensions.md)

### Pleasanter Extensionsトライアル

-   [Pleasanter Extensionsのトライアル](../../../developers-guide/index.md)

### テーブルの管理

-   [HTML](../../../managers-guide/manage-table/html/index.md)

### テーブルの管理：エディタ：項目の詳細設定

-   [拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)

### 開発者ガイド

-   [スクリプト](../../../managers-guide/manage-table/scripts/index.md)
-   [サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [スタイル](../../../developers-guide/style/index.md)

### 開発者ガイド：拡張機能

-   [拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)
-   [拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)
-   [拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)
-   [拡張スタイル](../../../developers-guide/extended-features/extended-style.md)
-   [拡張ナビゲーションメニュー](../../../developers-guide/extended-features/extended-navigationmenus.md)
-   [拡張フィールド](../../../developers-guide/extended-features/extended-fields.md)
-   [拡張項目](../../../developers-guide/extended-features/extended-column.md)
