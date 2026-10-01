---
title: 更新時に必ずコメントを入力させたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-process-comment-required
translationKey: faq-process-comment-required
shortname: FAQコメント必須化,プロセス
created: 2022-09-05
updated: 2024-07-12
---

## 回答

[プロセス](../../users-guide/hands-on/advanced/advanced-operations-process.md)と[自動バージョンアップ](../../managers-guide/manage-table/editor/automatic-version-upgrade/index.md)を組み合わせて使用します。

### プロセス

1. [コメント](../../users-guide/common/comment.md)の代わりに[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)をコメント入力欄として使用し、[入力検証](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/input-validation/index.md)で[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)にチェックする
1. 登録済みのコメントを残すために[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)をコメント履歴として使用し、「データの変更」でコメント入力欄からコメント履歴欄に値をコピーする設定を入力
1. 通常の「登録」、「更新」ボタンの置き換えとするため、実行種別を「作成または更新」とする。

### 自動バージョンアップ

1. 「常時」に設定する

---

## 概要

必須の制御を持たないテーブルの[コメント](../../users-guide/common/comment.md)項目に代えて、説明項目を 2 つ利用して、更新時に必須の制御をする例を紹介します。

## 想定するユースケース

プリザンターは通知機能に、変更項目を列挙する機能があります。
しかしながら、管理項目が多い、添付ファイルの内容が変更されたといった場合について、概要の可視化が困難な場合も想定されます。
変更を概観として把握したい用途においては、どのような目的で変更したかコメントを求めることが効果的です。

一方、システムにある[コメント](../../users-guide/common/comment.md)は必須の制御を持たないため、必ず変更内容のコメントを求めたい、といった場合に本事例のような対応が有効となります。

## 利用する項目および設定

- 利用する項目
  - 1 つ目は「編集内容」として、必須の制御を行い、毎回入力を求める入力欄として機能させます。
  - 2 つ目は「編集履歴」として、入力を保持する目的で利用します。
- 利用するプロセス機能
  - 「編集内容」を、更新ボタンを押した際に、毎回「編集履歴」に転記します。
    - あわせて、更新ボタンを押した人
  - 「編集内容」をクリアします。
    - クリアすることで、毎回必須の制御を働かせることができます。

オプショナルな内容とはなりますが、以下の例では分類項目および日付項目を利用して、更新者ならびに更新日時の情報を自動的に記録する設定としています。

## 項目の設定

### 「編集内容」項目

![「編集内容」項目の詳細設定。入力必須にチェックする](https://pleasanter.org/files/images/ja/FAQ/editor/assets/2e42b919da22469bbda7fb6b807aa764.png)

作成および更新で必ず入力を求めるため[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)にチェックします。

この例では「説明 A」を利用しています。[内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)や選択肢のない[分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)型項目を利用することも可能です。

### 「編集履歴」項目

![「編集履歴」項目の詳細設定。読取専用にチェックする](https://pleasanter.org/files/images/ja/FAQ/editor/assets/1ddba3383331484baaeb0d98c8f1a32a.png)

読取専用にチェックします。この項目はユーザの編集を想定しないためです。

履歴を残すため、複数行の項目である必要があります。他で利用していなければ[内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)を利用することも可能です。

### 「担当者」項目

オプションの設定です。
履歴に更新者を記録するために、「担当者」項目を利用します。

![「担当者」項目の詳細設定。読取専用と非表示にチェックする](https://pleasanter.org/files/images/ja/FAQ/editor/assets/354041eb65134dee85b83919651e8593.png)

ユーザを自動設定するため、読取専用とします。本例ではすぐにクリアするため、非表示をチェックしています。
最後に更新したユーザを残すことも可能です。この場合、プロセスの設定で担当者を空欄にする設定を行わないようにします。

### 「編集時刻」項目

オプションの設定です。
履歴に更新時刻を記録するために、「日付 A」項目を利用します。

![「編集時刻」に使う日付A項目の詳細設定。書式を指定する](https://pleasanter.org/files/images/ja/FAQ/editor/assets/5a7ca8966d424b1f9432639f7fdc65bc.png)

読取専用および非表示としています。
ユーザが入力することはなく、プロセスによって更新日を設定し、すぐにクリアします。

履歴に残したい時刻の粒度に応じて書式を設定します。

## プロセスの設定

1 つのルールを設定します。

![プロセスにルールを1つ登録した状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/dce12277a15c4efaa8524fbf9089e214.png)

### 全般

![プロセス設定の全般タブ。実行種別を「作成または更新」にする](https://pleasanter.org/files/images/ja/FAQ/editor/assets/db8512c4c9ca47c69c7c1c76c8f6d75e.png)

名称および表示名は、機能を表現する名前とします。
表示名は、ボタンを追加するときのボタンキャプションとなります。本例では特段の意味を持ちません。

画面種別は編集のままとし、現在の状況および変更後の状況を「*」とします。
状況によらず動作させ、かつ状況を変更しないためです。

説明は実現したい機能を説明として記述します。
機能要件ではありません。

実行種別を「作成または更新」とします。既存の「作成」および「更新」ボタンで発動させる際の設定です。

### データ変更

![プロセス設定のデータ変更タブ。ID 1 から 6 までの変更内容が並ぶ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/06887b07eeca4bfeae50086cea0782a1.png)

- ID 1, 2 は操作しているユーザおよび操作時刻を、自動的に設定するための設定となります。
- ID 3 では、編集履歴の内容に、担当者および編集時刻、編集内容を追記します。角カッコを使うことでデータ項目を転記できます。また、その項目自身を含めることで、追記が可能です。下図も参照してください。
  ![編集履歴に担当者・編集時刻・編集内容を追記する設定の例](https://pleasanter.org/files/images/ja/FAQ/editor/assets/604e7b6f9977431090ec7346bf507549.png)
- ID 4 では、編集内容をクリアします。変更種別を「値の入力」にしたうえで、値を空白とすると、クリア可能です。これにより、入力がクリアされ、次回入力時に再度必須の制御を働かせることが可能です。
- ID 5, 6 は操作しているユーザおよび操作時刻の情報をクリアして引き継がない設定となります。更新者、更新日時の意味として保持する場合この設定を削除できます。

## 動作例

作成および更新を行ない、その次の更新を行う際に必須の制御がかかった状態は下図のとおりです。

![次の更新を行う際に「編集内容」が入力必須になっている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/0eb6d7fdbafe478dace728e7ee688375.png)

本例では[自動バージョンアップ](../../managers-guide/manage-table/editor/automatic-version-upgrade/index.md)を「常時」としておりますため、次のように「編集履歴」に対応付く[変更履歴](../../users-guide/table/record-authoring/edit-records/table-record-history-delete.md)が確認できます。

![「編集履歴」に対応付く変更履歴が記録されている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/bcdc983a7a16403192799227a12bd139.png)

## 関連情報

-   [応用編：プロセスと状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [テーブルの管理：エディタ：自動バージョンアップ](../../managers-guide/manage-table/editor/automatic-version-upgrade/index.md)
-   [共通機能：コメントを追加](../../users-guide/common/comment.md)
-   [テーブルの管理：項目：説明](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力検証](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/input-validation/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブルの管理：項目：内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [自動バージョンアップ](../../managers-guide/manage-table/editor/automatic-version-upgrade/index.md)
-   [テーブル機能：レコードの変更履歴を削除](../../users-guide/table/record-authoring/edit-records/table-record-history-delete.md)
