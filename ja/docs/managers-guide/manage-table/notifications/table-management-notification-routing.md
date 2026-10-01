---
title: 通知 - メール通知の宛先を動的に設定する
category: 通知
order: '0'
status: ''
parts: ''
urlstring: table-management-notification-routing
translationKey: table-management-notification-routing
shortname: ''
created: 2025-06-18
updated: 2025-10-29
---

## 概要

メール通知の宛先は特定のメールアドレスだけではなく、担当者や管理者など任意の項目で指定されたメールアドレスを宛先できます。この設定は「アドレス」、「Cc」、「Bcc」の項目で利用可能です。

## 制限事項

一括更新による通知の場合、固定のメールアドレスにのみ通知可能です。[RelatedUsers]や[担当者]などは使用できません。

## 宛先に指定できる対象

|対象|挙動|
|---|---|
|固定のメールアドレス（example@example.com）|対象レコードの全てが指定した固定アドレスに送信されます。複数の固定アドレスを指定した場合には、全ての固定アドレスをTOとして送信します|
|担当者、管理者|対象レコードの担当者、管理者に指定されたユーザのメールアドレスに送信します|
|タイトル、内容、分類、説明|対象レコードのタイトル、内容、分類、説明に記載されたメールアドレスすべてに送信します。メールアドレスはカンマ区切りまたは改行区切りで指定することができます|

## 操作手順

レコードの関係者宛にメールを通知するには、次のように設定します。

1. 通知種別でメールを選択します。
1. アドレスに[RelatedUsers]と入力します。
1. 「変更」ボタンをクリックします。
1. 管理画面の「更新」ボタンをクリックします。

この設定を行うと、レコードの作成者、更新者、管理者、担当者のいずれかに該当するユーザのメールアドレスに通知が行われます。

※ 対象者のチェックはレコードの更新履歴も含みます。
※ 対象者にメールアドレスが設定されていない場合には、通知は行われません。

## 設定例

通知の宛先を下記のように設定した場合、下表に示すレコードの内容に合わせた宛先に動的にメールが送信されます。

```text
example＠example.com, [担当者], [内容]
```

![宛先の設定内容と実際の送信先の対応を示す表](https://pleasanter.org/files/images/ja/managers-guide/manage-table/notifications/assets/64ced18b5493403cade63ca46da7b32b.png)

![動的な宛先を設定した通知の設定例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/notifications/assets/dd4a6cd0fd6a424288ab645f558e962c.png)

- example＠example.com宛には固定で通知が送信されます。
- レコードごとに登録された担当者、および内容にされたメールアドレスにも通知メールが送信されます。  

## ユーザ/組織/グループでの動的な宛先指定

通知種別が「メール」の場合は、動的に宛先を指定できます。ただし、無効となっているユーザ/組織/グループには通知されません。

### アドレスにIDを直接指定する

アドレスにユーザID/組織ID/グループIDを直接指定できます。ユーザ/組織/グループの名称は表示されませんので、指定するIDに誤りがないようにご注意ください。

設定例：

|No|アドレスの指定|説明|
|:--|:--|:--|
|1|[User1]|ユーザID:1のユーザに通知されます。|
|2|[Dept1]|組織ID:1に所属するユーザに通知されます。|
|3|[Group1]|グループID:1に所属するユーザ/組織に通知されます。|

### アドレスに分類項目を指定する

アドレスに[ユーザの選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)、[組織の選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)、[グループの選択肢一覧](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-groups.md)を設定した分類項目を指定できます。レコード単位で設定されているユーザ/組織/グループで動的に宛先を変えたい場合に利用します。分類項目が[複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)の設定となっている場合は、複数選択のすべてに通知されます。

設定例：

|No|分類Aの表示名|分類Aの選択肢一覧|アドレスの指定|説明|
|:--|:--|:--|:--|:--|
|1|ユーザ|[[Users]]|[ユーザ]|対象レコードの分類Aに設定されたユーザに通知されます。|
|2|組織|[[Depts]]|[組織]|対象レコードの分類Aに設定された組織に所属するユーザに通知されます。|
|3|グループ|[[Groups]]|[グループ]|対象レコードの分類Aに設定されたグループIDに所属するユーザ/組織に通知されます。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.26.0 以降|作成後／更新後／削除後の通知タイミングを追加|
|1.3.2.0 以降|コピー後／一括更新後／一括削除後の通知タイミングを追加|
|1.3.3.0 以降|インポート後の通知タイミングを追加|
|1.3.9.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスに分類項目を指定する機能を追加|
|1.3.10.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスにIDを直接指定する機能を追加|
|1.3.17.0 以降|HTTPクライアントを利用した通知機能を追加|
|1.4.8.0 以降|DiffMatchPatch形式で値の差分を表示する機能を追加|
|1.4.10.0 以降|メールの宛先にCc、Bccを追加|

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：グループ](../editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-groups.md)
-   [テーブルの管理：エディタ：項目の詳細設定：複数選択](../editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)