---
title: Linux上でセットアップしたプリザンターにアクセスすると「502 Bad Gateway」が表示されてしまう
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-bad-gateway
translationKey: faq-bad-gateway
shortname: ''
created: 2024-09-25
updated: 2024-10-10
---

## 回答

SELinuxの設定により、リバースプロキシのアクセスに制限がかけられている可能性があります。コマンドを実行しアクセス制限を解除してください。

---

## 解消手順

以下コマンドを実行します。

``` bash
getenforce
```

### 「コマンド 'getenforce' が見つかりません。」「Permissive」「Disabled」のいずれかが表示された場合

SELinuxの設定が原因ではないため、本FAQの対象外です。

### 「Enforcing」が表示された場合

以下コマンドを実行します。

``` bash
sudo setsebool -P httpd_can_network_connect on
```

SELinuxの`httpd_can_network_connect`を変更することで、該当のサーバにおいてスクリプトやモジュールによるネットワーク接続がすべて許可されます。
