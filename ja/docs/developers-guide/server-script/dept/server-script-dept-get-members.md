---
title: dept.GetMembers
icon: material/alpha-m-box
category: サーバスクリプト
order: '26200'
status: ''
parts: ''
urlstring: server-script-dept-get-members
translationKey: server-script-dept-get-members
shortname: dept.GetMembers
created: 2022-10-06
updated: 2026-09-08
---

## 概要

[サーバスクリプト](../index.md)で組織に所属するユーザ情報を取得するためのメソッドです。

## 構文

``` js
dept.GetMembers()
```

## 戻り値

「userオブジェクト」のリストを返却します。

## 使用例

下記の例では、ログインユーザが所属している組織のメンバーのユーザ名をログに出力します。

``` js linenums="1" hl_lines="3"
let myDept = depts.Get(context.DeptId);
if (myDept) {
    const members = myDept.GetMembers();
    for (let member of members) {
        context.Log(`Name: ${member.Name}`);
    }
}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
