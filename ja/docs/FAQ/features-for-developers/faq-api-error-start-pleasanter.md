---
title: プリザンター起動直後にAPI実行するとエラーになる。
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-api-error-start-pleasanter
translationKey: faq-api-error-start-pleasanter
shortname: ''
created: 2026-05-19
updated: 2026-05-25
---

## 回答

下記手順で「Webサービス」を起動した後でAPI実行をしてください。

---

## 概要

.NETの仕様上、プリザンターのAPIは、最初のリクエストを受け付け「Webサービス」が起動したことを契機に、実行できるようになります。プリザンター起動直後（systemctl start pleasanterやIIS再起動）でリクエストを受け付けるまではプリザンターの「Webサービス」は起動していないため、API実行をするとエラーになります。「Webサービス」として起動させるには下記いずれかの手順をおこなってください。

1. 一度ログインページ等の任意のページにアクセスする
1. [ヘルスチェック機能](../../managers-guide/ops-status-check/health-check.md)を使用する

[ヘルスチェック機能](../../managers-guide/ops-status-check/health-check.md)はプリザンターのバージョン1.4.8.0以降で使用が可能です。