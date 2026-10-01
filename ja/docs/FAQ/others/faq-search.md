---
title: 検索にヒットしない
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-search
translationKey: faq-search
shortname: フルテキスト検索
created: 2018-12-26
updated: 2024-04-29
---

## 回答

[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)の設定内容によって検索されない場合があります。設定に合わせた操作や設定の見直しを行ってください。

---

## 概要

検索にヒットしない場合、いくつかの原因が考えられますのでそれぞれの原因に対応した操作をお試しください。  

### 1. 検索の種類の設定により、検索ワードが検索対象にマッチしない場合

例）[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)の設定を「タイトルの部分一致」としているのに、タイトルにないキーワードを検索対象とした場合等  
検索の種類では設定毎に検索条件が異なります。ご利用状況に合わせ、以下の手順にて設定を行ってください。  
1. 検索を行いたいテーブルを選択してレコード一覧画面を表示する  
1. ナビゲーションメニューより[管理]-[テーブルの管理]を選択し、テーブルの管理画面を表示する  
1. [検索]タブを選択後、検索の設定にある[検索の種類]を変更して「更新」ボタンを押下する  
詳細は下記マニュアルを参照してください。
[テーブルの管理：検索：検索の設定：検索の種類](../../managers-guide/manage-table/search/table-management-search-type.md)  

### 2. 検索の種類の設定を「フルテキスト」に設定している場合

SQL Serverによるフルテキストインデックス作成時に単語の分かち書きが自動的に行われるため、登録されていない単語で検索を行うとヒットしません。詳しくは上述のマニュアルにある詳細項目「フルテキスト」を参照してください。  

### 3. フルテキスト検索を有効化していない環境で検索の種類の設定を「フルテキスト」に設定しており、CSVインポートしたレコードを検索した場合

検索の種類で「フルテキスト」以外を設定している場合、CSVインポートしたデータは検索インデックスが自動的に作成されません。そのため、インポート後に検索の種類を「フルテキスト」に設定した場合は検索になにもヒットしません。正しく検索するためには検索インデックスを再構築する必要があります。検索インデックスを再構築するには、以下の手順を行ってください。  
1. 検索を行いたいテーブルを選択してレコード一覧画面を表示する  
1. ナビゲーションメニューより[管理]-[テーブルの管理]を選択し、テーブルの管理画面を表示する  
1． [検索]タブを選択後、下部にある検索インデックスの再構築ボタンを押下する  
詳細につきましては、下記マニュアルを参照してください。
[テーブルの管理：検索：操作：検索インデックスの再構築](https://pleasanter.org/manual/table-management-rebuild-search-indexes)  

### 4. 途中でフルテキスト検索を有効化した環境で、フルテキスト検索を有効化する前のレコードを検索した場合

途中で[検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)をフルテキスト検索を有効化した場合、フルテキスト検索を有効化する前に登録したレコードについては検索インデックスには何も登録されていないため、検索になにもヒットしない状況となります。正しく検索するためには検索インデックスを再構築する必要があります。検索インデックスを再構築するには、上述の検索インデックスを再構築する手順を行ってください。  

## 関連情報

-   [テーブルの管理：フィルタ：検索の種類](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)
-   [テーブルの管理：検索：検索の設定：検索の種類](../../managers-guide/manage-table/search/table-management-search-type.md)
-   [テーブルの管理：検索：操作：検索インデックスの再構築](https://pleasanter.org/manual/table-management-rebuild-search-indexes)
