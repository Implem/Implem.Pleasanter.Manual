---
title: context.Log
icon: material/alpha-m-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context-log
translationKey: server-script-context-log
shortname: context.Log
created: 2021-04-20
updated: 2026-08-05
---

## 概要

[サーバスクリプト](../index.md)のログをブラウザのコンソールに出力します。サーバ側で出力したログをクライアントに送出し、クライアント側のスクリプトでブラウザのコンソールに出力します。

## 構文

``` javascript
context.Log(message);
```

## パラメータ

|パラメータ|型|必須|概要|
|:----------|:----------|:---:|:---------------------------|
|message|object|○|エラーメッセージ|

## 戻り値

戻り値はありません。

## 使用例

下記の例では、組織ID 3のユーザが[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を完了にしようとした際に、ログを出力します。また、`try catch`によりエラーを検出した場合にも、エラー情報をログに出力します。

``` javascript linenums="1"
try {
    if (context.DeptId === 3 && model.Status === 900) {
        context.Log('条件に該当しました。');
    }
} catch (e) {
    context.Log(e.stack);
}
```

## サンプルスクリプト

??? note "1. 指定したサイトグループ名で支店ごとの未着手の件数を一覧表示する"

    サイトグループ名が一致する全サイトを一括取得し、支店ごとの「未着手」の件数を集計します。

    ### 実務での使いどころ

    複数拠点・複数案件のように同じ構成のサイトが増えていく運用で、リンク設定やサイトIDの管理をせずに集計対象を束ねられます。新しい支店サイトを追加した場合も、サイトグループ名を設定するだけで自動的に集計対象へ加わります。本部サイトから横断的に状況を集計したいダッシュボード的な用途に向いています。

    ### 前提条件

    あらかじめ、集計対象にしたい各サイトの「サイトの設定」→「その他」→「サイトグループ名」に、共通の値を設定しておく必要があります。同じグループ名を他の用途で使い回すと、意図しないサイトまで集計対象に含まれてしまうため、目的が分かる名前を付けてください（例：本部集計_サマリ用）。

    ##### JavaScript

    ``` javascript linenums="1"
    // 実行条件：一覧表示前
    const GROUP_NAME = '本部集計_サマリ用';
    const STATUS_UNPROCESSED = 100; // 未着手

    const sites = Array.from(items.GetSiteByGroupName(GROUP_NAME));

    if (!sites.length) {
        logs.LogUserError(`${GROUP_NAME} に該当するサイトが見つかりませんでした`, 'GroupSummary');
    } else {
        sites.forEach((site) => {
            const view = {
                View: {
                    ColumnFilterHash: {
                        Status: `["${STATUS_UNPROCESSED}"]`
                    }
                }
            };
            const records = items.Get(site.SiteId, JSON.stringify(view));
            context.Log(`${site.Title}(${site.SiteId})の未着手: ${records.Length}件`);
        });
    }
    ```

    ##### 実行結果

    ``` text
    東京支店(16491)の未着手: 11件
    大阪支店(16492)の未着手: 24件
    福岡支店(16493)の未着手: 8件
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
