---
title: context.Error
icon: material/alpha-m-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-error
translationKey: server-script-context-error
shortname: context.Error
created: 2021-04-20
updated: 2023-06-21
---

## 概要

[サーバスクリプト](../index.md)で「レコード」の作成前、更新前、削除前にエラー判定した場合に、処理をキャンセルしエラーメッセージを画面に表示します。サーバスクリプトは途中で停止いたしません。

## 制限事項

1. `context.Error`を設定した場合、サーバスクリプトの処理自体は行われますが、クライアントへ返却されるのはエラーメッセージのみとなります。そのため、`context.Error`に続く処理はサーバ上で行われますが、クライアント上のフォームには反映されません。
2. サーバスクリプトの[条件](../../../FAQ/editor/faq-condition-mode-range.md)が「作成前」、「更新前」、「削除前」の場合に有効となります。

## 構文

``` javascript
context.Error(message);
```

## パラメータ

| パラメータ | 型     | 必須 | 概要             |
| :--------- | :----- | :--: | :--------------- |
| message    | string |  ○   | エラーメッセージ |

## 戻り値

戻り値はありません。

## 使用例

下記の例では、組織ID 3 のユーザが[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を完了にして更新しようとした際に、その操作をキャンセルし、エラーメッセージを表示します。条件は「更新前」にチェックします。

##### JavaScript

``` javascript linenums="1"
try {
    if (context.DeptId === 3 && model.Status === 900) {
        context.Error('条件に該当したため、更新をキャンセルしました。');
    }
} catch (e) {
    context.Log(e.stack);
}
```

## 関連情報

- [開発者ガイド：サーバスクリプト](../index.md)
- [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
- [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
