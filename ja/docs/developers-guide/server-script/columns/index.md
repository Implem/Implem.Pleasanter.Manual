---
title: columns
icon: material/alpha-o-box
category: サーバスクリプト
order: '6000'
status: ''
parts: ''
urlstring: server-script-columns
translationKey: server-script-columns
shortname: columns
created: 2021-01-22
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)で[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の設定を取得、編集します。 [一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の[セルCSS](../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)の設定や[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)の[フィールドCSS](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)、[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)の設定などが可能です。

## プロパティ

|No|Name|Get|Set|Type|Description|
|:----|:----|:----|:----|:----|:----|
|1|ExtendedCellCss|○|○|string|[セルCSS](../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)|
|2|ExtendedFieldCss|○|○|string|[フィールドCSS](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)|
|3|ExtendedControlCss|○|○|string|[コントロールCSS](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)|
|4|ExtendedHtmlBeforeField|○|○|string|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)のフィールドの前|
|5|ExtendedHtmlBeforeLabel|○|○|string|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)のラベルの前|
|6|ExtendedHtmlBetweenLabelAndControl|○|○|string|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)のラベルとコントロールの間|
|7|ExtendedHtmlAfterControl|○|○|string|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)のコントロールの後|
|8|ExtendedHtmlAfterField|○|○|string|[拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)のフィールド後|
|9|Hide|○|○|bool|[非表示](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)、一覧画面では値が表示されない他、ExtendedCellCssおよびRawTextが無視されます。|
|10|ValidateRequired|○|○|bool|[入力必須](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)|
|11|RawText|○|○|string|一覧画面の項目の値を置換|
|12|ReadOnly|○|○|bool|[読取専用](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)|

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|[AddChoiceHash](server-script-columns-add-choice-hash.md)|[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)を動的に設定します。|
|2|[ClearChoiceHash](server-script-columns-clear-choice-hash.md)|[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)をクリアします。|

## 使用例

### 使用例1

以下の例では、ClassA（分類A）を非表示にします。

##### JavaScript（サーバスクリプト）

``` javascript
columns.ClassA.Hide = true;
```

### 使用例2

以下の例では、DescriptionA（説明A）を読取専用にします。

##### JavaScript（サーバスクリプト）

``` javascript
columns.DescriptionA.ReadOnly = true;
```

### 使用例3

