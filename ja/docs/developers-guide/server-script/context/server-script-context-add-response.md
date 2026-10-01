---
title: context.AddResponse
icon: material/alpha-m-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-add-response
translationKey: server-script-context-add-response
shortname: AddResponse
created: 2023-04-04
updated: 2026-02-02
---

## 概要

[サーバスクリプト](../index.md)で任意のクライアントレスポンスを返却します。

## 制限事項

1. リンクしたアイテムの作成ボタンでの子レコードの作成後の画面遷移など、method「Href」を指定しても製品側仕様が優先する場合があります。

## 構文

``` javascript
context.AddResponse(method,target,value)
```

## パラメータ

|パラメータ|型|概要|
|:--|:--|:--|
|method|string|レスポンスの操作種別を指定します。下記のmethod部分を参照してください。|
|target|string|対象の要素のIDを指定します。|
|value|object|要素や値を指定します。|

### メソッド

|種別|説明|
|:--|:--|
|ReplaceAll|上記のtargetに指定した要素をvalueに指定した要素に置き換えます。|
|Set|フォームに情報を格納します。|
|Href|ポストバック後の遷移先URLを指定します。|

## 戻り値

戻り値はありません。

## 使用例①

以下の例では、分類Cのフィールドを `<div style="color:red">Pleasanter</div>` で置き換えます。

``` javascript
context.AddResponse('ReplaceAll','#Results_ClassCField','<div class="field-normal" style="color:red">Pleasanter</div>');
```

## 使用例②

以下の例では、フォーム（`$p.data.MainForm`）に以下の情報を格納します。

格納する情報

|項目|値|
|:--|:--|
|数値A項目|123|

``` javascript
context.AddResponse('Set','NumA',123);
```

## 使用例③

以下の例では、作成後にサイトID1234のテーブルに遷移します。

``` javascript
context.AddResponse('Href','','/items/1234/index');
```

## サンプルコード

??? note "1. テーブル内に期限切れレコードが存在した場合、ガイド欄にアナウンスを表示する"

    ReplaceAllメソッドでガイド欄の文言を動的に置き換えるサンプルコードです。

    期限付きテーブルの一覧表示時に、期限切れのレコードを取得、1件でも期限切れレコードがあった場合、ガイド欄の内容を`ReplaceAll`メソッドで置き換えます。

    期限切れレコードが存在する場合、以下のようにガイド欄に文言とリンクが表示されます。

    ![ガイド欄に期限切れを知らせる文言とリンクが表示された状態](https://pleasanter.org/files/images/ja/developers-guide/server-script/context/assets/8c49761c86924e9d9cf2f7ebcf082538.png)

    !!! warning "注意事項"
        本サンプルはバージョン1.5.0.0以降に対応しています。

    ### CSS

    以下スタイルを設定することで、ガイド欄の文字色を赤にします。

    ```css linenums="1"
    .md-viewer * {
        color: red !important;
    }
    ```

    ### JavaScript

    条件：画面表示の前

    ```javascript linenums="1"
    // 一覧画面(index)のときだけ動作
    if (context.Action !== 'index') return;
    // 文字列をHTMLとして差し込むため、最低限のエスケープ
    const escapeHtml = (s) =>
        String(s ?? '').replace(
            /[&<>"']/g,
            (c) =>
                ({
                    '&': '&amp;',
                    '<': '&lt;',
                    '>': '&gt;',
                    '"': '&quot;',
                    "'": '&#39;',
                })[c],
        );
    // /items/<id>... の <id> 以降を落として /items/ で終わるURLを作る
    const getItemsBaseUrl = () => {
        const url = String(context.Url ?? '');
        const m = url.match(/^(.*?\/items\/)/);
        return m ? m[1] : '';
    };
    // 期限切れ(Overdue)のレコードを取得
    const getOverdueItems = () => {
        const param = {
            View: { Overdue: true, ColumnSorterHash: { IssueId: 'asc' } },
        };
        return Array.from(items.Get(context.SiteId, JSON.stringify(param)));
    };
    // main処理
    // 期限切れレコードを取得
    const overdueItems = getOverdueItems();
    // 期限切れレコードがなければ終了
    if (overdueItems.length === 0) return;
    // ベースURLを生成
    const baseUrl = getItemsBaseUrl();
    // 期限切れレコードのリンク一覧HTMLを生成
    const linksText = overdueItems
        .map((item) => {
            const id = item.IssueId;
            const title = escapeHtml(item.Title);
            return `- ### [${title}](${baseUrl}${id})`;
        })
        .join('\n');
    const guideText = `
    [md]
    # 期限切れのアイテムがあります。至急確認してください。
    ## 対象レコード
    ${linksText}
    `;
    // ガイドエリア用のHTMLを生成
    const html = `
    <div id="Guide">
        <div>
            <markdown-field class="is-disabled">
                <textarea class="md-text" id="guide-textarea" data-readonly="1">${guideText}</textarea>
            </markdown-field>
        </div>
    </div>
    `;
    // ガイドエリア(#Guide)を差し替え
    context.AddResponse('ReplaceAll', '#Guide', html);
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
