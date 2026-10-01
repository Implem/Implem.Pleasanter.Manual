---
title: プリザンターからのメールが受信できない
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-not-send-mail
translationKey: faq-not-send-mail
shortname: ''
created: 2025-07-17
updated: 2025-10-02
---

## 回答

概要に記載の手順で確認してください。まずは以下手順を参照し、メール送信ログ、システムログを確認してください。  
[FAQ：プリザンターのメール送信ログを確認したい](faq-view-outgoing-mail-log.md)  
[FAQ：プリザンターのログを確認したい \| Pleasanter](faq-view-syslogs.md)

---

## 概要

プリザンターからのメールが受信できない場合、下図の番号順に確認してください。

![メールが受信できない場合の確認箇所を番号で示した図](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/6aa7275b4971493dafcb694356d6bc5c.png)

## プリザンター（①、②）

|確認ポイント|考えられる原因|
|---|---|
|・メール送信ログ（OutgoingMails）にメール送信結果が記録されているか|・パラメータ設定誤り<br>・ネットワーク不通<br>・通知の設定条件誤り|
|・システムログ（Syslogs）にエラーが記録されていないか|・パラメータ設定誤り<br>・ネットワーク不通<br>・通知の設定条件誤り|

始めにメール送信ログ（OutgoingMailsテーブル）を確認し、メール送信結果が記録されているかを確認してください。確認手順は以下マニュアルを参照してください。  
[FAQ：プリザンターのメール送信ログを確認したい](faq-view-outgoing-mail-log.md)  
メール送信結果が記録されていない場合は、以下の点を確認してください。
    - テーブルの管理で[通知](../../users-guide/hands-on/advanced/advanced-operations-notification.md)や[リマインダー](../../users-guide/hands-on/advanced/advanced-operations-notification.md)、[プロセス](../../users-guide/hands-on/advanced/advanced-operations-process.md)の通知の設定が適切か。
    - [Mail.json](../../setup/parameters/mail-json.md)の設定が適切か。
    - プリザンターと送信メールサーバとのネットワークに障害はないか。

メール送信結果が記録されている場合は、プリザンターとしては設定内容に従って送信メールサーバに送信依頼を行った状態です。テーブルの管理の各設定とメール送信結果の送信先を確認して想定した宛先が送信先に含まれているかを確認してください。

## 送信側メールサーバ（③）

|確認ポイント|考えられる原因|
|---|---|
|・送信のログがあるか<br>・ログにエラーが記録されていないか|・パラメータ設定誤り（接続情報、資格情報）<br>・送信先メールアドレスがリストに含まれていないか|

①②に問題がない場合、次に確認するのは送信メールサーバです。メールサーバには宛先のアドレスをみて迷惑メールやスパムメールと判断して隔離する機能を有している場合があります。送信すべきメールが隔離されていないかを確認してください。

## 受信側メールサーバ／ゲートウェイ（④）

|確認ポイント|考えられる原因|
|---|---|
|・受信のログがあるか<br>・ログにエラーが記録されていないか|・パラメータ設定誤り（接続情報、資格情報）<br>・送信先メールアドレスが停止リストに含まれていないか|

③に問題がない場合、次に確認するのは相手先の受信メールサーバです。送信メールサーバと同様にメールサーバには宛先のアドレスをみて迷惑メールやスパムメールと判断して隔離する機能を有している場合があります。送信すべきメールが隔離されていないかを確認してください。

## 受信者メーラー（⑤）

|確認ポイント|考えられる原因|
|---|---|
|・迷惑メールフォルダ|・DKIM/SPFなどの設定不備|

最後に確認するのは受信者のメーラー（メールソフト）です。迷惑メールやスパムメールと判断して隔離されていないか、各自設定した振り分けルールに従って自動的に振り分けされていないかなどを確認してください。

## 関連情報

-   [FAQ：プリザンターのメール送信ログを確認したい](faq-view-outgoing-mail-log.md)
-   [FAQ：プリザンターのログを確認したい \| Pleasanter](faq-view-syslogs.md)
-   [応用編：通知、リマインダー](../../users-guide/hands-on/advanced/advanced-operations-notification.md)
-   [応用編：プロセスと状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [パラメータ設定：Mail.json](../../setup/parameters/mail-json.md)