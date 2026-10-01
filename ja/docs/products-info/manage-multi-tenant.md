---
title: マルチテナント管理機能
category: マルチテナント管理機能
order: '100'
status: ''
parts: ''
urlstring: manage-multi-tenant
translationKey: manage-multi-tenant
shortname: マルチテナント管理機能
created: 2026-08-03
updated: 2026-08-12
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/products-info/assets/3c9290c6661f437fb0e9de68426c2d2c.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/products-info/assets/a4c61adc096543ef9523bf97fe6e868b.svg#only-dark)](https://pleasanter.org/support/)

## 概要

### テナント

マルチテナント管理機能は、1つのプリザンター環境で複数の「[テナント](../managers-guide/tenant-administration/index.md)」（ユーザ、グループ、組織、サイトなどすべてを含む入れ物）を利用可能にする機能です。

![テナントにユーザ・グループ・組織・サイトなどが含まれることを示す図](https://pleasanter.org/files/images/ja/products-info/assets/3c5428cc24fb46bdab10c450d5902150.png)

### シングルテナントとマルチテナント

通常のプリザンターは**シングルテナント**です。1つのプリザンターで1つのテナントを利用できます。**マルチテナント**管理機能を使うと、1つのプリザンターで複数のテナントを作成・利用できるようになります。

![シングルテナントとマルチテナントの違いを示す図](https://pleasanter.org/files/images/ja/products-info/assets/dc52c11160e64e5385a03c5acb4edea2.png)

## マルチテナントのメリット

マルチテナントは、特に大規模運用環境において、大きなメリットがあります。

### 部門毎にアクセスできるサイトを分けたい

下図のように、全社で1台のプリザンターをシングルテナント構成で運用している場合、部門毎にアクセスできるサイトを分けるためには、テーブル毎に細かなアクセス制御を設定する必要があります。

一方、マルチテナントであれば、特別な設定を行わなくても、同一テナント内は自由にアクセスでき、他のテナントに対してはアクセス不可となります。

![部門毎のアクセス制御をシングルテナントとマルチテナントで比べた図](https://pleasanter.org/files/images/ja/products-info/assets/dea3834610824e31a71bd7655ad76657.png)

### 部門別・拠点別の管理を合理化したい

下図のように、事業部毎に1台のプリザンターをシングルテナント構成で運用している場合、部門毎の独立性は担保されていますが、事業部の人員や、契約プラン、契約期間は一般的に異なります。また、プリザンターの管理を所管する部門や人員数も事業部毎に異なります。このような場合、以下のような課題が発現します。

1. ライセンス管理の煩雑化
1. メンテナンス業務の重複、人員の冗長化
1. 事業部門・拠点の新設・統廃合への備えが困難

マルチテナントの導入により、このような課題を解消できます。

1. ライセンス管理の一元化、ライセンスコストの低減
1. メンテナンス業務の集約化、人員の圧縮
1. 事業部門・拠点の新設・統廃合に対して柔軟に対応

![マルチテナントの導入で運用上の課題が解消されることを示す図](https://pleasanter.org/files/images/ja/products-info/assets/3d4fb7f6ac95407381046fb290f1fcea.png)

### マルチテナント機能の利用

マルチテナント管理機能は、以下の各APIを通して利用できます。

| API                                   | URL                               | 説明                                         |
| :------------------------------------ | :-------------------------------- | :------------------------------------------- |
| 「API：テナント操作：テナント作成」 | /api/tenants/Create               | テナントと初期管理者ユーザを作成します       |
| 「API：テナント操作：テナント一覧取得」 | /api/tenants/Get                  | テナントの一覧を取得します                   |
| 「API：テナント操作：テナント停止」 | /api/tenants/{テナントID}/Suspend | テナントを停止し、ログイン不可の状態にします |
| 「API：テナント操作：テナント再開」 | /api/tenants/{テナントID}/Resume  | 停止中のテナントを再開します                 |
| 「API：テナント操作：テナント削除」 | /api/tenants/{テナントID}/Delete  | テナントの削除を申請します                   |

## 前提条件

1. テナント操作APIは「[特権ユーザ](../managers-guide/user-administration/user-management-privileged-users.md)」のみ実行できます。
1. APIの操作を行う前に[APIキーの作成](../developers-guide/api/basics/api-key.md)を実施してください。APIキーは「特権ユーザ」で作成してください。
1. [MultiTenant.json](../setup/parameters/multitenant-json.md)のパラメータ「DefaultTenantId」の値を正しく設定しないと、誰もログインできなくなる可能性があります。

## 保護テナント

[MultiTenant.json](../setup/parameters/multitenant-json.md)のパラメータ「DefaultTenantId」（既定値：1）で指定したテナントは保護テナントとなり、停止、再開、削除の対象テナントとして指定できません。

## エラー時の確認事項

[・API使用時の注意点やエラーが発生する場合の確認事項](../FAQ/features-for-developers/faq-api.md)  
[・FAQ:変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../FAQ/features-for-developers/faq-json-format.md)

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.5.7.0 以降   | 機能追加 |
