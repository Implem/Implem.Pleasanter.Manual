---
title: 編集画面を登録・更新する際に誕生日から年齢を自動計算したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-automatically-calculate-age
translationKey: faq-automatically-calculate-age
shortname: サンプルコード
created: 2021-03-18
updated: 2024-04-29
---

## 回答

[サーバスクリプト](../../developers-guide/server-script/index.md)で実現できます。

---

## 概要

日付項目へ誕生日を入力しておき、データの登録・更新時点の年齢を計算します。

以下は、「日付A」項目に入力された誕生日をもとに計算した年齢を「数値A」項目へ入力するサンプルです。

## 操作方法

1.  「記録テーブル」を作成してください。
1.  「[テーブルの管理](../../managers-guide/manage-table/index.md)」画面の「[エディタ](../../managers-guide/manage-table/editor/index.md)」タブを開き、「日付A」と「数値A」を有効化してください。
1.  以下の[サーバスクリプト](../../developers-guide/server-script/index.md)を「新規作成」してください。  
    [条件](../../developers-guide/server-script/basics/server-script-conditions.md)は「計算式の後」を選択してください。

    ``` js title="「条件」は「計算式の後」" linenums="1"
    function ConvertDateToNum(date) {
        return date.getFullYear() * 10000
            + (date.getMonth() + 1) * 100
            + date.getDate();
    }

    function CalculateAge(birthdayVal) {
        const today = ConvertDateToNum(new Date());
        const birth = ConvertDateToNum(new Date(birthdayVal));
        return Math.floor((today - birth) / 10000);
    }

    model.NumA = utilities.InRange(model.DateA)
        ? CalculateAge(model.DateA)
        : 0;
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../../developers-guide/server-script/index.md)
-   [開発者ガイド：サーバスクリプト：条件](../../developers-guide/server-script/basics/server-script-conditions.md)
