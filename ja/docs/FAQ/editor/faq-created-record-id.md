---
title: 作成したレコードのIDを取得したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-created-record-id
translationKey: faq-created-record-id
shortname: サンプルコード
created: 2020-12-25
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を利用してください。

---

## 概要

親テーブルにレコードを新規作成したと同時にリンクしたレコードを子テーブルに新規作成したい場合などで、新規作成したレコードのIDを取得したい場合は[スクリプト](../../managers-guide/manage-table/scripts/index.md)の実装が必要です。
顧客テーブル（親）でレコードを作成したタイミングで、作成したレコードとリンクしたレコードをチェックリストテーブル（子）に作成するサンプルになります。  

## 事前準備

本FAQでは以下のような親子関係のテーブルをもとに進めます。  
![顧客テーブル（親）とチェックリストテーブル（子）の親子関係を示す図](https://pleasanter.org/files/images/ja/FAQ/editor/assets/b9c694ba5d2d4f6eb3e2f109d22f0082.png)  
チェックリストテーブル（子）でリンクに使用する項目は分類A（ClassA）になります。 リンクの設定方法については以下ページを参照ください。  
[テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：リンク \| Pleasanter](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-link.md)

## 操作手順

1. 下記スクリプトを顧客テーブル（親）のテーブルの管理にあるスクリプトに登録します。実行タイミングは「新規作成」です。
1. 顧客テーブルでレコードを新規作成します。
1. チェックリストテーブルに移動します。
1. 2.で作成したレコードにリンクしているレコードが作成されていることを確認します。

## サンプルコード

##### JavaScript

```
$p.events.before_set_Create = function (args) {
    console.log(args.json);
    craeteCheckListRecored(args.json[0].Value);
}
function craeteCheckListRecored(recordId) {
    $p.apiCreate({
        id: 242196,
        data: {
            Offset: 0,
            Title: '顧客テーブルでレコードを作成したタイミングで、このレコードは作成されました。',
            ClassA: recordId
        },
        done: (data) => {
            console.log('Success!');
            console.log(data);
        },
        fail: (data) => {
            console.log(data);
        }
    })
}
```

### 補足説明

上記スクリプトでレコードを作成したタイミングでレコードIDを取得する部分は下記の部分になります。

##### JavaScript

```
$p.events.before_set_Create = function (args) {
    console.log(args.json);
    craeteCheckListRecored(args.json[0].Value);
}
```  
「$p.events.before_set_Create」のイベントが実行されたタイミングのレスポンス（args）に作成したレコード情報が格納されております。  
「args.json[0].Value」でレコードIDを確認することができます。

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：リンク \| Pleasanter](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-link.md)