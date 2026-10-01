---
title: 「レコードの遷移にAjaxを使用」をオンにしたり「ダイアログ編集」を選択したりしたらスクリプトが実行しなくなった
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-ajax-and-dialog-editor
translationKey: faq-ajax-and-dialog-editor
shortname: ''
created: 2019-02-04
updated: 2024-04-29
---

## 回答

[$p.events.on_editor_load](../../developers-guide/script/events/script-events-on-editor-load.md)を使用してください。

---

## 概要

以下の対象項目のチェックをオンにしたり選択したりした場合、HTMLの読み込み後に一度だけ実行されるスクリプト（以下、スクリプトと記載）が実行されなくなる場合があります。

| 対象項目                                                             | 事象例                                                                                                           |
| :------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
| [レコードの遷移にAjaxを使用](../../managers-guide/manage-table/editor/switch-record-with-ajax/index.md) [^1] | 対象項目を有効化し、編集画面にて「＜前」または「＞次」ボタンでレコードを遷移した場合、スクリプトが実行されない。 |
| [ダイアログ編集](../../managers-guide/manage-table/grid/table-management-grid-editor-type.md) [^2]          | 対象項目を選択し、一覧画面にてレコードを選択した場合、スクリプトが実行されない。                                 |

[^1]: 「テーブルの管理」画面→「エディタ」タブ
[^2]: 「テーブルの管理」画面→「一覧」タブ→「一覧編集種別」ドロップダウンリスト

プリザンターでは編集画面の表示方法が2種類あります。上記ケースでは、下記のNo. 2の方法で編集画面が表示される仕様となっており、Ajaxを使用しているためスクリプトが実行されません。

| No. | 表示方法                                                                         |
| :-- | :------------------------------------------------------------------------------- |
| 1   | ユーザ操作によりURLをリクエストし、HTMLを読み込むことで編集画面を表示            |
| 2   | ユーザ操作によりJavaScriptを使用し、Ajaxにより一部のHTMLを更新して編集画面を表示 |

上記事象は、[$p.events.on_editor_load](../../developers-guide/script/events/script-events-on-editor-load.md)イベントハンドラに処理を記述することで回避できます。
