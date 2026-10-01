---
title: レコードの否定条件の検索（フィルタ）
category: テーブル機能
order: '51'
status: ''
parts: ''
urlstring: table-record-negative-search
translationKey: table-record-negative-search
shortname: 否定,否定条件のフィルタ
created: 2022-08-19
updated: 2024-12-19
---

## 概要

一覧画面の画面上部の[フィルタ](table-record-search.md)で「否定」のメニューを操作することで、特定の項目の否定条件でレコードを検索することができます。

-   複数の条件を組み合わせた検索が可能です。
-   [ビューの保存種別](../../../../managers-guide/manage-table/view/index.md)で「セッション」または「ユーザ」を設定している場合は、他の画面に遷移した後もフィルタに設定した条件が保持されます。
-   [カレンダー](../data-visualize/table-calendar.md)や[ガントチャート](../data-visualize/table-gantt-chart.md)などの画面においても、一覧画面と同様にフィルタが機能します。

![フィルタの「否定」メニューでレコードを絞り込む操作のアニメーション](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/cd2a89685e50477093b0a4b3b4a4aa30.gif)

## 制限事項

1.  [常に検索条件を要求する](../../../../managers-guide/manage-table/grid/table-management-always-request-search-condition.md)のチェックをオンにしている場合、フィルタを1つ以上設定しない限り、レコードは表示されません。
1.  [ビューの保存種別](../../../../managers-guide/manage-table/view/index.md)を「保存しない」に設定している場合、画面遷移を行うとフィルタがリセットされます。
1.  データベースにSQL Serverを使用する場合と、PostgreSQLを使用する場合では、フィルタ結果が異なる場合があります。SQL Serverでは`LIKE`句またはフルテキスト検索が使用され、PostgreSQLでは`ILIKE`句または`pg_trgm`によるフルテキスト検索が使用されるためです。
1.  [一覧](table-grid.md)画面のみで使用できる機能です。
1.  [ビュー](../../../../managers-guide/manage-table/view/index.md)や[サーバスクリプト](../../../../developers-guide/server-script/index.md)などでは使用できません。

## 前提条件

1.  検索対象となる項目が[フィルタ](../../../../managers-guide/manage-table/filter/index.md)で有効化されている必要があります。
1.  検索対象となる項目が[一覧](../../../../managers-guide/manage-table/grid/index.md)または[エディタ](../edit-records/table-editor.md)で有効化されている必要があります。
1.  [フィルタ](../../../../managers-guide/manage-table/filter/index.md)で有効化されていても、[一覧](../../../../managers-guide/manage-table/grid/index.md)および[エディタの設定](../../../../managers-guide/manage-table/editor/editor-settings/index.md)で無効化されている場合、フィルタは画面に表示されません。
1.  [フィルタ](../../../../managers-guide/manage-table/filter/index.md)で「[否定フィルタを使用する](../../../../managers-guide/manage-table/filter/table-management-filter-use-negative-filter.md)」のチェックをオンにする必要があります。

## 操作方法

1.  フィルタのラベルにカーソルを載せてください。
1.  ドロップダウンリストが表示されるので、「否定」または「肯定」を選択してください。

| 項目 | 説明                                                                                                                           |
| :--- | :----------------------------------------------------------------------------------------------------------------------------- |
| 否定 | 否定条件の検索を行います。<br>ラベルの先頭に否定条件の検索を示す:fontawesome-solid-exclamation-circle:アイコンが表示されます。 |
| 肯定 | 通常の検索を行います。<br>アイコンは非表示となります。                                                                         |

!!! tip
    各項目の否定条件は[フィルタ](table-record-search.md)の検索条件を**否定**した結果となります。ある項目に対する通常の検索結果をA、否定の検索結果をBとした場合に、「検索結果A＋検索結果B＝レコード全体」となるイメージです。
    
    通常の検索条件の詳細仕様は、以下を参照してください。

    [テーブル機能：レコードの検索（フィルタ）](table-record-search.md)

### 「リセット」ボタン

「リセット」をクリックすると、すべてのフィルタ条件が選択中の[ビュー](../../../../managers-guide/manage-table/view/index.md)の設定に戻ります。

