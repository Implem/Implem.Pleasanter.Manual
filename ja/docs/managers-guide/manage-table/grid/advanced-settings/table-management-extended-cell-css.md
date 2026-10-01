---
title: セルCSS
category: 一覧画面
order: '30'
status: ''
parts: ''
urlstring: table-management-extended-cell-css
translationKey: table-management-extended-cell-css
shortname: セルCSS
created: 2021-05-06
updated: 2025-10-24
---

## 概要

[セルCSS](../../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)により[一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)上の[項目](../../editor/editor-settings/columns/index.md)の「th要素」、「td要素」に出力する「CSSクラス名」を設定します。[スタイル](../../../../developers-guide/style/index.md)と組み合わせて「セルの背景」や「文字」に色をつける場合などに使用できます。

## 制限事項

1. 「ログインユーザ」や「レコードの内容」によって「CSSクラス名」を変更することはできません。動的な制御が必要となる場合には[サーバスクリプト](../../../../developers-guide/server-script/index.md)の「columnsオブジェクト」の「ExtendedCellCss」を使用してください。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 操作方法

1. [一覧画面の項目の詳細設定](index.md)を参照してください。

## 関連情報

-   [FAQ：一覧画面で数値の範囲によってセルの色を変えたい](../../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)
-   [テーブル機能：レコードの一覧画面](../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理：項目](../../editor/editor-settings/columns/index.md)
-   [開発者ガイド：スタイル](../../../../developers-guide/style/index.md)
-   [開発者ガイド：サーバスクリプト](../../../../developers-guide/server-script/index.md)
-   [テーブルの管理：一覧画面：項目の詳細設定](index.md)