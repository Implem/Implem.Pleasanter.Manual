---
title: view.Filters
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-filters
translationKey: server-script-view-filters
shortname: view.Filters
created: 2021-01-22
updated: 2026-03-05
---

## 概要

[view](index.md)オブジェクトの「Filters」です。[サーバスクリプト](../index.md)で[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)や[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)に表示する「レコード」を[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)することで、ユーザに閲覧させるレコードを制限することができます。[レコードのアクセス制御](../../../users-guide/access-control/table-record-access-control.md)と異なり「レコード」1件1件にアクセス権を設定する必要がありません。[JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)が使用できます。

## 制限事項

1. 「ビュー処理時」の条件のみ使用できます。
1. [添付ファイル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)、[コメント項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)は使用できません。
1. [サーバスクリプト](../index.md)により[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)を設定した項目は[一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)等の[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)操作が動作しません。[サーバスクリプト](../index.md)により上書きされます。
1.` view.Filter`をすると「フィルタボタンを使用する」を有効にしても一覧画等面表示時に`view.Filter`に指定した条件で抽出したレコードが表示されます。
1. `view.Filter`をすると[常に検索条件を要求する](../../../managers-guide/manage-table/grid/table-management-always-request-search-condition.md)を有効にしても一覧画等面表示時に`view.Filter`に指定した条件で抽出したレコードが表示されます。
1. SQL Serverを使用する場合とPostgreSQLを使用する場合では検索結果が異なる場合がございます。SQL Serverでは`LIKE`句またはフルテキスト検索が使用されるのに対し、PostgreSQLでは`ILIKE`句または`pg_trgm`によるフルテキスト検索が行われます。

## 注意事項

1. `view.Filters`の機能で、一覧画面でレコードを抽出されないようにフィルタした場合であっても、[横断検索](../../../users-guide/common/crosssearch.md)では検索結果リストに表示されます。これを防ぐにはテーブルの管理の設定[横断検索を無効化](../../../managers-guide/manage-table/search/table-management-disable-cross-search.md)で横断検索を無効化する必要があります。

## プロパティ

|No|プロパティ名|変更|説明|
|:--|:--|:--|:--|
|1|」`[カラム名]`|○|[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)をかける[カラム名](../../dev-column-name.md)を指定しフィルタ文字列を設定。|

## メソッド

メソッドはありません。

## 使用例

### 使用例1

下記の例では[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)が 900 (完了) または 910 (保留) のレコードを抽出して表示します。

```javascript
view.Filters.Status = '["900","910"]';
```

### 使用例2

下記の例では[担当者項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)にセットされた[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)のユーザIDが 215 と 319 のレコードを抽出して表示します。

```javascript
view.Filters.Owner = '["215","319"]';
```

### 使用例3

下記の例では[数値項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)にセットされた数値が 600000 ～ 700000 のレコードを抽出して表示します。カンマより前を省略すると 700000 以下、カンマより後を省略すると 600000 以上がセットされたレコードを抽出して表示します。複数の範囲を検索する場合は `'["100000,200000","600000,700000"]'` のように指定します。

```javascript
view.Filters.NumA = '["600000,700000"]'
```

### 使用例4

下記の例では[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)にセットされた日付が本日のレコードを抽出して表示します。`'["Today"]'`は本日、`'["ThisMonth"]'`は今月、`'["ThisYear"]'`は今年を抽出します。

```javascript
view.Filters.DateA = '["Today"]';
```

### 使用例5

下記の例では[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)にセットされた日付が 2021/5/1 00:00:00 ～ 2021/5/31 23:59:59.997 のレコードを抽出して表示します。カンマより前を省略すると 2021/5/31 23:59:59.997以前、カンマより後を省略すると 2021/5/1 00:00:00以降がセットされたレコードを抽出して表示します。複数の範囲を検索する場合は `'["2021/1/1,2021/1/31 23:59:59.997","2021/5/1,2021/5/31 23:59:59.997"]'` のように指定します。

```javascript
view.Filters.DateB = '["2021/5/1,2021/5/31 23:59:59.997"]'
```

### 使用例6

下記の例では[チェック項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)がオンになっているレコードを抽出して表示します。`false` を代入するとオフのレコードを抽出します。

```javascript
view.Filters.CheckA = true;
```

### 使用例7

下記の例では[内容項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)に ソフトウェア の文字を含むレコードを抽出して表示します。[テーブルの管理](../../../managers-guide/manage-table/index.md)の[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)で[検索の種類](../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)を設定すると「部分一致検索」だけでなく「前方一致検索」や「完全一致検索」も行えます。[タイトル項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)、「[説明項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)および選択肢の無い[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)でも同様の検索が行えます。

```javascript
view.Filters.Body = 'ソフトウェア';
```

### 使用例8

下記の例では[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)が 900 (完了) かつ[日付項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)にセットされた日付が本日のレコードを抽出して表示します。異なる項目を複数セットした場合には AND 条件で[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)されます。

```javascript linenums="1"
view.Filters.Status = '["900"]';
view.Filters.DateA = '["Today"]';
```

### 使用例9