### 「未完了」チェックボックス

「未完了」のチェックをオンにした状態で「否定」を選択することで、「未完了」<span class="pl-negative">**でない**</span>レコードを検索します。

### 「自分」チェックボックス

「自分」のチェックをオンにした状態で「否定」を選択することで、[管理者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)項目かつ[担当者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)項目がログインユーザ<span class="pl-negative">**でない**</span>レコードを検索します。

### 「期限が近い」チェックボックス

「期限が近い」のチェックをオンにした状態で「否定」を選択することで、「期限が近い」の範囲に<span class="pl-negative">**該当しない**</span>レコードを検索します。

!!! tip "あわせて確認"
    [テーブル機能：レコードの検索（フィルタ）：「期限が近い」チェックボックス](table-record-search.md)

### 「遅延」チェックボックス

「遅延」のチェックをオンにした状態で「否定」を選択することで、「遅延」<span class="pl-negative">**でない**</span>レコードを検索します。

!!! tip "あわせて確認"
    [テーブル機能：レコードの検索（フィルタ）：「遅延」チェックボックス](table-record-search.md)

### 「期限超過」チェックボックス

「期限超過」のチェックをオンにした状態で「否定」を選択することで、「期限超過」<span class="pl-negative">**でない**</span>レコードを検索します。

!!! tip "あわせて確認"
    [テーブル機能：レコードの検索（フィルタ）：「期限超過」チェックボックス](table-record-search.md)

### 「分類」「タイトル」「内容」「説明」テキストボックス

「分類」「タイトル」「内容」「説明」テキストボックスに文字列が入力されている状態で「否定」を選択することで、入力された文字列を<span class="pl-negative">**含まない**</span>レコードを検索します。

-   「分類」「タイトル」「内容」「説明」テキストボックスに半角空白または全角空白が入力されている状態で「否定」を選択した場合は、項目が未入力<span class="pl-negative">**でない**</span>レコードを検索します。

### 「分類」「状況」「管理者」「担当者」ドロップダウンリスト

「分類」「状況」「管理者」「担当者」ドロップダウンリストから選択肢のチェックをオンにした状態で「否定」を選択することで、チェック対象<span class="pl-negative">**以外の**</span>レコードを検索します。

-   複数の選択肢をチェックした状態で「否定」を選択した場合には<span class="pl-negative">**否定のAND条件**</span>で検索します。
-   `(未設定)`を選択した状態で「否定」を選択した場合は、選択肢が未設定<span class="pl-negative">**でない**</span>レコードを検索します。

### 「数値」「作業量」「進捗率」ドロップダウンリスト

「数値」「作業量」「進捗率」ドロップダウンリストから検索対象の数値の範囲を示す選択肢にチェックを入れた状態で「否定」を選択することで、チェック対象<span class="pl-negative">**以外の**</span>レコードを検索します。

-   複数の選択肢をチェックした状態で「否定」を選択した場合には<span class="pl-negative">**否定のAND条件**</span>で検索します。
-   `(未設定)`を選択した状態で「否定」を選択した場合は、数値が未入力<span class="pl-negative">**でない**</span>レコードを検索します。

### 「数値」「作業量」「進捗率」テキストボックス

[テーブルの管理](../../../../managers-guide/manage-table/index.md)の[フィルタ](../../../../managers-guide/manage-table/filter/index.md)タブで「数値」「作業量」「進捗率」項目を有効化し、「詳細設定」の「モード選択」で「範囲指定」を指定した場合、「開始」および「終了」欄に数値が入力されている状態で「否定」を選択することで、入力された数値の範囲に<span class="pl-negative">**該当しない**</span>レコードを検索します。

-   「開始」のみが入力されている状態で「否定」を選択した場合には、「開始」に入力された数値以上<span class="pl-negative">**でない**</span>（＝「開始」に入力された数値未満の）レコードを検索します。
-   「終了」のみが入力されている状態で「否定」を選択した場合には、「終了」に入力された数値以下<span class="pl-negative">**でない**</span>（＝「終了」に入力された数値を超過する）レコードを検索します。

### 「日付」「作成日時」「更新日時」ドロップダウンリスト

