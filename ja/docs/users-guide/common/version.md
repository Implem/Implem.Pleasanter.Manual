---
title: バージョン
category: 共通機能
order: '5'
status: ''
parts: ''
urlstring: version
translationKey: version
shortname: バージョン
created: 2026-05-22
updated: 2026-07-06
---

## 概要

プリザンターのバージョンやライセンス等の情報を表示します。

## 操作手順

1. ナビゲーションメニューの「ヘルプ」メニューより「バージョン」をクリックしてください。
1. バージョンが表示されます。

### バージョン画面の一例（Community Editionの場合）

![Community Edition のバージョン画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/82a086f4661d49cabf904802f5bac08a.png)

### バージョン画面の一例（Pleasanter Extensionsトライアル中の場合）

![Pleasanter Extensions トライアル中のバージョン画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/248f53163f6141dc94ed692cde2ca636.png)

### バージョン画面の一例（Enterprise Editionの場合）

![Enterprise Edition のバージョン画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/b7b50bb71f864c74947e808fe13c1c81.png)

### 画面項目一覧

|No.|画面項目名|説明|
|:---|:---|:---|
|1|バージョン|プリザンターのバージョンです。|
|2|ライセンス|プリザンターのライセンスです。Community Editionおよび[Pleasanter Extensionsのトライアル中](../../products-info/extensions-trial/index.md)の場合、クリックすると[AGPL](https://github.com/Implem/Implem.Pleasanter/blob/net-framework/LICENSE)の説明のページを表示します。プリザンターのライセンスについては[AGPLに関するFAQ集](../../FAQ/license/faq-license-agpl.md)を参照ください。|
|3|Pleasanter Extensions トライアル|[Pleasanter Extensionsのトライアル](../../products-info/extensions-trial/index.md)のみ表示します。|
|4|トライアル期限|[Pleasanter Extensionsのトライアル](../../products-info/extensions-trial/index.md)のみ表示します。トライアル期限を表示します。|
|5|商用ライセンスへの切り替え|Community Editionおよび[Pleasanter Extensionsのトライアル](../../products-info/extensions-trial/index.md)で表示します。クリックすると[拡張コンテンツのご案内ページ](https://pleasanter.org/extensions/#sec-3)を表示します。|
|6|ライセンス期限|Enterprise Editionのみ表示されます。ライセンスの期限を表示します。[Version.json](../../setup/parameters/version-json.md)の設定で表示の有無を指定することができます。|
|7|使用者|Enterprise Editionのみ表示されます。ライセンスの使用者名を表示します。「Version.json」の設定で表示の有無を指定することができます。|
|8|ユーザ数上限|Enterprise Editionのみ表示されます。ユーザ数の上限を表示します。「Version.json」の設定で表示の有無を指定することができます。|
|9|データベース使用量|[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)でログインすると、バージョン画面で現在のデータ使用量を確認することができます。詳細は[DB使用量を確認したい](../../FAQ/operations-and-maintenance/faq-db-amount-to-use.md)を参照ください。|
|10|著作権表示|プリザンターの著作権表示です。クリックすると[株式会社インプリムのホームページ](https://implem.co.jp/)を表示します。|

### 画面項目の表示条件

|画面項目名|Community Edition|Pleasanter Extensionsのトライアル|Enterprise Edition|
|:---|:---|:---|:---|
|バージョン|○|○|○|
|ライセンス|○|○|○|
|Pleasanter Extensions トライアル|×|○|×|
|トライアル期限|×|○|×|
|商用ライセンスへの切り替え|○|○|×|
|ライセンス期限|×|×|○※1|
|使用者|×|×|○※1|
|ユーザ数上限|×|×|○※1|
|データベース使用量|○※2|○※2|○※2|
|著作権表示|○|○|○|

※1 [Version.json](../../setup/parameters/version-json.md)の設定で表示の有無を指定することができます。
※2 [特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)でログインした場合のみ確認することができます。

## 関連情報

[Pleasanter Extensionsトライアル](../../products-info/extensions-trial/index.md)
[パラメータ設定：Version.json](../../setup/parameters/version-json.md)
[プリザンターのバージョンを確認したい](../../FAQ/operations-and-maintenance/faq-version.md)
[DB使用量を確認したい](../../FAQ/operations-and-maintenance/faq-db-amount-to-use.md)
[AGPLに関するFAQ集](../../FAQ/license/faq-license-agpl.md)