---
title: コマンドボタンの表示／非表示を制御したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-command-button
translationKey: faq-command-button
shortname: ''
created: 2024-02-07
updated: 2024-06-21
---

## 回答

[サイトのアクセス制御](../../managers-guide/manage-table/site-access-control/index.md)や[テーブルの管理](../../managers-guide/manage-table/index.md)、[スクリプト](../../managers-guide/manage-table/scripts/index.md)、[スタイル](../../developers-guide/style/index.md)、[サーバスクリプト](../../developers-guide/server-script/index.md)で制御します。

---

## 概要

Pleasanterの画面下部に表示されるコマンドボタンの表示・非表示制御は、ボタンの種類により異なります。

![画面下部に並ぶコマンドボタンの例](https://pleasanter.org/files/images/ja/FAQ/editor/assets/e508b79fddea4279889b34b8db5bb6d0.png)

設定方法は以下のとおりです。

|ボタン種類|画面分類|制御方法|マニュアルリンク|
|:----|:----|:----|:----|
|戻る|一覧|テーブルの管理 > スタイルから、CSSで設定します|[FAQ：サンプルコード：特定のボタンを非表示にしたい](faq-hide-button.md)|
|一括削除|一覧|テーブルの管理 > サイトのアクセス制御で設定します|[サイト機能：アクセス制御](../../managers-guide/manage-table/site-access-control/index.md)|
|インポート|一覧|テーブルの管理 > サイトのアクセス制御で設定します|[サイト機能：アクセス制御](../../managers-guide/manage-table/site-access-control/index.md)|
|エクスポート|一覧|テーブルの管理 > サイトのアクセス制御で設定します|[サイト機能：アクセス制御](../../managers-guide/manage-table/site-access-control/index.md)|
|編集モード|一覧|テーブルの管理 > 一覧から一覧編集種別を設定します|[テーブルの管理：一覧画面：一覧編集種別](../../managers-guide/manage-table/grid/table-management-grid-editor-type.md)|
|実行|一覧|テーブルの管理 > プロセスで設定します|[テーブルの管理：プロセス](../../managers-guide/manage-table/process/index.md)|
|戻る|編集|テーブルの管理 > スタイルから、CSSで設定します|[FAQ：サンプルコード：特定のボタンを非表示にしたい](faq-hide-button.md)|
|作成|編集（新規作成時）|テーブルの管理 > スタイルから、CSSで設定します|[FAQ：サンプルコード：特定のボタンを非表示にしたい](faq-hide-button.md)|
|更新|編集（更新時）|テーブルの管理 > スタイルから、CSSで設定します|[FAQ：サンプルコード：特定のボタンを非表示にしたい](faq-hide-button.md)|
|参照コピー|編集|テーブルの管理 > エディタから参照コピーを設定します|[テーブルの管理：エディタ：参照コピーを許可](../../managers-guide/manage-table/editor/allow-reference-copy/index.md)|
|コピー|編集|テーブルの管理 > エディタからコピーを設定します|[テーブルの管理：エディタ：コピーを許可](../../managers-guide/manage-table/editor/allow-copy/index.md)|
|メール|編集|テーブルの管理 > サイトのアクセス制御で設定します|[サイト機能：アクセス制御](../../managers-guide/manage-table/site-access-control/index.md)|
|削除|編集|テーブルの管理 > サイトのアクセス制御で設定します|[サイト機能：アクセス制御](../../managers-guide/manage-table/site-access-control/index.md)|
|プロセスで追加したボタン|編集|テーブルの管理 > プロセスで設定します|[テーブルの管理：プロセス](../../managers-guide/manage-table/process/index.md)|

上記以外の方法として、サーバスクリプトの[elements.DisplayType](../../developers-guide/server-script/elements/server-script-elements-display-type.md)で設定することも可能です。
