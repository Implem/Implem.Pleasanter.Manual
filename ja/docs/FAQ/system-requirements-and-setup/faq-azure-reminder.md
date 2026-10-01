---
title: Azure上でプリザンターを構築した際のリマインダーの設定方法を教えてほしい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-azure-reminder
translationKey: faq-azure-reminder
shortname: ''
created: 2018-12-26
updated: 2024-04-29
---

**プリザンターのバージョン1.3.7.0以降では、設定ファイル[BackgroundService.json](../../setup/parameters/background-service-json.md)の`"Reminder"`をtrueにすることで、[リマインダー](../../users-guide/hands-on/advanced/advanced-operations-notification.md)を実行できるようになりました。本FAQは1.3.6以前のプリザンターの内容となります。**

## 回答

AppServiceの「Webジョブ」機能でToolsフォルダ内の「Reminder.ps1」を設定してください。

---

## 概要

AppServiceでスクリプトを常駐プログラムとして実行するには「Webジョブ」機能を使用します。

## 操作手順

1.  [こちら](https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/Reminder.ps1)からReminder.ps1ファイルをダウンロードする
1.  ダウンロードしたReminder.ps1ファイルを開き、1行目のコメントアウトを有効化（#を消す）し、`http://localhost/`の部分をクライアントからアクセス可能なURLに変更して保存する
1.  AzureポータルでプリザンターのApp Serviceを選択する
1.  左側の機能一覧から「Webジョブ」を選択する
1.  メニューバーの「＋追加」をクリックする
1.  ジョブ名（任意）を入力し、手順2で保存した「Reminder.ps1」ファイルをアップロードする。  
    その際、「種類」は”継続”を、「スケール」は”単一のインスタンス”を選択する

## 関連情報

-   [パラメータ設定：BackgroundService.json](../../setup/parameters/background-service-json.md)
-   [応用編：通知、リマインダー](../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [Reminder.ps1](https://github.com/Implem/Implem.Pleasanter/blob/master/Implem.Pleasanter/Tools/Reminder.ps1)
