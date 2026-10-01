---
title: context.Forms
icon: material/alpha-p-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-forms
translationKey: server-script-context-forms
shortname: context.Forms
created: 2021-06-07
updated: 2026-08-05
---

## 概要

[サーバスクリプト](../index.md)でユーザが送信したフォームの情報を取得します。

## プロパティ

| No  | Name | Get | Set | Type          | Description                      |
| :-- | :--- | :-- | :-- | :------------ | :------------------------------- |
| 1   | Keys | ○   | -   | KeyCollection | フォームの要素のIDのコレクション |

## メソッド

| No  | Name      | Description                      |
| :-- | :-------- | :------------------------------- |
| 1   | Item.get  | フォームの要素の値を取得する     |
| 2   | ControlId | 送信元コントロールのIDを取得する |

## 使用例

下記の例では、ユーザが送信したフォームの要素のIDを列挙してIDと値をログに出力します。

``` javascript
for (let key of context.Forms.Keys){
    context.Log(key + ': ' + context.Forms.Item.get(key));
}
```

下記の例では、ユーザがフォーム送信時に使用した要素のIDをログに出力します。

``` javascript
context.Log(context.Forms.ControlId());
```

## サンプルコード

??? note "1.選択レコードの金額合計を表示する"

    一覧画面で複数のレコードを選択し、追加したボタン（選択行の金額合計）を押下すると、選択したレコードの金額（数値項目）の合計を画面下部にメッセージとして表示します。

    ### 実務での使いどころ

    発注や請求の確定作業で、まとめて処理する前に概算金額をその場で確認したい場面に使えます。見積や請求のレコードを一覧からいくつか選び、確定ボタンを押す前にこのボタンを押すだけで合計金額が表示されるため、想定外の金額のまま処理を進めてしまう事故を防げます。経理担当者が月末に対象レコードをまとめて選び、金額感を確認してから一括処理に進む、といった使い方を想定しています。

    ### 事前準備

    1.  一覧画面のツールバーに「選択行の金額合計」ボタンを追加します。

        1. 「テーブルの管理 > スクリプト」タブで「新規作成」を選択する。
        2. タイトル: 任意の名前（例：選択行の金額合計ボタン設置）
        3. スクリプト: 下記サンプル「1:ボタンの作成」を貼り付け
        4. 出力先:「全て」のチェックを外し、「一覧」にチェック

    2.  合計を計算して表示する処理を追加します。

        1. 「テーブルの管理 > サーバスクリプト」タブで「新規作成」を選択する。
        2. タイトル: 任意の名前（例：選択行の金額合計）
        3. スクリプト: 下記サンプル「2:計算コード」を貼り付け
        4. 条件:「画面表示前」にチェック

    3.  テーブルに数値項目を1つ用意してください。

        ※本サンプルでは数値項目1＝金額として使用

    ### 処理

    #### 1. ボタンの作成

    スクリプトに配置する。

    ##### JavaScript

    ``` javascript linenums="1"
    const BUTTON_LABEL = '選択行の金額合計';

    $p.events.on_grid_load = function () {
        $('#MainCommands').append(
            $('<button id="button-sum-selected" class="button button-icon button-positive ui-button ui-corner-all ui-widget applied" data-action="GridRows" data-method="post" onclick="$p.send($(this));">')
                .html('<span class="ui-icon ui-icon-calculator"></span>' + BUTTON_LABEL)
        );
    };
    ```

    #### 2. 計算コード

    サーバースクリプトに配置し、「画面表示前」にチェックする。  
    ボタン押下時のみ、選択したレコードの金額合計を計算して画面下部に表示します。

    ##### JavaScript

    ``` javascript linenums="1"
    (function () {
        try {
            // 「選択行の金額合計」ボタン押下時のみ実行する
            if (context.ControlId !== 'button-sum-selected') {
                return;
            }

            // ボタン設置スクリプトが送信するフォーム項目 GridCheckedItems（カンマ区切りのID文字列）から
            // 選択中のレコードIDを取得する
            let raw;
            try {
                raw = context.Forms.Item.get('GridCheckedItems');
            } catch (e) {
                // キー自体が存在しない場合（未選択状態）はここに来る
                raw = null;
            }

            const selectedIds = raw
                ? raw.split(',').map(function (s) { return parseInt(s, 10); }).filter(function (n) { return !isNaN(n); })
                : [];

            // 0件選択、または取得に失敗した場合はエラーにせずメッセージ表示のみで終了する
            if (!Array.isArray(selectedIds) || selectedIds.length === 0) {
                context.AddMessage('レコードが選択されていません。1件以上選択してから押してください。', 'alert-warning');
                return;
            }

            // 選択したレコードIDの配列を、items.Get に渡すフィルタ条件（JSON文字列）に変換する
            const idFilter = JSON.stringify(selectedIds.map(function (id) { return String(id); }));
            const data = {
                View: {
                    ColumnFilterHash: {
                        ResultId: idFilter
                    }
                }
            };

            // サイトIDと上記フィルタを指定し、選択したレコードだけをまとめて1回のAPI呼び出しで取得する
            const results = items.Get(context.SiteId, JSON.stringify(data));

            // 取得したレコードの数値項目1（金額）を1件ずつ加算していく
            let sum = 0;
            for (const item of results) {
                if (item && typeof item.NumA === 'number') {
                    sum += item.NumA;
                }
            }

            // 計算した合計金額を、画面下部にメッセージとして表示する
            context.AddMessage(`選択した ${selectedIds.length} 件の金額合計: ¥${sum.toLocaleString()}`, 'alert-information');
        } catch (e) {
            // 想定外のエラーはログに記録し、画面には汎用メッセージのみ表示する
            context.Log(e.stack);
            context.AddMessage('処理中にエラーが発生しました。詳細はシステムログをご確認ください。', 'alert-error');
        }
    })();
    ```

    ##### 選択テーブル

    ``` text
    案件A_予算　　　100,000
    案件A_追加予算　100,000
    案件A_経費　　　-50,000
    ```

    ##### 実行結果

    ``` text
    選択した 3 件の金額合計: ¥150,000
    ```

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.1.28.0 以降  | 機能追加 |

## 関連情報

- [開発者ガイド：サーバスクリプト](../index.md)
