---
title: $p.deptId
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-dept-id
translationKey: script-dept-id
shortname: $p.deptId
created: 2022-12-20
updated: 2026-08-27
---

## 概要

ログインしているユーザの組織IDを取得する関数について説明します。

## 構文

```
$p.deptId()
```

## 使用例

以下は組織を入力する項目にログインしているユーザの組織IDを設定するスクリプトです。

##### JavaScript

```
$p.set($p.getControl('ClassA'), $p.deptId());
```
