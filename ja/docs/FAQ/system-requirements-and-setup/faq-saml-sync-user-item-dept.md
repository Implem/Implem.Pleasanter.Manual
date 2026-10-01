---
title: SAML認証で、ユーザー項目の「DeptCode」を指定せずに組織に反映したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-saml-sync-user-item-dept
translationKey: faq-saml-sync-user-item-dept
shortname: ''
created: 2025-07-14
updated: 2025-09-24
---

## 回答

プリザンターでは、「DeptCode」の値をもとに組織コードに設定する属性名を指定します。そのため、「DeptCode」が無い状態では組織に反映されません。

---

## 概要

[SAML認証](../../setup/additional/authn-authz/saml.md)の設定におけるAuthentication.jsonの「DeptCode」と「Dept」の役割は次のようになっています。

### DeptCode

「組織コード」に設定する属性名を指定します。ここで取得した組織コードを持つ[組織](../../managers-guide/department-administration/index.md)がこのユーザに割り当てられます。該当する[組織](../../managers-guide/department-administration/index.md)が存在しなかった場合は新しい組織が作成されます。

### Dept

「組織名」に設定する属性名を指定します。「DeptCode」から引き当てた[組織](../../managers-guide/department-administration/index.md)の組織名を更新します。該当する組織が存在しなかった場合はこの「組織名」で組織が作成されます。

## 関連情報

-   [SAML認証を利用する](../../setup/additional/authn-authz/saml.md)
-   [組織管理機能](../../managers-guide/department-administration/index.md)
