---
title: Validation.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: validation-json
translationKey: validation-json
shortname: Validation.json
created: 2023-09-14
updated: 2024-09-13
---

## 概要

プリザンターは半角文字、全角文字にかかわらず全ての文字を1文字としてカウントします。これを半角を1文字、全角を2文字とカウントするような運用をしたい場合は本パラメータを設定します。設定内容は「テーブルの管理：エディタ：項目の詳細設定：最大文字数」のカウント方法に反映されます。

## 注意事項

* 原則変更不要です。カウント方法を変更したい場合のみ設定してください。
* パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|MaxLength|null|未使用|
|MaxLengthCountType|"Character"|半角全角にかかわらず1文字とカウントする場合は"Character"と指定。1文字のカウント方法を正規表現で設定する場合は"Regex"と指定。|
|SingleByteCharactorRegexClient|"\\x01-\\x7E\\uFF65-\\uFF9F"|MaxLengthCountTypeを"Regex"と指定した場合に有効。１文字と数える文字のクライアントサイドの正規表現。|
|SingleSyteCharactorRegexServer|"\\u0001-\\u007E\\uFF65-\\uFF9F"|MaxLengthCountTypeを"Regex"と指定した場合に有効。１文字と数える文字のサーバサイドの正規表現。|
