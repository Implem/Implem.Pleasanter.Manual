---
title: groupMember
icon: material/alpha-o-box
category: サーバスクリプト
order: '32000'
status: ''
parts: ''
urlstring: server-script-group-member
translationKey: server-script-group-member
shortname: groupMember
created: 2021-06-08
updated: 2026-05-21
---

## 概要

[サーバスクリプト](../index.md)で使用可能な「グループメンバー」の情報を読み取るためのオブジェクトです。「groupオブジェクト」のGetMembersメソッドで「groupMemberオブジェクト」のコレクションを取得できます。

## プロパティ

|No| 項目名 | get | set | type | 説明 |
|--:|:--|:-:|:-:|:--|:--|
| 1| GroupId | 〇 |  | int | グループID |
| 2| GroupName | 〇 |  | string | グループ名<span class="pl-attention">^*1^</span> |
| 3| DeptId  | 〇 |  | int |組織ID |
| 4| DeptName | 〇 |  | string | 組織名<span class="pl-attention">^*1^</span> |
| 5| DeptCode | 〇 |  | string | 組織コード<span class="pl-attention">^*1^</span> |
| 6| UserId | 〇 |  | int | ユーザID |
| 7| LoginId | 〇 |  | string | ログインID<span class="pl-attention">^*1^</span> |
| 8| Name | 〇 |  | string | ユーザ名<span class="pl-attention">^*1^</span> |
| 9| UserCode | 〇 |  | string | ユーザコード<span class="pl-attention">^*1^</span> |
|10| TenantManager | 〇 |  | bool | テナント管理者であればTrue<span class="pl-attention">^*1^</span> |
|11| Disabled | 〇 |  | bool | 無効であればTrue<span class="pl-attention">^*1^</span> |
|12| Admin | 〇 |  | bool | [グループの管理権限](../../../managers-guide/group-administration/group-add-user.md)を持っていればTrue |

<span class="pl-attention">*1</span>　バージョン1.5.2.0以降で利用可

グループメンバーが[組織](../../../managers-guide/department-administration/index.md)、[グループ](../../../managers-guide/group-administration/index.md)、[ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)かに応じてGroupId、DeptId、UserIdの各プロパティに下表の値が格納されます。

||メンバーがユーザの場合|メンバーが組織の場合|メンバーが子グループの場合|
|:-:|:-:|:-:|:-:|
|GroupId|0|0|グループID|
|DeptId|0|組織ID|0|
|UserId|ユーザID|0|0|

## 使用例

### バージョン1.5.1.0以前の使用例

下記の例ではグループID 1 のグループに所属するメンバーの組織IDとユーザIDをログに出力します。

##### JavaScript

```js
let group = groups.Get(1);
for (let member of group.GetMembers()) {
    context.Log(`${member.DeptId},${member.UserId}`);
}
```

### バージョン1.5.2.0以降の使用例

下記の例ではグループID 6のメンバー情報を取得し、ユーザメンバー、組織メンバー、子グループメンバーかに応じて取得情報を切り分けています。

##### JavaScript

```js
// グループID=6のグループオブジェクトを取得する
let group = groups.Get(6);

// 出力件数カウンタ初期化
let cnt = 0;

// グループが存在する場合のみ処理を実行
if (group) {

    // グループメンバー一覧をイテレート
    // GetMembers() はユーザ・組織・グループの各メンバーを返す
    for (let member of group.GetMembers()) {

        // メンバー種別の判定：UserId / DeptId / GroupId のいずれか1つだけが非ゼロになる

        if (member.UserId != 0) {
            // UserId != 0 の場合はユーザメンバー
            context.Log(`
            【ユーザ】
            UserId        : ${member.UserId}         // ユーザID
            LoginId       : ${member.LoginId}        // ログインID
            Name          : ${member.Name}           // 表示名
            UserCode      : ${member.UserCode}       // ユーザコード
            TenantManager : ${member.TenantManager}  // テナント管理者フラグ
            Disabled      : ${member.Disabled}       // 無効フラグ
            Admin         : ${member.Admin}          // グループの管理者フラグ
            `);

        } else if (member.DeptId != 0) {
            // DeptId != 0 の場合は組織メンバー
            context.Log(`
            【組織】
            DeptId   : ${member.DeptId}   // 組織ID
            DeptName : ${member.DeptName} // 組織名
            DeptCode : ${member.DeptCode} // 組織コード
            `);

        } else if (member.GroupId != 0) {
            // GroupId != 0 の場合はグループメンバー（ネストされたグループ）
            context.Log(`
            【グループ】
            GroupId   : ${member.GroupId}   // グループID
            GroupName : ${member.GroupName} // グループ名
            `);
        }

        // メンバーごとの区切り線
        context.Log('-----');

        // 出力件数をインクリメント
        cnt++;
    }
}

// 処理したメンバーの総件数を出力
context.Log(`出力件数： ${cnt}件`);
```

## 対応バージョン

|対応バージョン|内容|
|---|---|
|1.5.2.0 以降|groupMemberオブジェクトに以下のプロパティを追加<br>GroupName、DeptName、DeptCode、LoginId、Name、<br>UserCode、TenantManager、Disabled|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [グループ管理機能：所属するユーザ/組織の追加](../../../managers-guide/group-administration/group-add-user.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)
-   [グループ管理機能](../../../managers-guide/group-administration/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)