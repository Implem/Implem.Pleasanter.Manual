---
title: depts
icon: material/alpha-o-box
category: サーバスクリプト
order: '26000'
status: ''
parts: ''
urlstring: server-script-depts
translationKey: server-script-depts
shortname: depts
created: 2022-09-29
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で使用可能な[組織](../../../managers-guide/department-administration/index.md)に関する操作を行うオブジェクトです。

## プロパティ

プロパティはありません。

## メソッド

| No  | Name                                    | Description                                                                                                                       |
| :-- | :-------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [Create](server-script-depts-create.md) | 「[サーバスクリプト](../index.md)」から新しい「[組織](../../../managers-guide/department-administration/index.md)」を作成します。 |
| 2   | [Get](server-script-depts-get.md)       | 「deptオブジェクト」を取得します。                                                                                                |
| 3   | [Update](server-script-depts-update.md) | 「サーバスクリプト」から指定した組織を更新します。                                                                                |

## 使用例

下記の例では、ログインユーザが所属している組織の情報を取得します。

``` javascript linenums="1"
let myDept = depts.Get(context.DeptId);
if (myDept) {
    context.Log(`DeptName: ${myDept.DeptName}`);
}
```

## サンプルコード

??? note "1. 複合条件判定によるボタン表示制御"

    組織・グループの所属状況を複合判断し、ボタン表示を制御するサンプルコードです。

    ### 機能要件

    1.  以下条件で、ボタンの表示を制御します。

        <table border="1"><thead><tr><th>部門(組織)</th><th>役職(グループ)</th><th>承認</th><th>更新</th></tr></thead><tbody><tr><td rowspan="3">営業部</td><td>部長</td><td>表示</td><td>表示</td></tr><tr><td>課長</td><td>非表示</td><td>表示</td></tr><tr><td>一般社員</td><td>非表示</td><td>非表示</td></tr><tr><td rowspan="3">開発部</td><td>部長</td><td>非表示</td><td>表示</td></tr><tr><td>課長</td><td>非表示</td><td>表示</td></tr><tr><td>一般社員</td><td>非表示</td><td>非表示</td></tr></tbody></table>

    2.  部門、役職を以下のように定義します。

        | 種類   | ID  | 組織/グループ |
        | :----- | :-- | :-----------: |
        | 営業部 | 6   |     組織      |
        | 開発部 | 7   |     組織      |
        | 部長   | 3   |   グループ    |
        | 課長   | 2   |   グループ    |

        一般社員は、グループ所属なしの想定です。

    3.  ボタン制御
    
        - 承認：プロセスで設定
        - 更新：標準の更新ボタン

    これらを、`elements.DisplayType`で制御します。

    ```javascript linenums="1" title="条件：画面表示の前"
    // ===== 設定 =====
    const deptSales = 6; // 営業部
    const deptDev = 7; // 開発部
    const groupManager = 3; // 部長
    const groupSecManager = 2; // 課長

    // ボタンごとの表示条件:
    //   「depts のいずれか」かつ「groups のいずれか」に所属していれば表示。
    //   配列を空 [] にすると、その軸は「問わない（全員可）」を意味する。
    const buttonRules = [
        { 
            id: 'Process_1', 
            depts: [deptSales], 
            groups: [groupManager] 
        }, // 承認：営業部 × 部長
        {
            id: 'UpdateCommand',
            depts: [deptSales, deptDev],
            groups: [groupManager, groupSecManager],
        }, // 更新：営業/開発 × 部長/課長
    ];

    // ===== エンジン：基本は触らない =====
    const SHOW = 0; // DisplayType 0:標準（表示）
    const HIDE = 1; // DisplayType 1:無し（非表示）

    function isUserInDept(deptId, userId) {
        const dept = depts.Get(deptId);
        if (!dept) return false;
        return Array.from(dept.GetMembers()).some(function (m) {
            return m.UserId === userId;
        });
    }

    function isUserInGroup(groupId, userId) {
        const group = groups.Get(groupId);
        if (!group) return false;
        return group.ContainsUser(userId);
    }

    // 軸（部門 or 役職）の判定: 未指定（空配列）なら無条件 true、そうでなければいずれかに一致
    function matchesAny(ids, isMemberOf) {
        return ids.length === 0 || ids.some(isMemberOf);
    }

    const userId = context.UserId;

    buttonRules.forEach(function (rule) {
        const visible =
            matchesAny(rule.depts, function (id) {
                return isUserInDept(id, userId);
            }) &&
            matchesAny(rule.groups, function (id) {
                return isUserInGroup(id, userId);
            });
        elements.DisplayType(rule.id, visible ? SHOW : HIDE);
    });
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)
