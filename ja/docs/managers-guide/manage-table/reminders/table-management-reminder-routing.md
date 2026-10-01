---
title: リマインダーの宛先を動的に設定する
category: リマインダー
order: '0'
status: ''
parts: ''
urlstring: table-management-reminder-routing
translationKey: table-management-reminder-routing
shortname: テーブルの管理：リマインダーの宛先を動的に設定する
created: 2025-06-17
updated: 2026-07-24
---

## 概要

リマインダーの宛先は、特定のメールアドレスだけではなく、担当者や管理者など任意の項目で指定されたメールアドレスを宛先できます。この設定は「アドレス」、「Cc」、「Bcc」の項目で利用可能です。

### 宛先に指定できる対象

|宛先の対象|挙動|
|---|---|
|固定のメールアドレス（example@example.com）|対象レコードの全てが指定した固定アドレスに送信されます。複数の固定アドレスを指定した場合には、全ての固定アドレスをTOとして送信します|
|担当者、管理者|対象レコードの担当者、管理者に指定されたユーザのメールアドレスに送信します|
|タイトル、内容、分類、説明|対象レコードのタイトル、内容、分類、説明に記載されたメールアドレスすべてに送信します。メールアドレスはカンマ区切りまたは改行区切りで指定することができます|

## 操作手順

レコードの関係者宛にリマインダーメールを送信するには、次のように設定します。

1. リマインダー種別でメールを選択します。
1. アドレスに[RelatedUsers]と入力します。
1. 「変更」ボタンをクリックします。
1. 管理画面の「更新」ボタンをクリックします。

この設定を行うと、レコードの作成者、更新者、管理者、担当者のいずれかに該当するユーザのメールアドレスに通知が行われます。

※ 対象者のチェックはレコードの更新履歴も含みます。
※ 対象者にメールアドレスが設定されていない場合には、通知は行われません。

## 設定例

リマインダーの宛先を下記のように設定した場合、下表に示すレコードの内容に合わせた宛先に動的にメールが送信されます。

```
example＠example.com, [担当者], [内容]
```

![宛先の設定内容と実際の送信先の対応を示す表](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/64ced18b5493403cade63ca46da7b32b.png)

- example＠example.com宛には、固定でリマインド通知のメールが送られます。
- レコードごとに登録された担当者、および内容に記載されているメールアドレスにもリマインド通知のメールが送信されます。
- URLの先頭部分には[Service.json](../../../setup/parameters/service-json.md)のAbsoluteUriに指定した内容が出力されます。

### 実際の設定例

以下、上記表に合わせて3つレコードを作成しています。

- レコード1： ID = 110071
- レコード2： ID = 110072
- レコード3： ID = 110073

![設定例で使用する3件のレコードの一覧](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/d98d1785bbd04522998e148165dae86e.png)

宛先の対象として、フリー項目「説明A」を「送信先アドレス」という名前で配置しています。レコード2(ID = 110072)では、「送信先アドレス」にユーザ([User1][User2])を指定しています。レコード3(ID = 110073)では、「送信先アドレス」にユーザ([User3])を指定しています。

![「送信先アドレス」にユーザを指定したレコードの編集画面](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/62a8ed3026b64907a205b1177def3707.png)

リマインダーの開始日時を「2024/05/22」と設定しています。

![開始日時を2024/05/22に設定したリマインダーの設定](https://pleasanter.org/files/images/ja/managers-guide/manage-table/reminders/assets/97705d3228ca4de1a316432f1e812d2b.png)

### 送信結果

リマインダーの宛先に設定している項目([担当者]、[送信先アドレス])に記載されているユーザに該当のレコードがリマインドされます。

Aさんに来たメール
```
2024/05/20 月 (2 日超過)
	要件定義)作業[非定型])ネットワーク要件の確認 --- Aさん (実施中)
	http://pleasanter.example.local/items/11071/edit

2024/05/17 金 (5 日超過)
	単体テスト)レビュー対応)単体テスト実施 --- Aさん (レビュー)
	http://pleasanter.example.local/items/11072/edit
```

user3さん(user3@example.com、[User3])に来たメール
```
2024/05/17 金 (5 日超過)
	単体テスト)レビュー対応)単体テスト実施 --- Aさん (レビュー)
	http://pleasanter.example.local/items/11072/edit
```

## ユーザ/組織/グループでの動的な宛先指定

リマインダー種別が「メール」の場合は、動的に宛先を指定することができます。ただし、無効となっているユーザ/組織/グループには通知されません。

### アドレスにIDを直接指定する

アドレスにユーザID/組織ID/グループIDを直接指定できます。ユーザ/組織/グループの名称は表示されませんので、指定するIDに誤りがないようにご注意ください。

設定例：

|No|アドレスの指定|説明|
|:--|:--|:--|
|1|[User1]|ユーザID:1のユーザに通知されます。|
|2|[Dept1]|組織ID:1に所属するユーザに通知されます。|
|3|[Group1]|グループID:1に所属するユーザ/組織に通知されます。|

### アドレスに分類項目を指定する

アドレスに「[ユーザの選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)」、「[組織の選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)」、「[グループの選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-groups.md)」を設定した分類項目を指定できます。レコード単位で設定されているユーザ/組織/グループで動的に宛先を変えたい場合に利用します。分類項目が「[複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)」の設定となっている場合は、複数選択のすべてに通知されます。

設定例：

|No|分類Aの表示名|分類Aの選択肢一覧|アドレスの指定|説明|
|:--|:--|:--|:--|:--|
|1|ユーザ|[[Users]]|[ユーザ]|対象レコードの分類Aに設定されたユーザに通知されます。|
|2|組織|[[Depts]]|[組織]|対象レコードの分類Aに設定された組織に所属するユーザに通知されます。|
|3|グループ|[[Groups]]|[グループ]|対象レコードの分類Aに設定されたグループIDに所属するユーザ/組織に通知されます。|

## 制限事項

- リマインダーメールのFROMはFixedFromで設定したメールアドレスとなります。
- [Mail.json](../../../setup/parameters/mail-json.md)のFixedFromを設定している場合、差出人の入力項目は非表示となります。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.3.9.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスに分類項目を指定する機能を追加|
|1.3.10.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスにIDを直接指定する機能を追加<br>リマインダー種別の指定機能を追加|