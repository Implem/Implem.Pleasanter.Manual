---
title: elements.DisplayType
icon: material/alpha-m-box
category: サーバスクリプト
order: '6410'
status: ''
parts: ''
urlstring: server-script-elements-display-type
translationKey: server-script-elements-display-type
shortname: elements.DisplayType
created: 2021-10-11
updated: 2026-07-08
---

## 概要

[サーバスクリプト](../index.md)で「ナビゲーションメニュー」、「コマンドボタン」、[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)で追加したボタンの表示状態を制御します。

## 制限事項

1. 画面上部の「ナビゲーションメニュー」、画面下部の「コマンドボタン」、[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)で追加したボタンに適用可能です。
1. 戻るボタンには適用できません。
1. ナビゲーションメニューに「2:無効」を設定することはできません。
1. サーバスクリプトの[条件](../../../FAQ/editor/faq-condition-mode-range.md)が「画面表示の前」の場合に有効となります。

## 構文

```
elements.DisplayType(id, displayType);
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|id|string|○|HTMLのID属性|
|displayType|int|○|0:標準/1:無し/2:無効/3:非表示|

## 戻り値

戻り値はありません。

## 使用例①

以下の例ではdisplayTypeに1を指定することで、ヘルプメニューのHTMLが出力されません。

##### JavaScript

```
elements.DisplayType('HelpMenuContainer',1);
```

## 使用例②

以下の例ではdisplayTypeに2を指定することで、削除ボタンが無効化されます。

##### JavaScript

```
elements.DisplayType('DeleteCommand',2);
```

## 使用例③

以下の例ではdisplayTypeに3を指定することで、[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)で追加したボタン(ID:1)が非表示となります。

##### JavaScript

```
elements.DisplayType('Process_1',3);
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)