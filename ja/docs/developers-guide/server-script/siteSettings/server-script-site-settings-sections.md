---
title: siteSettings.Sections
category: サーバスクリプト
order: '3005'
status: ''
parts: ''
urlstring: server-script-site-settings-sections
translationKey: server-script-site-settings-sections
shortname: siteSettings.Sections
created: 2021-02-04
updated: 2026-01-26
---

## 概要 

[siteSettingsオブジェクト](index.md)のSectionsオブジェクトです。[サーバスクリプト](../index.md)で「セクション」の設定を変更するメソッドです。

## プロパティ

|No|プロパティ名|型|変更|説明|
|:--|:----------|:--|:---:|:---------------------------|
|1|Id|int|×|対象セクションのID|
|2|LabelText|string|〇|対象セクションのラベル名|
|3|AllowExpand|bool|〇|セクションの折りたたみを許可を指定|
|4|Expand|bool|〇|既定の表示を指定|

## 使用例①

以下の例では、1つ目のセクションのIDをNumAに設定します。

##### JavaScript

``` javascript
model.NumA = siteSettings.Sections[0].Id;
```

## 使用例②

以下の例では、2つ目のセクションのLabelText（入力項目）を設定します。

##### JavaScript

``` javascript
siteSettings.Sections[1].LabelText = '入力項目';
```

## 使用例③

以下の例では、1つ目のセクションのAllowExpand（許可）を設定します。

##### JavaScript

``` javascript
siteSettings.Sections[0].AllowExpand = true;
```

## 使用例④

以下の例では、2つ目のセクションの既定の表示（閉じる）を設定します。

##### JavaScript

``` javascript
siteSettings.Sections[1].Expand = false;
```

## サンプルコード

??? note "1. ステータスに応じてセクションの開閉を制御する"

    ステータスに応じてセクションの開閉を制御します。

    なお、本サンプルコードを動作させるため、見出し項目の設定にて、「セクションの折りたたみを許可」にチェック、既定の表示を「閉じる」に設定してください。

    ##### JavaScript

    条件：画面表示の前

    ``` javascript linenums="1"
    const rules = {
        150: 0,
        200: 1,
        300: 2,
        900: 3,
    };
    const sectionIndex = rules[model.Status];
    if (sectionIndex !== undefined) {
        siteSettings.Sections[sectionIndex].Expand = true;
    }
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
