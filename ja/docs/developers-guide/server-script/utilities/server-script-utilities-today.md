---
title: utilities.Today
icon: material/alpha-m-box
category: サーバスクリプト
order: '6510'
status: ''
parts: ''
urlstring: server-script-utilities-today
translationKey: server-script-utilities-today
shortname: utilities.Today
created: 2021-08-20
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)でローカル時間における当日の0時の日時をUTCで返します。

## 構文

```
utilities.Today()
```

## パラメータ

パラメータはありません。

## 戻り値

ローカル時間における当日の0時の日時をUTCで返却します。日本時間2023年6月21日に実行した場合、「2023/06/20 15:00:00」が返却されます。

## 使用例

以下の例では、日付Aに当日の日時を入力します。サーバスクリプト内ではUTCの日時として扱われますが、サーバスクリプト終了後、日付Aにはローカル時刻に変換された日時が格納されます。

##### JavaScript

```
model.DateA = utilities.Today();
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

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.39.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：スクリプト](../../../managers-guide/manage-table/scripts/index.md)