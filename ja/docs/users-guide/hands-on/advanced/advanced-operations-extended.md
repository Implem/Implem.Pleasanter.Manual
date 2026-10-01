---
title: スクリプト、サーバスクリプト、スタイル、拡張機能
category: 操作ガイド（応用編）
order: '80'
status: ''
parts: ''
urlstring: advanced-operations-extended
translationKey: advanced-operations-extended
shortname: 拡張機能
created: 2023-09-20
updated: 2024-12-19
---

## 概要

プリザンターはノーコード開発ツールとして簡単な操作で業務アプリをすばやく作成できます。またローコード開発ツールとして[スクリプト](../../../managers-guide/manage-table/scripts/index.md)、[サーバスクリプト](../../../developers-guide/server-script/index.md)、[API](../../../developers-guide/api/basics/api.md)、[拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)など豊富な[開発者向け機能](../../../developers-guide/index.md)を用意しているので、標準機能だけでは実現が難しい複雑な業務要件にも対応できます。

ここでは開発者向け機能の概要を紹介します。

## API

プリザンターが提供する[API](../../../developers-guide/api/basics/api.md)はサイトおよびレコードの登録・参照・更新・削除の基本操作の他、メール送信や任意のSQLを実行する機能があります。APIを使用することで、他システムとのデータ連携を行うことができます。プリザンターのAPIはWEB APIですので、外部システムからのAPI操作だけでなく、PowerShellやPythonなどのスクリプト言語によるバッチ処理などで利用できます。また後述の[スクリプト](../../../managers-guide/manage-table/scripts/index.md)ではプリザンター内のテーブルからのデータ取得、登録更新削除などのビジネスロジックの作成に利用できます。

## スクリプト

クライアントサイドでJavaScriptを実行し、標準機能では実現できないUI操作やUI操作に伴った追加処理を行うことができます。実装はプレーンなJavaScriptに加え、jQueryが利用可能です。レコードIDの取得、画面項目の値取得の関数や、一覧画面表示時、編集画面更新前に動作する関数の他、プリザンターAPI実行関数などスクリプト専用関数を豊富に準備しているので、標準機能で実現できない追加処理を素早く高品質で実装することができます。また外部ライブラリを導入することで、グラフ表示やピボットテーブルなど様々な機能をプリザンター上で利用することができます。

## サーバスクリプト

サーバサイドでJavaScriptを実行し、条件分岐、計算、文字列処理、レコードの操作、メールやチャットへの通知、動的なアクセス制御等を行うことが可能です。実装はプレーンなJavaScriptが利用できます。データ取得、他テーブルレコード取得の他、画面設定情報の取得・更新、ビュー情報の設定などサーバスクリプト専用のメソッド、プロパティを豊富に準備しているので、標準機能で実現できない追加処理を素早く高品質で実装することができます。

## スクリプトとサーバスクリプトの違い

スクリプトとサーバスクリプトの大きな違いは、動作場所になります。その他の違いについては下記の通りです。

| 内容                   | スクリプト                                                                           | サーバスクリプト                                                                                                       |
| :--------------------- | :----------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------- |
| 動作場所               | クライアントサイド                                                                   | サーバサイド                                                                                                           |
| 動作トリガ             | 画面上の操作（画面表示、ボタン押下、値変更等）。それぞれの操作に対する処理を実装する | サーバ側での処理タイミング（画面表示の前、作成後等）。詳細は「サーバスクリプト：条件」で定義。                         |
| 外部API呼び出し        | 可能。$.ajaxなどで実装。プリザンターAPIの場合は専用スクリプト（$p.api〇〇）あり。    | 可能。専用メソッドあり（[httpClient](../../../developers-guide/server-script/httpClient/index.md)） |
| 外部ライブラリ読み込み | 可能                                                                                 | 不可能                                                                                                                 |

## スタイル

一覧画面で1行毎に背景色を変える、指定した列の背景色を変える、編集画面で指定した項目の文字を強調する、ボタンのフォントサイズを大きくするなど、標準と異なるデザインを指定することができます。スタイルはCSS（Cascading Style Sheets）で記述します。一覧画面や編集画面の項目の設定でCSSを設定できるほか、スクリプトやサーバスクリプトで様々な処理と組み合わせてCSSを設定することができます。

## 拡張機能

[スクリプト](../../../managers-guide/manage-table/scripts/index.md)、[サーバスクリプト](../../../developers-guide/server-script/index.md)、[API](../../../developers-guide/api/basics/api.md)、[スタイル](../../../developers-guide/style/index.md)の他に更なる拡張機能を用意しています。

### 拡張HTML

ログイン画面入力フォームの上部などに自由にHTMLを差し込むことが可能です。スクリプトの実装をせずに個別の説明文を差し込むことができます。

### 拡張SQL

拡張SQLは、プリザンターがデータベースに対して発行するSQL処理を、プログラミングによってカスタマイズする機能です。

1.  **レコードの作成前、更新後などのデータ反映時のタイミングで任意のSQLを追加、実行することができる**

    ［例］レコードの新規作成のタイミングで、別テーブルのレコードを更新

1.  **リンクサーバ（SQL Server）またはDBリンク（PostgreSQL）を利用することで、別システムのデータベースに対してSQLを実行できる**<br>

1.  **プリザンター内で発生するイベントに対して、対象をWhere句やOrderBy句で制御できる**

    ［例］レコードのアクセス制御を利用せず、より細かい条件でレコード単位のアクセス制御を実現  
    ［例］特定グループのメンバーのみ二段階認証をスキップ

1.  **APIから呼び出して実行できる**  

    ［例］スクリプト、サーバスクリプトからデータベース内のデータを直接取得・更新する処理を実装

### 拡張スクリプト、拡張サーバスクリプト、拡張スタイル

スクリプト、サーバスクリプト、スタイルは[テーブルの管理](../../../managers-guide/manage-table/index.md)にてテーブル単位での設定を行いますが、プリザンター全体で利用するようなケースにおいてはこちらの機能で一括管理することができます。

### 拡張ナビゲーションメニュー

ナビゲーションメニューの表示内容はパラメータファイル「NavigationMenu.json」にて既定値として設定済みです。この機能を利用することで、ナビゲーションメニューの追加・置換・削除を細かく指定することができます。

### 拡張フィールド

テーブルに存在しない項目を一覧画面のフィルタに追加することができます。この機能を利用することで、検索条件を任意に拡張することができます。

### 拡張項目

組織の管理、グループの管理、ユーザの管理に[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)や[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)などの項目を追加することができます。

## 関連情報

-   [テーブルの管理：スクリプト](../../../managers-guide/manage-table/scripts/index.md)
-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)
-   [開発者ガイド：API](../../../developers-guide/api/basics/api.md)
-   [開発者ガイド：拡張機能：拡張SQL](../../../developers-guide/extended-features/extended-sql/index.md)
-   [開発者ガイド](../../../developers-guide/index.md)
-   [開発者ガイド：サーバスクリプト：httpClient](../../../developers-guide/server-script/httpClient/index.md)
-   [開発者ガイド：スタイル](../../../developers-guide/style/index.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
