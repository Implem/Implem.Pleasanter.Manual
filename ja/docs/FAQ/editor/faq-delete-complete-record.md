---
title: 状況が完了になった自レコードを自動で削除したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-delete-complete-record
translationKey: faq-delete-complete-record
shortname: サンプルコード
created: 2020-10-23
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)で実現可能です。

---

## 概要

更新ボタンを押した後に状況項目が"完了"になっていた場合、自レコードを削除するサンプルです。

## 操作手順

1. 期限付きテーブルまたは記録テーブルを作成してください  
1. [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載してください。出力先には「編集」をチェックして更新します。  
1.  [新規作成]ボタンから新たにレコードを作成してください。  
1. 3で作成したレコードの変更画面を開き、[状況項目]を”完了”に設定し、[更新]ボタンを押下してください。

## サンプルコード

##### JavaScript

```
//「更新」ボタンを押した後の処理
$p.events.after_set_Update = function () {
    $p.ex.DeleteMySelfData();
}
$p.ex.DeleteMySelfData = function() {
    //状況が「完了」となっているときに自分自身の削除を実行します。
    if ($p.getControl('Status').val() == 900) {
        $p.apiDelete({
            'id': $p.id(),
            'done': function () {
                $p.clearMessage();
                $p.setMessage('#Message', JSON.stringify({
                    Css: 'alert-success',
                    Text: 'ステータスが[完了]となったので自レコードを削除しました'
                }));
            },
            'fail': function () {
                console.log('自レコードの削除に失敗しました');
            }
        });
    }
}
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