「日付」「作成日時」「更新日時」ドロップダウンリストから検索対象の日付の範囲を示す選択肢にチェックを入れた状態で「否定」を選択することで、チェック対象<span class="pl-negative">**以外の**</span>レコードを検索します。

-   複数の選択肢をチェックした状態で「否定」を選択した場合には<span class="pl-negative">**否定のAND条件**</span>で検索します。
-   `(未設定)`を選択した状態で「否定」を選択した場合は、日付が未入力<span class="pl-negative">**でない**</span>レコードを検索します。

### 「日付」「作成日時」「更新日時」テキストボックス

[テーブルの管理](../../../../managers-guide/manage-table/index.md)の[フィルタ](../../../../managers-guide/manage-table/filter/index.md)タブで「日付」「作成日時」「更新日時」項目を有効化し、「詳細設定」の「モード選択」で「範囲指定」を指定した場合、「開始」および「終了」欄に日付が入力されている状態で「否定」を選択することで、入力された日付の範囲に<span class="pl-negative">**該当しない**</span>レコードを検索します。

-   「開始」のみが入力されている状態で「否定」を選択した場合には、「開始」に入力された日付以上<span class="pl-negative">**でない**</span>（＝「開始」に入力された日付未満の）レコードを検索します。
-   「終了」のみが入力されている状態で「否定」を選択した場合には、「終了」に入力された日付以下<span class="pl-negative">**でない**</span>（＝「終了」に入力された日付を超過する）レコードを検索します。

### 「チェック」「ロック」チェックボックス

「チェック」「ロック」チェックボックスをオンにした状態で「否定」を選択することで、オン<span class="pl-negative">**でない**</span>レコードを検索します。

### 「チェック」「ロック」ドロップダウンリスト

[コントロール種別](../../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-check-filter-control-type.md)を「オンとオフ」に設定している場合、「オン」を選択した状態で「否定」を選択した場合はオン<span class="pl-negative">**でない**</span>レコードを検索します。「オフ」を選択した状態で「否定」を選択した場合はオフ<span class="pl-negative">**でない**</span>レコードを検索します。

### 添付ファイル項目

[添付ファイル](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)項目の検索機能はありません。

### 検索

[検索](../../../../managers-guide/manage-table/search/index.md)テキストボックスに文字列が入力された状態で「否定」を選択することで、入力した文字列を<span class="pl-negative">**含まない**</span>レコードを検索します。

-   検索キーワードを空白で区切って「否定」を選択した場合は、<span class="pl-negative">**否定のOR条件**</span>で検索します。
-   検索キーワード間に` or `を入力して「否定」を選択した場合は、<span class="pl-negative">**否定のAND条件**</span>で検索します。

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.3.18.0以降   | 機能追加 |

## 関連情報

-   [テーブル機能：レコードのエディタ画面](../edit-records/table-editor.md)
-   [テーブル機能：レコードのカレンダー表示](../data-visualize/table-calendar.md)
-   [テーブル機能：レコードのガントチャート表示](../data-visualize/table-gantt-chart.md)
-   [テーブル機能：レコードの一覧画面](table-grid.md)
-   [テーブル機能：レコードの検索（フィルタ）](table-record-search.md)
-   [テーブルの管理](../../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：エディタ：エディタの設定](../../../../managers-guide/manage-table/editor/editor-settings/index.md)
-   [テーブルの管理：ビュー](../../../../managers-guide/manage-table/view/index.md)
-   [テーブルの管理：フィルタ](../../../../managers-guide/manage-table/filter/index.md)
-   [テーブルの管理：フィルタ：チェック項目フィルタのコントロール種別](../../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-check-filter-control-type.md)
-   [テーブルの管理：検索](../../../../managers-guide/manage-table/search/index.md)
-   [テーブルの管理：一覧画面](../../../../managers-guide/manage-table/grid/index.md)
-   [テーブルの管理：一覧画面：常に検索条件を要求する](../../../../managers-guide/manage-table/grid/table-management-always-request-search-condition.md)
-   [テーブルの管理：項目：管理者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)
-   [テーブルの管理：項目：添付ファイル](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [開発者ガイド：サーバスクリプト](../../../../developers-guide/server-script/index.md)
