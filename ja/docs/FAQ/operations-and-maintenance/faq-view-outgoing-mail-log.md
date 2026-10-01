---
title: プリザンターのメール送信ログを確認したい
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-view-outgoing-mail-log
translationKey: faq-view-outgoing-mail-log
shortname: ''
created: 2021-09-25
updated: 2024-04-29
---

## 回答

「OutgoingMailsテーブル」を参照してください。

---

## 概要

プリザンターの「メール送信ログ」を取得する手順です。プリザンターのメール送信ログは「データベース」内の「OutgoingMailsテーブル」に格納されています。

## 注意事項

1. 本手順はデータベースを直接操作するため、危険が伴います。事前に[バックアップ](../backup-restore/faq-backup-and-restore.md)を取得することを強くお勧めします。

## 操作手順

1. プリザンターをインストールしているサーバにログイン
1. Azure Data Studioなどデータベースに接続可能なツールを起動します。
1. 下記SQLを実行し「OutgoingMailsテーブル」のデータを取得

### サンプルコード

##### SQL（直近の1000件を取得する場合）

```
select top 100 * from "OutgoingMails" order by "OutgoingMailId" desc;
```

##### SQL（特定の期間のログを取得する場合）

```
select top 100 * from "OutgoingMails" where "CreatedTime" between '2021/09/25 00:00:00' and '2021/09/26 00:00:00' order by "OutgoingMailId" desc;
```

## ログの内容

「OutgoingMailsテーブル」の内容は下記のとおりです。

1. Host：送信先のホストです。
1. Port：送信先のポートです。
1. From：メール送信元のFromアドレスです。
1. To：メール送信先のToアドレスです。
1. Cc：メール送信先のCcアドレスです。
1. Bcc：メール送信先のBccアドレスです。
1. Title：メールの件名です。
1. Body：メールの本文です。
1. SentTime：メールの送信日時です。
1. Comments：使用しない項目です。
1. Creator：ユーザがログインしている場合、ユーザIDを示します。ユーザ名はUsersテーブルと紐づけて確認する必要があります。
1. Updator：上記と同様です。

## 関連情報

-   [FAQ：プリザンターのDBデータをバックアップする方法とリストアする方法を知りたい](../backup-restore/faq-backup-and-restore.md)