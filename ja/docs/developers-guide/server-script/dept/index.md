---
title: dept
icon: material/alpha-o-box
category: サーバスクリプト
order: '26100'
status: ''
parts: ''
urlstring: server-script-dept
translationKey: server-script-dept
shortname: dept
created: 2022-09-29
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で[組織](../../../managers-guide/department-administration/index.md)の情報を読み取るためのオブジェクトです。「deptsオブジェクト」のGetメソッドで取得します。

## プロパティ

| No  | プロパティ名 | get | set | type   | 説明       |
| :-- | :----------- | :-- | :-- | :----- | :--------- |
| 1   | DeptId       | ○   | -   | int    | 組織ID     |
| 2   | DeptCode     | ○   | -   | string | 組織コード |
| 3   | DeptName     | ○   | -   | string | 組織名     |

## メソッド

| No  | Name                                            | Description                                            |
| :-- | :---------------------------------------------- | :----------------------------------------------------- |
| 1   | [GetMembers](server-script-dept-get-members.md) | 所属しているユーザの「userオブジェクト」を取得します。 |

## 使用例

下記の例では、ログインユーザが所属している組織の「deptオブジェクト」を取得し、組織コードと組織名をログに出力しています。

```js linenums="1"
let myDept = depts.Get(context.DeptId);
if (myDept) {
    context.Log(`${myDept.DeptCode},${myDept.DeptName}`);
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [組織管理機能](../../../managers-guide/department-administration/index.md)
-   [開発者ガイド：サーバスクリプト：dept.GetMembers](server-script-dept-get-members.md)
