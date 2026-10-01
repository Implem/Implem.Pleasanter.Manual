---
title: 更新ボタンを押したタイミングで別テーブルに新規レコードを作成したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-create-new-record-after-updating
translationKey: faq-create-new-record-after-updating
shortname: サンプルコード
created: 2020-10-22
updated: 2024-07-12
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使用してください。

---

## 概要

レコードの更新後に別のテーブルにレコードを新規作成したい場合は、[スクリプト](../../managers-guide/manage-table/scripts/index.md)で実装します。

## 操作手順

1. 期限付きテーブルまたは記録テーブルを作成してください。  
1. [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載し、idの値を新規レコードを作成したいサイトのIDに設定してください。出力先には「編集」をチェックして更新します。  
1.  [+新規作成]ボタンから新たにレコードを作成してください。  
1.  3で作成したレコードの変更画面を開き、[更新]ボタンを押下してください。

### 実行結果

  記録テーブルAにあるレコードを更新すると、記録テーブルBにレコードが新規作成されます。

#### 更新前

![更新前の状態を示す画面](https://pleasanter.org/files/images/ja/FAQ/editor/assets/436a12295e6b4737a3ad8c198c96e6cc.png)

#### 記録テーブルAのレコードを更新

![記録テーブルAのレコードを更新しているところ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/f285dde68713429fa5ba3d0d6a8e6dff.png)

#### 更新後

![更新後の状態。記録テーブルBにレコードが新規作成されている](https://pleasanter.org/files/images/ja/FAQ/editor/assets/c52b3968210041a1b53bffc44ea4587c.png)

## サンプルコード

##### JavaScript

```
//「更新」ボタンを押した後の処理
$p.events.after_send_Update = function () {
    getParentData();
}

function getParentData() {
    //タイトル項目が「タイトルテスト」というレコードを作成します。
    $p.apiCreate({
        'id': 9999,
        'data': {
            'Offset': 0,
            'Title': 'FAQ:サンプルコード：更新ボタンを押した後に新たに別レコードを作成'
        },
        'done': function (data) {
            $p.clearMessage();
            $p.setMessage(
                '#Message', JSON.stringify({
                    'Css': 'alert-success',
                    'Text': '新規レコードを作成しました'
                 }));
        },
        'fail': function (data) {
            console.log(data);
        }
    });
}
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
