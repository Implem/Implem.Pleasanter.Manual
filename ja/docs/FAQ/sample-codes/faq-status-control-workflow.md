---
title: 項目の非表示や読取専用などの状態変更を「状況による制御」機能で実現する
category: FAQ：サンプルコード集
order: '6'
status: ''
parts: ''
urlstring: faq-status-control-workflow
translationKey: faq-status-control-workflow
shortname: 状況による制御
created: 2022-07-04
updated: 2025-01-30
---

## 説明

稟議申請などで用いられる承認ワークフローにおける項目の制御を[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)機能を用いて実現します。当ページでの説明は、承認欄の項目について起票後は[非表示](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)、申請後は[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)、承認／否認後は[読取専用](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)、保留後はレコードが読取専用となるように設定しています。状況による制御の設定方法は「[テーブルの管理：状況による制御](../../managers-guide/manage-table/control-by-status/index.md)」を参照してください。

## 概要

[プロセス](../../users-guide/hands-on/advanced/advanced-operations-process.md)機能と組み合わせて、承認ワークフローを作成します。処理のフローとしては以下となります。

1.  申請者がタイトル、起案日、申請者、金額、起案理由を入力してレコードを作成（起票）します。
1.  申請者が申請ボタンを押下してレコードを更新（申請）します。
1.  承認者が承認区分より「承認」または「否認」を選択、承認日、承認者を入力、承認／否認ボタンを押下してレコードを更新（承認／否認）します。
1.  承認者が保留とする場合は保留ボタンを押下してレコードを更新（保留）します。

※以下のFAQも合わせて参照してください。  
[FAQ：稟議申請などのワークフロー（承認プロセス）をプロセス機能で実現する](faq-process-workflow.md)

## 準備

[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)設定に必要なテーブル設定を行います。

※テーブルの設定は以下を参照してください。  
[テーブルの管理：エディタ](../../managers-guide/manage-table/editor/index.md)

![状況による制御で利用するテーブルのエディタ設定](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/79db4da2bea5402ead28bdffdce1b3dc.png)

| No  | 項目（表示名） | 利用項目      | 設定内容/説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --- | -------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 起案日         | 日付A         | エディタの設定で[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)とします。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 2   | 申請者         | 担当者        | エディタの設定で[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)とします。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 3   | ステータス     | 状況          | エディタの設定で[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に”起票,申請,承認／否認,保留”を設定、既定値を”起票”に設定します。また、[読取専用](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)に設定します。[^1]                                                                                                                                                                                                                                                                                                                          |
| 4   | 金額           | 数値A         | エディタの設定で[書式](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-format.md)を”通貨”に設定します。また、[数値フィルタのモード選択](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-num-filter-mode.md)で”範囲指定”に設定します。                                                                                                                                                                                                                                                                                                                                                                                                        |
| 5   | 起案理由       | 説明A         | エディタの設定で[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)とします。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 6   | 添付資料       | 添付ファイルA | 任意での入力項目（デフォルトの設定）とします。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 7   | 承認区分       | 分類A         | エディタの設定で[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に”承認,否認”を設定します。また、[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)で起票後は[非表示](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)、申請後は[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)、承認／否認後は[読取専用](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)とします。 |
| 8   | 承認日         | 日付B         | [状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)で起票後は[非表示](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)、申請後は[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)、承認／否認後は[読取専用](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)とします。                                                                                                                                                                                                     |
| 9   | 承認者         | 分類B         | エディタの設定で[選択肢一覧](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)に[[Users]]を設定します。[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)で起票後は[非表示](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)、申請後は[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)、承認／否認後は[読取専用](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)とします。         |

[^1]: 選択肢一覧の設定例は以下のとおりです。

``` text linenums="1"
100,起票,起,status-new
200,申請,申,status-inprogress
900,承認／否認,承,status-closed
910,保留,留,status-rejected
```

## 状況による制御の設定

以下のとおり、4つの[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)を設定します。

![設定する4つの状況による制御の一覧](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/cc4983763fe646b39139c89329803cd5.png)

| No  | 項目（表示名） | 起票後 | 申請後   | 承認／否認後 |
| --- | -------------- | ------ | -------- | ------------ |
| 1   | 承認区分       | 非表示 | 入力必須 | 読取専用     |
| 2   | 承認日         | 非表示 | 入力必須 | 読取専用     |
| 3   | 承認者         | 非表示 | 入力必須 | 読取専用     |

## 稟議申請の流れ

1.  稟議申請を作成する。（ステータス起票）
1.  申請者が申請プロセスを実施（ステータス起票→申請）
1.  承認者が承認／否認プロセスを実施（ステータス申請→承認／否認）
1.  承認者が保留プロセスを実施（ステータス申請→承認）

### 起票時（新規作成時）

[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定でステータスが「起票」の場合は承認欄の各項目が[非表示](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)となります。入力が必要な項目のみを表示し、承認欄の誤った入力を防止することができます。
![新規作成時の編集画面。承認欄の項目が非表示になっている](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/55ab8ccca5a041d69fad5e3b8e1b9c7c.png)

### 起票後（新規作成後）

[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定でステータスが「起票」の場合は承認欄の各項目が[非表示](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)となります。入力が必要な項目のみを表示し、承認欄の誤った入力を防止することができます。
![起票後の編集画面。承認欄の項目が非表示になっている](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/107ce05b5f4243c2ab3bba53c2bf64dc.png)

### 申請後

[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定でステータスが「申請」の場合は承認欄の各項目が[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)となります。承認欄の入力漏れを防止することができます。
![申請後の編集画面。承認欄の項目が入力必須になっている](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/1e066d3df6ef445b9ee7b6c80597ac83.png)

### 承認／否認後

[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定でステータスが「承認／否認」の場合は承認欄の各項目が[読取専用](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)となります。承認欄の誤った更新を防止することができます。
![承認／否認後の編集画面。承認欄の項目が読取専用になっている](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/1dd9382d5f4149ce8b6fc3f0e2fa2489.png)  

### 保留後

[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)の設定でステータスが「保留」の場合はレコードが読取専用となります。保留後のレコード更新を防止することができます。
![保留後の編集画面。レコード全体が読取専用になっている](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/d95dcb2bead04015b17b452af838da32.png)
