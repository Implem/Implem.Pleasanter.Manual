---
title: 大規模運用サポート機能
category: 大規模運用サポート機能
order: '0'
status: ''
parts: ''
urlstring: large-scale-ops-supports
translationKey: large-scale-ops-supports
shortname: 大規模運用サポート機能
created: 2026-08-07
updated: 2026-09-08
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/products-info/assets/6b84d23846e34a02b755057e1aa17578.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/products-info/assets/896adb03e25c43ef8d47317beb90f854.svg#only-dark)](https://pleasanter.org/support/)

## 概要

全社インフラとして大規模運用時の安定した応答性能を支える追加機能を提供します。年間サポートサービスの契約プランに応じて、利用できる機能が異なります。

|機能|エントリー|ベーシック|ベーシックプラス|ビジネス|ビジネスプラス|アンリミテッド|
|---|:-:|:-:|:-:|:-:|:-:|:-:|
|[同一テーブルに対して大量データを一括操作する処理の同時実行を抑止する](../setup/additional/performance/block-site-task-while-running.md)|	|〇|〇|〇|〇|〇|
|[SCIM機能](../setup/additional/account-integration/scim/index.md)|||〇|〇|〇|〇|
|[SAMLレスポンス内のユーザ情報をカスタム項目としてユーザ画面に取り込む](../setup/additional/authn-authz/saml-response-mapping.md)|||〇|〇|〇|〇|
|[キューイング](../setup/additional/performance/queuing-manage-jobs.md)||||〇|〇|〇|
|[レートリミット機能](../setup/additional/performance/ratelimit.md)||||〇|〇|〇|
|[サイト設定のキャッシュを有効化](../setup/additional/performance/enable-site-settings-cache.md)||||〇|〇|〇|
|[マルチテナント管理機能](manage-multi-tenant.md)[^1]||||||〇|

[^1]: アンリミテッドプランの契約に加え、マルチテナントオプションの契約が必要です。

## 制限事項

1. 「大規模運用サポート機能」は年間サポート旧プランでは使用できません。

## 各機能の概要

#### [同一テーブルに対して大量データを一括操作する処理の同時実行を抑止する](../setup/additional/performance/block-site-task-while-running.md)

1つのテーブルに対してインポートや一括更新など大量のデータを一括操作する処理を同時に実行すると、データベースが高負荷状態になり処理時間が非常に長くなることでシステム全体のパフォーマンスが悪化する場合があります。本機能では1つのテーブルに対して大量データを一括操作する処理の同時実行を抑止することでシステム全体のパフォーマンスを安定化することができます。

#### [SCIM機能](../setup/additional/account-integration/scim/index.md)

SCIM（System for Cross-domain Identity Management）は、異なるシステムやクラウドサービス間で、ユーザ情報・グループ情報を自動で連携・管理するための標準規格（プロトコル）です。SCIM機能を利用すると、Microsoft Entra ID（旧Azure AD）のようなIDプロバイダとプリザンターとの間で、ユーザ情報・グループ情報を自動連携・管理できます。

#### [SAMLレスポンス内のユーザ情報をカスタム項目としてユーザ画面に取り込む](../setup/additional/authn-authz/saml-response-mapping.md)

SAML認証でのログインに成功すると、SAMLレスポンスとして渡されるユーザデータを基に、プリザンターのユーザ情報を作成・更新できます。本機能はSAML認証の[SamlParameters.Attributes項目一覧](../setup/additional/authn-authz/saml.md#Attributes)に記載されている項目以外の任意の項目を、拡張項目を使って設置した項目へマッピングする機能です。

#### [キューイング](../setup/additional/performance/queuing-manage-jobs.md)

高負荷処理を、リクエスト中に即時実行するのではなく、バックグラウンドジョブとしてキュー（待ち行列）へ登録し、順次実行する機能です。ユーザは、画面を通じて自分が実行したジョブの一覧を確認できますが、他のユーザが実行したジョブの一覧を確認することはできません。

#### [レートリミット機能](../setup/additional/performance/ratelimit.md)

「レートリミット機能」は、特定の利用者・IPアドレス・APIキー単位で、過剰なリクエスト（短時間の大量な画面操作や、エクスポート・インポートなどの重い処理の集中実行）を抑制し、システムの安定稼働を支える機能です。一時的なアクセス集中（バースト）の許容、一定時間内の実行回数制限、同時実行数制限などを柔軟に設定でき、利用環境に応じた負荷制御を実現します。

#### [サイト設定のキャッシュを有効化](../setup/additional/performance/enable-site-settings-cache.md)

プリザンターは、テーブルの参照や更新の都度、テーブルの設定情報であるサイト設定をデータベースから読み込みます。多数のテーブルを相互に参照する複雑なリンク構成のテーブルほど、この読み込みが処理性能に影響を与える可能性があります。本機能は、一度読み込んだサイト設定をWebサーバのメモリ上にキャッシュし、以降の処理で再利用します（データベースやKVSなどへの永続化は行いません。処理速度を優先した選択であり、サーバの再起動によってキャッシュは消去されます）。これにより、データベースへのアクセス回数が削減され、処理性能が向上します。キャッシュの有効化はテーブルごとに設定できます。テーブルの構成や運用状況に応じてオン・オフを切り替え可能です。

#### [マルチテナント管理機能](manage-multi-tenant.md)

マルチテナント管理機能は、1つのプリザンター環境で複数のテナント（サイト、組織、グループ、ユーザなどすべてを含む入れ物）を利用可能にする機能です。
