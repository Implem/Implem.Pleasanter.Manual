---
title: 選択肢によるフィルタを行ったが、選択した項目以外のレコードが検索結果に表示する
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-invalid-search-results-choices
translationKey: faq-invalid-search-results-choices
shortname: ''
created: 2024-07-04
updated: 2024-07-04
---

## 回答

[テーブルの管理](../../managers-guide/manage-table/index.md)－[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)にて該当項目の[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)を「完全一致」に設定してください。

---

## 概要

他テーブルや組織、ユーザを選択肢として設定した分類項目において、一覧画面のフィルタにて項目の選択肢によるフィルタを行った際に、選択した項目以外のレコードが検索結果に表示する場合があります。

### 事例

1. 分類Aの選択肢でユーザマスタを指定（[[Users]]）
![分類Aの選択肢一覧にユーザマスタを指定した設定](https://pleasanter.org/files/images/ja/FAQ/grid/assets/1c60bf110c484feba28501b232105ecd.png)

2. ユーザマスタは以下のような内容で登録
"テナント管理者"のIDは2、"中村 隆"のIDは12で登録。
![ユーザマスタの一覧。テナント管理者と中村 隆が登録されている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/e3cef0712f4a4211837e9c347f4562df.png)

3. フィルタで何も設定しない場合はレコードが3件表示
![フィルタを設定していない状態の一覧画面。レコードが3件表示されている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/4d2ca1d273a043d9b25212db8728ed80.png)

4. フィルタにて分類Aで"テナント管理者"を選択
![フィルタの分類Aで「テナント管理者」を選んだ状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/9429c50d8b584385aedbdd7ea094f485.png)

5. 検索結果に"テナント管理者"の他に"中村 隆"が含まれる
![検索結果に「テナント管理者」以外に「中村 隆」も表示されている状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/db0eea39b0794c7e9123cd4a423d5c26.png)

6. [テーブルの管理](../../managers-guide/manage-table/index.md)－[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)にて分類Aの[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)は「部分一致」になっている
![フィルタの設定。分類Aの検索の種類が「部分一致」になっている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/a409245ffec747ffb7ab885808406280.png)

これは他テーブルや組織、ユーザを選択肢として設定した場合、表示上はレコードのタイトルや組織名、ユーザ名で選択しますが、データ上はレコードID（組織ID、ユーザID）での検索になるためです。上記例ですと選択した"テナント管理者"のユーザID「2」でレコードを検索しますが、検索の種類が「部分一致」であるため、ユーザIDに「2」が含まれるレコードが検索対象となるため、"テナント管理者"の他に"中村 隆"も検索結果として表示します。

### 解決方法

[テーブルの管理](../../managers-guide/manage-table/index.md)－[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)にて該当項目の[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)を「完全一致」に設定することで、チェックした選択肢だけを検索結果として表示します。
1. [検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)を「完全一致」に設定
![分類Aの検索の種類を「完全一致」に設定したところ](https://pleasanter.org/files/images/ja/FAQ/grid/assets/493d530ec7814fd6bcc9a0b62f4a487c.png)

1. チェックした選択肢だけが検索結果に表示
![完全一致にした後の検索結果。選んだ選択肢のレコードだけが表示されている](https://pleasanter.org/files/images/ja/FAQ/grid/assets/b59a53bdfadd46dfa9a74a3e87762a8b.png)

## 関連情報

-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：フィルタ：検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)