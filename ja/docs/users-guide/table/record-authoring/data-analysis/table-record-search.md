---
title: レコードの検索（フィルタ）
category: テーブル機能
order: '51'
status: ''
parts: ''
urlstring: table-record-search
translationKey: table-record-search
shortname: フィルタ
created: 2019-04-30
updated: 2024-09-12
---

## 概要

[一覧](table-grid.md)画面上部の**フィルタ**を操作することで、ユーザが指定した条件を満たすレコードを検索できます。

-   複数の条件を組み合わせた検索が可能です。
-   [ビューの保存種別](../../../../managers-guide/manage-table/view/index.md)で「セッション」または「ユーザ」を設定している場合は、他の画面に遷移した後もフィルタに設定した条件が保持されます。
-   [カレンダー](../data-visualize/table-calendar.md)や[ガントチャート](../data-visualize/table-gantt-chart.md)などの画面においても、一覧画面と同様にフィルタが機能します。

![一覧画面上部のフィルタでレコードを絞り込む操作](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/0c058e70fef749f59fc9b33f3b60515b.gif)

## 制限事項

1.  [常に検索条件を要求する](../../../../managers-guide/manage-table/grid/table-management-always-request-search-condition.md)のチェックをオンにしている場合、フィルタを1つ以上設定しない限り、レコードは表示されません。
1.  [ビューの保存種別](../../../../managers-guide/manage-table/view/index.md)を「保存しない」に設定している場合、画面遷移を行うとフィルタが[リセット](#_6)されます。
1.  データベースにSQL Serverを使用する場合と、PostgreSQLを使用する場合では、フィルタ結果が異なる場合があります。SQL Serverでは`LIKE`句またはフルテキスト検索が使用され、PostgreSQLでは`ILIKE`句または`pg_trgm`によるフルテキスト検索が使用されるためです。
1.  一覧画面で二階層以上先のリンクしているテーブルの値でフィルタを行う場合は、[検索機能を使う](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)を有効化する必要があります。

## 前提条件

1.  検索対象となる項目が[フィルタ](../../../../managers-guide/manage-table/filter/index.md)で有効化されている必要があります。
1.  検索対象となる項目が[一覧](../../../../managers-guide/manage-table/grid/index.md)または[エディタ](../edit-records/table-editor.md)で有効化されている必要があります。
1.  [フィルタ](../../../../managers-guide/manage-table/filter/index.md)で有効化されていても、[一覧](../../../../managers-guide/manage-table/grid/index.md)および[エディタ](../edit-records/table-editor.md)で無効化されている場合、フィルタは画面に表示されません。

## 操作方法

### フィルタの折りたたみ・展開

フィルタ領域の左上にある×ボタンをクリックすると、フィルタ領域が折りたたまれて表示します。  
もう一度クリックすると、元の状態に展開します。

### 「リセット」ボタン

「リセット」をクリックすると、すべてのフィルタ条件が選択中の[ビュー](../../../../managers-guide/manage-table/view/index.md)の設定に戻ります。

### 「未完了」チェックボックス

「未完了」のチェックをオンにすると、未完了と判定されたレコードを検索します。

-   [状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目に900未満の選択肢が登録されている場合（標準設定では「完了」と「保留」**以外**の選択肢が登録されている場合）、「未完了」と判定します。
-   [状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目が[一覧](../../../../managers-guide/manage-table/grid/index.md)および[エディタ](../edit-records/table-editor.md)で無効化されている場合、「未完了」チェックボックスはフィルタに表示されません。

### 「自分」チェックボックス

「自分」のチェックをオンにすると、[管理者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)項目または[担当者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)項目にログインユーザが選択されているレコードを検索します。

-   [管理者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)項目および[担当者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)項目がいずれも[一覧](../../../../managers-guide/manage-table/grid/index.md)および[エディタ](../edit-records/table-editor.md)で無効化されている場合、「自分」チェックボックスはフィルタに表示されません。

### 「期限が近い」チェックボックス

「期限が近い」のチェックをオンにすると、[完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)項目の日時を基準として、[「期限が近い」の日数（前）](../../../../managers-guide/manage-table/filter/table-management-filter-near-completion-time.md)～[「期限が近い」の日数（後）](../../../../managers-guide/manage-table/filter/table-management-filter-near-completion-time.md)の範囲に該当するレコードを検索します。

-   「期限が近い」フィルタは[期限付きテーブル](../../index.md)でのみ利用できます。
-   標準では、[完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)項目の日時の7日前が[「期限が近い」の日数（前）](../../../../managers-guide/manage-table/filter/table-management-filter-near-completion-time.md)、[完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)項目の日時の7日後が[「期限が近い」の日数（後）](../../../../managers-guide/manage-table/filter/table-management-filter-near-completion-time.md)です。
-   [完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)項目が[一覧](../../../../managers-guide/manage-table/grid/index.md)および[エディタ](../edit-records/table-editor.md)で無効化されている場合、「期限が近い」チェックボックスはフィルタに表示されません。

### 「遅延」チェックボックス

「遅延」のチェックをオンにすると、遅延と判定されたレコードを検索します。

-   [状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目が未完了かつスケジュール消化率に比べて進捗状況が低いレコードを「遅延」と判定します。
-   「遅延」フィルタは[期限付きテーブル](../../index.md)でのみ利用できます。
-   「遅延」の条件は以下のとおりです。

    1.  未完了（[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目で設定した番号が900未満）
    1.  現在の時刻が[完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)項目の日時を過ぎた場合に、進捗率が100％未満の場合
    1.  進捗状況がスケジュール消化率を満たしていない場合  

        進捗状況＝（現在時刻－開始項目[^1]）／（完了項目－開始項目[^1]）×100

[^1]: 開始項目が未入力の場合は、[作成日時](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-created-time.md)項目が使われます。

### 「期限超過」チェックボックス

[期限超過](../../../../managers-guide/manage-table/filter/table-management-filter-use-overdue-filter.md)のチェックをオンにすると、[状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)項目に900未満の選択肢が登録され、かつ[完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)項目に設定された日時を超過したレコードを検索します。

-   [期限超過](../../../../managers-guide/manage-table/filter/table-management-filter-use-overdue-filter.md)フィルタは[期限付きテーブル](../../index.md)でのみ利用できます。

### 「サイト」ドロップダウンリスト

「サイト」ドロップダウンリストに表示されたテーブルの名称のチェックをオンにすると、オンにしたテーブルで[検索結果一覧](table-grid.md)に表示されているデータが絞り込まれます。

-   「サイト」ドロップダウンリストは[テーブルの管理](../../../../managers-guide/manage-table/index.md)の[フィルタ](../../../../managers-guide/manage-table/filter/index.md)タブで「サイト」項目を有効化し、「モード選択」に「既定」を指定した場合に表示されます。
-   テーブルを[サイト統合](../edit-records/table-site-integration.md)している場合、統合しているすべてのテーブルの名称が「サイト」ドロップダウンリストに表示されます。
-   テーブルを[サイト統合](../edit-records/table-site-integration.md)していない場合、「サイト」ドロップダウンリストには何も表示されません。

!!! tip
    テーブルをサイト統合する手順は、[サイト統合](../edit-records/table-site-integration.md)を参照してください。

### 「サイト」テキストボックス

「サイト」テキストボックスで範囲を指定すると、登録されているテーブルのサイトIDで[検索結果一覧](table-grid.md)に表示されているデータが絞り込まれます。

-   「サイト」テキストボックスは[テーブルの管理](../../../../managers-guide/manage-table/index.md)の[フィルタ](../../../../managers-guide/manage-table/filter/index.md)タブで「サイト」項目を有効化し、「モード選択」に「範囲指定」を指定した場合に表示されます。
-   「サイト」テキストボックスをクリックすると、数値の範囲を入力するダイアログが開きます。「開始」と「終了」に数値を入力し、「OK」をクリックしてください。
-   「開始」のみまたは「終了」のみを入力することが可能です。
-   複数のテーブルを[サイト統合](../edit-records/table-site-integration.md)している場合、目的のテーブルに登録されているデータのみに絞り込んで[検索結果一覧](table-grid.md)に表示することができます。

!!! tip
    テーブルをサイト統合する手順は、[サイト統合](../edit-records/table-site-integration.md)を参照してください。

### 「分類」「タイトル」「内容」「説明」テキストボックス

「分類」「タイトル」「内容」「説明」テキストボックスでは、入力した文字列によるキーワード検索が可能です。

-   [分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)項目では、選択肢がない場合、テキストボックスでの検索が可能です。
-   検索キーワードはアルファベットの大文字・小文字を区別しません。
-   検索キーワードを空白で区切るとAND検索します。
-   OR検索には対応していません。
-   項目が未入力のレコードを検索したい場合は、テキストボックスに半角空白または全角空白を入力し、++enter++を押下してください。

### 「分類」「状況」「管理者」「担当者」ドロップダウンリスト

「分類」「状況」「管理者」「担当者」ドロップダウンリストを開き、選択肢のチェックをオンにすることで検索が可能です。

-   複数の選択肢のチェックをオンにした場合はOR条件で検索します。
-   `(未設定)`を選択すると、選択肢が設定されていないレコードを検索します。
-   「自分」を選択すると、ログインしているユーザーが設定されているレコードを検索します。
-   [項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の詳細設定で[検索機能を使う](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)のチェックをオンにしている場合は、ドロップダウンリストをクリックした際に検索ダイアログが表示されます。検索ダイアログから選択肢を選択してください。

    ![検索ダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/data-analysis/assets/7962d5cc9abe47d793f7f008aa558f15.png)

-   検索ダイアログの操作は[検索機能を使う](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)の「複数選択が有効な場合」と同様です。

### 「数値」「作業量」「進捗率」ドロップダウンリスト

「数値」「作業量」「進捗率」ドロップダウンリストを開き、数値の範囲を示す選択肢のチェックをオンにすることで検索が可能です。

-   複数の選択肢をチェックした場合にはOR条件で検索します。
-   `(未設定)`を選択すると、数値が未入力のレコードを検索します。

### 「数値」「作業量」「進捗率」テキストボックス

「数値」「作業量」「進捗率」テキストボックスをクリックすると数値の範囲を入力するダイアログが開くので、「開始」および「終了」欄に数値を入力し、「OK」をクリックしてください。

-   「数値」「作業量」「進捗率」テキストボックスは、[テーブルの管理](../../../../managers-guide/manage-table/index.md)の[フィルタ](../../../../managers-guide/manage-table/filter/index.md)タブで「数値」「作業量」「進捗率」項目を有効化し、「詳細設定」の「モード選択」で「範囲指定」を指定した場合に表示されます。
-   「開始」のみまたは「終了」のみを入力することも可能です。

### 「日付」「作成日時」「更新日時」ドロップダウンリスト

「日付」「作成日時」「更新日時」ドロップダウンリストを開き、検索対象の日付の範囲を示す選択肢にチェックを入れることで検索が可能です。

-   複数の選択肢をチェックした場合にはOR条件で検索します。
-   `(未設定)`を選択すると、日付が未入力のレコードを検索します。

### 「日付」「作成日時」「更新日時」テキストボックス

「日付」「作成日時」「更新日時」テキストボックスをクリックすると日付の範囲を入力するダイアログが開くので、「開始」および「終了」欄に数値を入力し、「OK」をクリックしてください。

-   「日付」「作成日時」「更新日時」テキストボックスは、[テーブルの管理](../../../../managers-guide/manage-table/index.md)の[フィルタ](../../../../managers-guide/manage-table/filter/index.md)タブで「日付」「作成日時」「更新日時」項目を有効化し、「詳細設定」の「モード選択」で「範囲指定」を指定した場合に表示されます。
-   「開始」のみまたは「終了」のみを入力することも可能です。
-   [エディタの書式](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)が「年月日」に設定されている場合、「終了」に指定した日付の23:59:59.997時までの範囲を抽出します。

### 「チェック」「ロック」チェックボックス

「チェック」をオンにすることで、チェックが入っているレコードを検索できます。「ロック」をオンにすることで、ロックされているレコードを検索できます。

### 「チェック」「ロック」ドロップダウンリスト

[コントロール種別](../../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-check-filter-control-type.md)を「オンとオフ」に設定している場合、「オン」を選択するとチェックが入っているレコードを、「オフ」を選択するとチェックが入っていないレコードを検索できます。

### 添付ファイル

[添付ファイル](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)項目の検索機能はありません。

### 検索

[検索](../../../../managers-guide/manage-table/search/index.md)テキストボックスに入力した文字列によりサイト内のレコードを検索します。

-   項目の詳細設定で[フルテキストの種類](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-full-text-type.md)が設定されている項目の文字列が検索対象となります。
-   検索キーワードはアルファベットの大文字・小文字を区別しません。
-   検索キーワードを空白で区切るとAND検索します。
-   検索キーワード間に`or`を入力した場合にはOR検索します。
-   「検索の設定」で選択された[検索の種類](../../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)により検索の動作は異なります。

## カスタマイズ

フィルタの表示内容やフィルタで使用する機能は、[テーブルの管理](../../../../managers-guide/manage-table/index.md)でカスタマイズできます。  
詳細は以下のページを参照してください。

-   [テーブルの管理：フィルタ](../../../../managers-guide/manage-table/filter/index.md)
-   [テーブルの管理：フィルタ：項目連携](../../../../managers-guide/manage-table/filter/table-management-filter-column-relation.md)

## 関連情報

-   [テーブル機能](../../index.md)
-   [テーブル機能：サイト統合](../edit-records/table-site-integration.md)
-   [テーブル機能：レコードのエディタ画面](../edit-records/table-editor.md)
-   [テーブル機能：レコードのカレンダー表示](../data-visualize/table-calendar.md)
-   [テーブル機能：レコードのガントチャート表示](../data-visualize/table-gantt-chart.md)
-   [テーブル機能：レコードの一覧画面](table-grid.md)
-   [テーブルの管理：ビュー](../../../../managers-guide/manage-table/view/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：エディタの書式](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-editor-format.md)
-   [テーブルの管理：エディタ：項目の詳細設定：検索機能を使う](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-use-search.md)
-   [テーブルの管理：エディタ：項目の詳細設定：フルテキストの種類](../../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-full-text-type.md)
-   [テーブルの管理：フィルタ](../../../../managers-guide/manage-table/filter/index.md)
-   [テーブルの管理：フィルタ：「期限が近い」の日数（前）と（後）](../../../../managers-guide/manage-table/filter/table-management-filter-near-completion-time.md)
-   [テーブルの管理：フィルタ：検索の種類](../../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-search-types.md)
-   [テーブルの管理：フィルタ：チェック項目フィルタのコントロール種別](../../../../managers-guide/manage-table/filter/filter-settings/table-management-filter-check-filter-control-type.md)
-   [テーブルの管理：フィルタ：期限超過フィルタを使用する](../../../../managers-guide/manage-table/filter/table-management-filter-use-overdue-filter.md)
-   [テーブルの管理：一覧画面](../../../../managers-guide/manage-table/grid/index.md)
-   [テーブルの管理：一覧画面：常に検索条件を要求する](../../../../managers-guide/manage-table/grid/table-management-always-request-search-condition.md)
-   [テーブルの管理：検索](../../../../managers-guide/manage-table/search/index.md)
-   [テーブルの管理：項目](../../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブルの管理：項目：状況](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理：項目：管理者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-manager.md)
-   [テーブルの管理：項目：担当者](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-owner.md)
-   [テーブルの管理：項目：完了](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)
-   [テーブルの管理：項目：分類](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：添付ファイル](../../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
