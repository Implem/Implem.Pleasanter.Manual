---
title: $p.apiSendMail
category: スクリプト
order: '0'
status: ''
parts: ''
urlstring: script-api-send-mail
translationKey: script-api-send-mail
shortname: ''
created: 2020-10-23
updated: 2026-09-09
---

## 概要

AjaxのPOSTリクエストにより、指定宛先にメールを送信します。

## 構文

##### JavaScript

```
$p.apiSendMail({
    id: 123,
    data: {
        To: <Toに設定したいメールアドレス>,
        Cc: <Ccに設定したいメールアドレス>,
        Bcc: <Bccに設定したいメールアドレス>,
        Title: <メール件名に設定する値>,
        Body: <メール本文に設定する値>
    }
})
``` 

## 各パラメータの説明

|パラメータ名|説明|
|:--|:--|
|ID|操作対象のサイトID|
|To|Toに設定する宛先|
|Cc|Ccに設定する宛先|
|Bcc|Bccに設定する宛先|
|Title|メールのタイトルに設定する値|
|Body|メールの本文に設定する値|

## 使用例

##### JavaScript

```
$p.apiSendMail({
    id: 123,
    data: {
        To: 'to_user1@example.com',
        Cc: 'cc_user1@example.com',
        Bcc: 'bcc_user1@example.com',
        Title: 'メール送信検証',
        Body: 'これはメール送信検証の本文です。'
    }
})
``` 
