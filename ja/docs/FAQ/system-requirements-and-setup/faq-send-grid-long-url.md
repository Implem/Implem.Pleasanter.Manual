---
title: プリザンターからSendGridを使って送信されたメールのURLが長くなってしまう
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-send-grid-long-url
translationKey: faq-send-grid-long-url
shortname: ''
created: 2020-02-05
updated: 2024-04-29
---

## 回答

SendGridのFAQサイトを参照の上、設定を変更してください。

---

## 概要

メール送信にSendGridを利用している環境において、メール内に記載されたURLが以下のように長くなっている場合、以下URLを確認の上、SendGridの設定を変更してください。

SendGridの よくあるご質問 -トラブル対策：[メール本文内のURLが勝手に置換されてしまいます。解除できますか？](https://support.sendgrid.kke.co.jp/hc/ja/articles/206253421-%E3%83%A1%E3%83%BC%E3%83%AB%E6%9C%AC%E6%96%87%E5%86%85%E3%81%AEURL%E3%81%8C%E5%8B%9D%E6%89%8B%E3%81%AB%E7%BD%AE%E6%8F%9B%E3%81%95%E3%82%8C%E3%81%A6%E3%81%97%E3%81%BE%E3%81%84%E3%81%BE%E3%81%99-%E8%A7%A3%E9%99%A4%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%81%8B)

``` text
2020/02/○ 月 (○ 日超過)
    見積書の作成)株式会社○○様宛見積書の作成--- 吉田 芳雄 (未着手)
https://test3458.ct.sendgrid.net/wf/click?upn=2BC6H8QrcQ7RDnsMv1lFcA9aCc2xTTQ-3D_BqOEXxDcFMnimDkNxzZLhWAikutFfL1K-2BMpXS5Uiq2BC6H8QrcQ7RDnsMv1lFcA9aCc2xTTQ-3D_BqOEXxDcFMnimDkNxzZLhWAikutFfL1K-2BMpXS5Uiq
```
