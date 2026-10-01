---
title: コメントの削除を禁止したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-disable-comment-deletion
translationKey: faq-disable-comment-deletion
shortname: ''
created: 2026-01-13
updated: 2026-01-19
---

## 回答

コメントの削除ボタンをスタイルまたはスクリプトで非表示にしてください。

---

## 概要

コメントの削除ボタンは[スタイル](../../developers-guide/style/index.md)で非表示にすることができます。[スタイル](../../developers-guide/style/index.md)で非表示にする場合はすべてのユーザが対象となります。

##### スタイル：コメントの削除ボタンを非表示にする（出力先：編集）

```css
comment>.button.delete {
    display: none;
}
```

### 応用：特定ユーザ以外はコメント削除を禁止

[スクリプト](../../managers-guide/manage-table/scripts/index.md)を使うと、よりきめ細かな制御を実現できます。以下のスクリプトで特定のユーザ以外はコメント削除を禁止することができます。

##### スクリプト：特定のユーザ以外はコメント削除を禁止（出力先：編集）

```js
$p.events.on_editor_load = function () {
    // コメント削除を許可するユーザID
    const allowedUserId = 1;
    // ログインユーザのIDを取得
    let loginUserId = $p.userId();
    // ユーザIDが許可されたIDでない場合、削除ボタンを非表示にする
    if (loginUserId !== allowedUserId) {
        let deleteButtons = document.querySelectorAll('.button.delete');
        deleteButtons.forEach(function(button) {
            button.style.display = 'none';
        });
    }
};
```

## 関連項目

-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