下記の例では[状況項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)が 900 (完了) または[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の選択肢に 設計 がセットされたレコードを抽出して表示します。`or_`で始まる任意のプロパティにJSON形式のフィルタ条件を代入することで、OR条件による[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)を行うことができます。画面からの[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)操作は明示的に無効化する必要があります。

```javascript linenums="1"
// 画面からのフィルタ操作を無効化
view.Filters.ClassA = '';
view.Filters.Status = '';
// OR条件の設定
let data = {};
data.Status = '["900"]';
data.ClassA = '["設計"]';
view.Filters.or_MyFilterName = JSON.stringify(data);
```

### 使用例10

下記の例では組織IDが 3 のユーザがアクセスした場合[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の選択肢に 人事 がセットされたレコードを抽出して表示します。組織IDが 7 のユーザが使用した場合[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の選択肢に 開発 がセットされたレコードを抽出して表示します。それ以外の組織のユーザがアクセスした場合には全てのレコードを抽出して表示します。

```javascript linenums="1"
context.Log(context.DeptId);
switch (context.DeptId) {
    case 3:
        view.Filters.ClassA = '["人事"]'
        break;
    case 7:
        view.Filters.ClassA = '["開発"]'
        break;
    default:
        break;
}
```

### 使用例11

下記の例ではユーザIDが 2 以外のユーザがアクセスした場合 分類A が 設計 かつ 分類D が 3 のレコード、または  分類B が テスト かつ 分類D が 7 のレコードを抽出して表示します。ユーザIDが 2 のユーザがアクセスした場合には全てのレコードを抽出して表示します。`and_`で始まる任意のプロパティにJSON形式のフィルタ条件を代入することで、OR条件と条件をAND条件を組み合わせた[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)を行うことができます。

```javascript linenums="1"
if (context.UserId !== 2) {
    let data1 = {};
    data1.ClassA = '["設計"]';
    data1.ClassD = '["3"]';
    let data2 = {};
    data2.ClassA = '["テスト"]';
    data2.ClassD = '["7"]';
    let data = {};
    data.and_Filter1 = JSON.stringify(data1);
    data.and_Filter2 = JSON.stringify(data2);
    view.Filters.or_Filter = JSON.stringify(data);
}
```

### 使用例12

下記の例では 分類A でリンクした サイトID 6 のレコードの分類B に 東京都中野区 がセットされているレコードを抽出して表示します。下記の記述によりマスタレコードの項目でフィルタすることができます。

```javascript
view.Filters['ClassA~6,ClassB'] = '東京都中野区';
```

### 使用例13

下記の例では 分類A でリンクされた サイトID 7 の子レコードの 分類B に システム開発 がセットされているレコードを抽出して表示します。下記の記述により子レコードの項目でフィルタすることができます。子レコードに複数のレコードがヒットした場合、親レコードの同じレコードが複数表示されます。

```javascript
view.Filters['ClassA~~7,ClassB'] = '["システム開発"]';
```

### 使用例14

下記の例では 分類A の値と 分類B の値が一致しているレコードのみを抽出して表示します。`eq_`で始まる任意のプロパティに`{１つ目の項目}|{二つ目の項目}`の形式で比較する項目を指定することで、２つの項目の値が一致しているレコードのみをフィルタすることができます。[^1]

[^1]: ただし、２つの項目にはデータタイプの異なる項目は指定できません。各項目のデータタイプは [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)の一覧に記載されています。

```javascript
view.Filters.eq_MyFilterName = 'ClassA|ClassB';
```

### 使用例15

下記の例では 分類A の値と 分類B の値が一致していないレコードのみを抽出して表示します。`notEq_`で始まる任意のプロパティに`{１つ目の項目}|{二つ目の項目}`の形式で比較する項目を指定することで、２つの項目の値が一致しているレコードのみをフィルタすることができます。[^2]

[^2]: ただし、２つの項目にはデータタイプの異なる項目は指定できません。各項目のデータタイプは [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)の一覧に記載されています。

```javascript
view.Filters.notEq_MyFilterName = 'NumA|NumB';
```

`eq_`、`notEq_`で始まるプロパティは、`or_`や`and_`で始まるプロパティと組み合わせて使用することができます。また、リンクしている親レコードの項目を指定することも可能です。下記の例では「分類A でリンクした サイトID 10 のレコードの タイトル と、分類B の値が一致する」または「分類A でリンクしてた サイトID 10 のレコードの 数値A の値と、数値A の値が一致する」レコードのみを抽出して表示します。

```javascript linenums="1"
let data = {}
data.eq_Filter1 = 'ClassA~10,Title|ClassB';
data.eq_Filter2 = 'ClassA~10,NumA|NumA';
view.Filters.or_MyFilter = JSON.stringify(data);
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
|1.1.14.0 以降|OR条件による[フィルタ](../../../users-guide/hands-on/advanced/advanced-operations-link.md)機能の追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブル機能：レコードの一覧画面](../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [応用編：リンク](../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [レコードのアクセス制御（レコードの編集）](../../../users-guide/access-control/table-record-access-control.md)
-   [開発者ガイド：JSONデータレイアウト：View](../../json-data-layout/api-view/index.md)
-   [テーブルの管理：項目：添付ファイル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [テーブルの管理：項目：コメント](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-comments.md)
-   [テーブルの管理：一覧画面：常に検索条件を要求する](../../../managers-guide/manage-table/grid/table-management-always-request-search-condition.md)
-   [共通機能：横断検索](../../../users-guide/common/crosssearch.md)
-   [テーブルの管理：検索：検索の設定：横断検索を無効化](../../../managers-guide/manage-table/search/table-management-disable-cross-search.md)
-   [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)
-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理：項目：担当者](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [テーブルの管理：項目：数値](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：チェック](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：フィルタ：検索の種類](../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)
-   [テーブルの管理：項目：タイトル](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-title.md)
-   [テーブルの管理：項目：説明](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
