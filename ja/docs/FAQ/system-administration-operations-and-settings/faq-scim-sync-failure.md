---
title: SCIMでユーザ情報が連携されない
category: FAQ：システム管理の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-scim-sync-failure
translationKey: faq-scim-sync-failure
shortname: FAQ：SCIMでユーザ情報が連携されない
created: 2026-08-13
updated: 2026-09-08
---

## 回答

接続テストの成功可否、エラーメッセージの内容により、解決策が異なります。以下を参考にしてください。

---

## 接続テストに失敗する

以下の6点を確認してください。

1. 接続先URLが正しい
1. 接続先URLの末尾が/scim/v2である
1. SCIMトークンが正しい
1. SCIMトークンが有効または期限内である
1. プリザンターでSCIM機能を有効化している
1. IPアドレス制限で接続が拒否されていない

## 401 Unauthorizedが返る

SCIMトークンが正しくない可能性があります。SCIMトークンが有効か、有効期限内か、接続先のテナント用であるかを確認してください。

## 403 Forbiddenが返る

IPアドレス制限でIDプロバイダからの接続を拒否している可能性があります。[Security.json](../../setup/parameters/security-json.md)のパラメータAllowIpAddressesに、IDプロバイダの送信元IPアドレスが間違いなく含まれていることを確認してください。

## externalId is requiredが返る

UserまたはGroupのexternalIdが送信されていません。IDプロバイダ側の属性マッピングで、externalIdにobjectIdを設定してください。

## 同じ名前のグループが複数作成される

グループは名前ではなくexternalIdで照合してください。Microsoft Entra ID側で別のobjectIdを持つグループは、同じ名前でも別のグループとして作成されます。

## 見直すべきマニュアル

1. 「[SCIM機能](../../setup/additional/account-integration/scim/index.md)」
1. 「SCIM機能：プリザンターの設定」
1. 「SCIM機能：IDプロバイダの設定」
1. [Security.json](../../setup/parameters/security-json.md)
1. [Scim.json](../../setup/parameters/scim-json.md)
