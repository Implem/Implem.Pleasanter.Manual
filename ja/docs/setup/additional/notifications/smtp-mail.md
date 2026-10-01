---
title: プリザンターからメールを送信できるように設定する
category: 追加設定：通知
order: '100'
status: ''
parts: ''
urlstring: smtp-mail
translationKey: smtp-mail
shortname: メールの送信設定
created: 2019-04-29
updated: 2026-06-09
---

リマインダーや通知機能でメールを送信するためには以下の設定が必要となります。

## Mail.jsonの設定  

こちらを参照：[パラメータ設定：Mail.json](../../../users-guide/common/mail.md)  

## 設定変更の反映

-   Windows環境の場合はIISを再起動してください。  
-   Linux環境の場合はプリザンターのサービスを再起動してください。  

```
sudo systemctl restart pleasanter
```

-   Microsoft Azure環境の場合はApp Serviceを再起動してください。