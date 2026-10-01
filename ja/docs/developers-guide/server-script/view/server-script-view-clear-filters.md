---
title: view.ClearFilters
icon: material/alpha-m-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-clear-filters
translationKey: server-script-view-clear-filters
shortname: view.ClearFilters
created: 2022-07-19
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)で、設定されているフィルタ条件をクリアします。Web UIで設定されているフィルタを、サーバスクリプトで無効化する場合などに利用できます。

`view.ClearFilters()`の呼び出し時点で既に設定されていたフィルタ条件は削除されます。`view.ClearFilters()`の呼び出し後に新たにサーバスクリプトで設定された[view.Filters](server-script-view-filters.md)の内容は有効となります。

## 注意事項

1. 「ビュー処理時」の条件のみ使用できます。

## 構文

``` javascript
view.ClearFilters();
```

## パラメータ

パラメータはありません。

## 戻り値

戻り値はありません。

## 使用例

下記の例では、画面からのフィルタ操作をすべて無効化しその後[view.Filters](server-script-view-filters.md)に[内容項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)内に "ソフトウェア" の文字列を含むレコードを抽出する条件を追加しています。

##### JavaScript

``` javascript linenums="1"
view.ClearFilters(); // 画面からのフィルタ操作をすべて無効化
view.Filters.Body = 'ソフトウェア'; // Bodyに'ソフトウエア' 文字列が含まれるものを抽出。
```

## サンプルコード

??? note "1. ユーザロールごとにフィルタ条件を制御する"

    以下のようなフィルタ条件を制御します。

    |ロール|権限|
    |:--|:--|
    |特権ユーザ|すべてのレコードを参照可|
    |管理職|所属組織のレコードを参照可|
    |一般社員|自分担当のレコードのみ参照可|

    制御のため、以下のようにグループを用意し、ユーザを所属させます。

    |ロール|特権ユーザグループ|管理職グループ|
    |:--|:--:|:--:|
    |特権ユーザ|所属||
    |管理職||所属|
    |一般社員|||

    なお、本サンプルコードでは、**特権ユーザグループ：GroupId=5**、**管理職グループ：GroupId=4**として定義しています。

    また、所属組織の担当レコードであることを判別するため、ClassAに組織を選択できるように設定しておきます。

    その上で、以下のように制御します。

    -   管理職：自分の組織ID=ClassAを対象
    -   一般社員：自分のユーザID=Ownerを対象

    ##### JavaScript

    ```javascript linenums="1"
    // グループIDを定義
    const ADMIN_GROUP_ID = 5;
    const MANAGE_GROUP_ID = 4;
    // ユーザが特定のグループに所属しているか判定
    function isUserInGroup(userId, groupId) {
        const group = groups.Get(groupId);
        if (!group) return false;
        for (const member of group.GetMembers()) {
            if (member.UserId === userId) return true;
        }
        return false;
    }
    // フィルタ適用ルールを定義
    const rules = [
        {
            name: '特権ユーザグループ',
            when: () => isUserInGroup(context.UserId, ADMIN_GROUP_ID),
            apply: () => view.ClearFilters(),
        },
        {
            name: '管理職グループ',
            when: () => isUserInGroup(context.UserId, MANAGE_GROUP_ID),
            apply: () => {
                const user = users.Get(context.UserId);
                view.Filters.ClassA = `["${user.DeptId}"]`;
            },
        },
        {
            name: '一般社員',
            when: () => true,
            apply: () => {
                view.Filters.Owner = `["${context.UserId}"]`;
            },
        },
    ];
    // ルールを順番に評価し、最初に該当したルールを適用
    for (const rule of rules) {
        if (rule.when()) {
            logs.LogInfo(rule.name);
            rule.apply();
            break;
        }
    }
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.13.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：view.Filters](server-script-view-filters.md)
-   [テーブルの管理：項目：内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