以下の例では[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の分類Aのセルに赤字でABCと出力します。条件に行表示の前を指定する必要があります。HTMLのタグを挿入可能です。

##### JavaScript（サーバスクリプト）

``` javascript
columns.ClassA.RawText = '<font color="red">ABC</font>';
```

## サンプルコード

??? note "1. ログインユーザの属性と状況による画面項目制御"

    ログインユーザの属性（`context.HasPrivilege`、`context.Groups`で判定）と、状況により画面項目の制御（`columns.ReadOnly,Hide`で制御）を行います。サンプルコードでは以下のような仕様で実装しています。

    **制御パターン判定**

    | ユーザ種類 | 状況 | 制御パターン |
    |---|---|---|
    | 特権ユーザ | － | パターンA |
    | 管理者グループ所属ユーザ(ID1,2) | － | パターンB |
    | 上記以外のユーザ | 完了(900) or 保留(910) | パターンC |
    | 上記以外のユーザ | 以外 | パターンD |

    　

    **画面項目制御**

    | 画面項目 | 項目ID | パターンA | パターンB | パターンC | パターンD |
    |---|---|---|---|---|---|
    | タイトル | Title | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 内容 | Body | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 状況 | Status | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 分類A | ClassA | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 分類B | ClassB | 編集可 | 読取専用 | 非表示 | 非表示 |
    | 日付A | DateA | 編集可 | 読取専用 | 読取専用 | 編集可 |
    | 説明A | DescriptionA | 編集可 | 編集可 | 非表示 | 非表示 |

    ##### JavaScript

    条件：画面表示の前

    ```javascript linenums="1"
    // 設定
    const ADMIN_GROUP_IDS = new Set([1, 2]);
    const STATUS_PATTERN_C = new Set([900, 910]); // 完了/保留
    const PATTERN_RULES = {
        // パターンA: 何もしない（全編集可）
        A: [],
        // パターンB: ClassB, DateA を読取専用
        B: [
            ['ClassB', 'ReadOnly'],
            ['DateA', 'ReadOnly'],
        ],
        // パターンC: タイトル/内容/状況/分類A/日付Aは読取専用、ClassB/説明Aは非表示
        C: [
            ['Title', 'ReadOnly'],
            ['Body', 'ReadOnly'],
            ['Status', 'ReadOnly'],
            ['ClassA', 'ReadOnly'],
            ['DateA', 'ReadOnly'],
            ['ClassB', 'Hide'],
            ['DescriptionA', 'Hide'],
        ],
        // パターンD: ClassB, DescriptionA を非表示
        D: [
            ['ClassB', 'Hide'],
            ['DescriptionA', 'Hide'],
        ],
    };
    const DEBUG = true;
    // 判定（業務ルール）
    function decidePattern() {
        if (context.HasPrivilege) return 'A';
        // context.Groups は Iterable のため Set化して判定をシンプルに
        const userGroupIds = new Set(context.Groups);
        const isAdminGroupUser = [...ADMIN_GROUP_IDS].some((id) =>
            userGroupIds.has(id)
        );
        if (isAdminGroupUser) return 'B';
        // 上記以外のユーザ
        return STATUS_PATTERN_C.has(model.Status) ? 'D' : 'C';
    }
    // 適用（UI制御）
    function applyPattern(pattern) {
        const rules = PATTERN_RULES[pattern] ?? [];
        for (const [columnName, control] of rules) {
            // サンプルとして：列が存在しない場合も落とさずスキップ
            if (!columns[columnName]) continue;
            columns[columnName][control] = true;
        }
    }
    // 実行
    const pattern = decidePattern();
    if (DEBUG) context.Log(`pattern=${pattern}`);
    applyPattern(pattern);

    ```

    ##### 実行結果

    ```text
    (Info):pattern=C
    ```

??? note "2. 数値項目をスター記号で表示"

    数値項目に入力された数値に応じスター記号で表示します。

    以下のようなイメージで"4.5"といった値にも対応しています。

    ![数値項目をスター記号で表示した例](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/1bd8affc6f074cab8633279d217b3dad.png)

    本サンプルコードでは、最大5個までのスター表示に対応しています。

    ##### JavaScript

    条件：行表示の前

    ```javascript linenums="1"
    const maxStars = 5;
    function toStarHtml(score) {
        const s = Math.max(0, Math.min(maxStars, Number(score) || 0));
        const pct = (s / maxStars) * 100; // 0〜100%
        return `
            <span
                style="
                    display: inline-block;
                    position: relative;
                    line-height: 1;
                    font-size: 20px;
                    letter-spacing: -0.2em;
                "
            >
                <span style="color: #ccc">★★★★★</span>
                <span
                    style="position:absolute;
                    left:0;
                    top:0;
                    width:${pct}%;
                    overflow:hidden;
                    white-space:nowrap;
                    color:#f60;"
                >
                    ★★★★★
                </span>
            </span>
    `.trim();
    }
    columns.NumA.RawText = toStarHtml(model.NumA);
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.38.0 以降|ExtendedHtmlBeforeLabelの追加<br>ExtendedHtmlBetweenLabelAndControlの追加<br>ExtendedHtmlAfterFieldの追加|
|1.2.15.0 以降|ValidateRequiredの追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [FAQ：一覧画面で数値の範囲によってセルの色を変えたい](../../../FAQ/grid/faq-grid-cell-color-by-num-range.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フィールドCSS](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-field-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：拡張HTML](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：コントロールCSS](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-extended-control-css.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)
-   [開発者ガイド：サーバスクリプト：columns.AddChoiceHash](server-script-columns-add-choice-hash.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [開発者ガイド：サーバスクリプト：columns.ClearChoiceHash](server-script-columns-clear-choice-hash.md)
