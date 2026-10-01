---
title: リンクの経路が異なる同一サイトを含める
category: 一覧画面
order: '290'
status: ''
parts: ''
urlstring: table-management-enable-expand-link-path
translationKey: table-management-enable-expand-link-path
shortname: ''
created: 2025-01-14
updated: 2025-01-14
---

## 概要

「リンクの経路が異なる同一サイトを含める」をオンにすると、一覧項目の選択肢にリンクの経路が異なる同一サイトを含めることができます。

## 注意事項

1. この設定をオンにしたテーブルでは、設定しているリンクの構成によっては画面表示時のレスポンスが悪化する場合があります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。
1. この機能を利用するには、あらかじめ[General.json](../../../setup/parameters/general.json.md)のEnableExpandLinkPathをtrueに設定しておく必要があります。

## 操作手順

1. 対象の[テーブル](../../../users-guide/table/index.md)を開いてください。
1. 「管理」メニューから[テーブルの管理](../index.md)をクリックしてください。
1. [一覧](index.md)タブを開いてください。
1. 画面下部にある「リンクの経路が異なる同一サイトを含める」のチェックボックスをオンにします。
1. 画面下部の「更新」ボタンをクリックしてください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [パラメータ設定：General.json](../../../setup/parameters/general.json.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [テーブルの管理](../index.md)
-   [テーブルの管理：一覧画面](index.md)