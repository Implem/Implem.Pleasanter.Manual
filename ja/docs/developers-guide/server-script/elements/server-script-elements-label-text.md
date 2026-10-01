---
title: elements.LabelText
icon: material/alpha-m-box
category: サーバスクリプト
order: '6410'
status: ''
parts: ''
urlstring: server-script-elements-label-text
translationKey: server-script-elements-label-text
shortname: elements.LabelText
created: 2023-03-30
updated: 2023-06-21
---

## 概要

[サーバスクリプト](../index.md)でボタンやメニューの表示名を変更します。

## 制限事項

1. 画面上部の「ナビゲーションメニュー」、画面下部の「コマンドボタン」、[プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)で追加したボタンの表示名を変更可能です。
1. 戻るボタンには適用できません。

## 構文

```
elements.LabelText(key, labelText)
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|key|string|○|HTMLのID属性|
|labelText|string|○|文字列|

## 戻り値

戻り値はありません。

## 使用例

以下の例では、更新ボタンの表示名を「アップデート」に変更します。

##### JavaScript

```
elements.LabelText('UpdateCommand','アップデート');
```

## サンプルコード

??? note "1. プロセスのボタンのラベルを今日の日付で設定する。"

    プロセスで設定したボタンのラベルを、"{今日の日付}のデータの取得"とします。

    ##### JavaScript
    ```javascript
    const dateFormat = (input) => {
        if (!input) return '';
        // 返却値は文字列であるため、new Date()する
        const date = new Date(input);
        const y = date.getFullYear();
        const m = String(date.getMonth() + 1).padStart(1, '0');
        const d = String(date.getDate()).padStart(1, '0');
        const dateTime = `${y}年${m}月${d}日`;
        return dateTime;
    };
    elements.LabelText('Process_1', `${dateFormat(utilities.Today())}のデータ取得`);
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [プリザンターの直近のアップデート情報](../../../update-info/index.md)