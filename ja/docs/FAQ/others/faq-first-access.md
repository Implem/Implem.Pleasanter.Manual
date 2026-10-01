---
title: しばらく操作していないと初回アクセスに時間がかかる
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-first-access
translationKey: faq-first-access
shortname: ''
created: 2019-10-09
updated: 2024-04-29
---

## 回答

IISの設定「アイドルタイムアウトの操作」を「Terminate」から「Suspend」に変更してください。

---

## 概要

しばらく操作しなかった後で別ページにアクセスすると時間がかかることがありますが、これはIISのデフォルトの設定では一定時間アイドル状態（アクセスのない状態）になったワーカープロセスが停止するため、その後の最初のリクエストで時間がかかってしまいます。設定変更により、ワーカープロセスを停止せずにスワップアウトするようになるため、再リクエスト時の応答時間を短縮することができます。

## 操作手順

1. IISマネージャーを開きます。
1. Pleasanterで使用しているアプリケーションプール(初期設定ではDefaultAppPool)を選択し、アプリケーションプール既定値の設定を選択します。
1.  「プロセスモデル」の「アイドルタイムアウトの操作」を、「Terminate」から「Suspend」に変更します。

![IISマネージャーでアイドルタイムアウトの操作を Suspend に変更するところ](https://pleasanter.org/files/images/ja/FAQ/others/assets/475c3f15a2144bc09667f81d0c0e25b3.png)

