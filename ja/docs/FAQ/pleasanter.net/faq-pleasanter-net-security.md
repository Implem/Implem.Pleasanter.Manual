---
title: Pleasanter.netのセキュリティについて
category: FAQ：Pleasanter.net
order: '9000'
status: ''
parts: ''
urlstring: faq-pleasanter-net-security
translationKey: faq-pleasanter-net-security
shortname: ''
created: 2019-12-12
updated: 2024-12-05
---

Pleasanter.netのセキュリティ対策につきましては、下記のとおりです。

-   TLSによる通信の暗号化
-   アカウント/パスワードによるユーザ認証
-   パスワードのハッシュ暗号化（SHA512）
-   SQL Database Transparent Data Encryptionによるデータの暗号化
-   SQL Database Advanced Data Securityによる不正なリクエストの防止
-   Application Gateway(WAF)による不正なリクエストの防止
-   全てのリクエストのロギング（保存期間1年間）
-   IPアドレスによる接続制限（スタンダードプランのオプションサービス）
-   国内Microsoft Azureデータセンターによる物理的なセキュリティ