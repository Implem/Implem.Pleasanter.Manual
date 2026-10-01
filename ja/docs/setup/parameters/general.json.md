---
title: General.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: general.json
translationKey: general.json
shortname: General.json
created: 2019-04-30
updated: 2026-05-25
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

<span class="pl-attention">説明欄に※印を添えたパラメータは1.5.2.0以降で削除されます。カスタマイズを目的として本パラメータを利用している場合、[拡張スタートガイド](../../developers-guide/extended-features/extended-startguide.md)を利用したカスタマイズへの移行を検討してください。</span>

|パラメータ名|設定例|説明|
|:--|:--|:--|
|HtmlHeadKeywords|"Implem,Pleasanter,OSS"|HTMLヘッダに出力されるkeywordsを指定。|
|HtmlHeadDescription|"Business application platform"|HTMLに出力されるdescriptionを指定。|
|HtmlHeadViewport|""|HTMLに出力されるviewportを指定。|
|HtmlLogoText|"Pleasanter"|未使用。|
|HtmlPortalUrl|"https://pleasanter.net"|Pleasanter.netのURLを指定。|
|HtmlApplicationBuildingGuideUrl|"https://pleasanter.org/downloads/hands-on1.pdf"|アプリ作成ガイドメニューをクリックした際の移動先のURLを指定。 <span class="pl-attention">※</span>|
|HtmlUserManualUrl|"https://pleasanter.org/manual"|利用ガイドメニューをクリックした際の移動先のURLを指定。 <span class="pl-attention">※</span>|
|HtmlBlogUrl|"https://pleasanter.org/archives/category/%e3%83%96%e3%83%ad%e3%82%b0"|ブログメニューをクリックした際の移動先のURLを指定。|
|HtmlSupportUrl|"https://implem.co.jp/service/"|サポートメニューをクリックした際の移動先のURLを指定。 <span class="pl-attention">※</span>|
|HtmlContactUrl|"https://implem.co.jp/contact/"|お問い合わせメニューをクリックした際の移動先のURLを指定。|
|HtmlAGPLUrl|"https://github.com/Implem/Implem.Pleasanter/blob/master/LICENSE"|ライセンスのリンクをクリックした際のURLを指定。|
|HtmlTrialLicenseUrl|"https://pleasanter.org/ja/manual/pleasanter-extensions-trial"|トライアル中のリンクをクリックした際のURLを指定。|
|HtmlEnterpriseEditionUrl|"https://pleasanter.org/enterprise"|Enterprise editionをクリックした際の移動先のURLを指定。|
|HtmlCasesUrl|"https://pleasanter.org/cases"|事例ページのURLを指定。|
|DisplayLogoText|false|ロゴに隣接して表示する文字列の表示有無をtrue/falseで指定。|
|DisableAutoComplete|false|form要素にautocomplete="off"を出力する場合にtrueを指定。firefox等で意図しないautocompleteの発生を抑止する場合にはtrueを指定。|
|SiteMenuHotSpan|30|サイト内のレコードの最終更新日時が本パラメータで指定した日数よりも古い場合、薄い文字色で表示。|
|AnchorTargetBlank|true|[内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)、[説明](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)、[コメント](../../users-guide/common/comment.md)に記述したリンクを新規タブとして表示したい場合にはtrueを指定。|
|LimitWarning1|86400|現在時刻 - 期限の秒数が本パラメータの数値よりも小さい場合にlimit-warning1のスタイルで一覧画面上の期限を表示。|
|limit-warning2|0|現在時刻 - 期限の秒数が本パラメータの数値よりも小さい場合にlimit-warning2のスタイルで一覧画面上の期限を表示。|
|limit-warning3|-259200|現在時刻 - 期限の秒数が本パラメータの数値よりも小さい場合にlimit-warning2のスタイルで一覧画面上の期限を表示。|
|DeleteTempOldThan|1440|CodeDefiner実行時に本パラメータで指定した分数よりも古いApp_Data\Temp配下のファイルを削除。|
|DeleteHistoriesOldThan|1440|CodeDefiner実行時に本パラメータで指定した分数よりも古いApp_Data\Histories配下のファイルを削除。|
|NearCompletionTimeBeforeDays|7|本パラメータで指定した日数よりも直近の期限を持つレコードを「期限が近い」チェックボックスでフィルタされる期限の日数の既定値を指定。|
|NearCompletionTimeBeforeDays|7|「期限が近い」の日数（前）の既定値を指定。|
|NearCompletionTimeBeforeDaysMin|0|「期限が近い」の日数（前）の最小値を指定。|
|NearCompletionTimeBeforeDaysMax|30|「期限が近い」の日数（前）の最大値を指定。|
|NearCompletionTimeAfterDays|7|「期限が近い」の日数（後）の既定値を指定。|
|NearCompletionTimeAfterDaysMin|0|「期限が近い」の日数（後）の最小値を指定。|
|NearCompletionTimeAfterDaysMax|30|「期限が近い」の日数（後）の最大値を指定。|
|GridPageSize|20|ページ当たりの表示件数の既定値を指定。|
|GridPageSizeMin|10|ページ当たりの表示件数の最小値を指定。|
|GridPageSizeMax|200|ページ当たりの表示件数の最大値を指定。|
|AllowViewReset|true|ビューのリセットの許可の初期値を指定。|
|ExportOutputColumnMax|100|エクスポートカラムの上限値を指定。|
|ImportEncoding|"Shift-JIS"|インポート時のエンコード指定。|
|UpdatableImport|"Shift-JIS"|インポート時のIDが一致するレコードを更新する設定の初期値を指定。|
|AllowStandardExport|true|「標準エクスポートを許可」チェックボックスの初期値を指定|
|StandardExportType|0|「標準エクスポート種別」の既定値を指定します。<br>0：「既定」を選択<br>1：[一覧](../../managers-guide/manage-table/grid/index.md)を選択<br>2：[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)を選択<br>それ以外の値：「既定」を選択|
|ImportMax|10000|CSVインポートのレコード数の上限を指定。0の場合には制限無し。|
|ViewerSwitchingType|1|マークダウンの[ビュワー切替](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-change-viewer.md)設定の既定値を指定。1:自動/2:手動/3:無効|
|UseNegativeFilters|false|一覧画面の[否定条件のフィルタ](../../users-guide/table/record-authoring/data-analysis/table-record-negative-search.md)について使用可否の既定値を指定。|
|AllowCopy|true|「コピーを許可 」の既定値を指定。|
|AllowReferenceCopy|false|[参照コピーを許可](../../managers-guide/manage-table/editor/allow-reference-copy/index.md)の既定値を指定。|
|CharToAddWhenCopying|" - コピー"|[コピー時に追加する文字](../../managers-guide/manage-table/editor/characters-to-add-when-copying/index.md)の既定値を指定。|
|UpdateResponseType|0|1を指定することで更新時にポストバックを行わない。|
|SolutionBackupPath|"C:\\Projects\\Backups"|CodeDefinerによるソースコードのバックアップ先を指定。|
|SolutionBackupExcludeDirectories|"\\Backups"|CodeDefinerによるソースコードのバックアップで除外するディレクトリを指定。|
|SizeToUseTextArea|1025|本パラメータ以上の文字列長を持つ項目はTextAreaとして表示。本パラメータは変更不可。|
|CompletionCode|900|状況項目の値が本パラメータ以上の場合には完了レコードとする。|
|CommentDisplayLimitHistories|1|履歴画面に表示するコメント数の上限を指定。|
|CommentDisplayLimit|3|一覧画面に表示するコメント数の上限を指定。|
|WorkValueHeight|40|一覧画面上の作業量を示すSVGグラフ画像の高さを指定。|
|WorkValueTextTop|13|一覧画面上の作業量を示すSVGグラフ上に表示するテキストの相対X座標を指定。|
|ProgressRateWidth|50|一覧画面上の進捗率を示すSVGグラフ画像の幅を指定。|
|ProgressRateItemHeight|40|一覧画面上の進捗率を示すSVGグラフ画像の各要素の高さを指定。|
|ProgressRateTextTop|13|一覧画面上の進捗率を示すSVGグラフ上に表示するテキストの相対X座標を指定。|
|CalendarBegin|-120|カレンダーで選択可能な月の最小値を現在からの相対的な月数で指定。|
|CalendarEnd|120|カレンダーで選択可能な月の最大値を現在からの相対的な月数で指定。|
|CalendarLimit|300|カレンダーに表示可能なレコード数の最大値を指定。|
|CalendarYLimit|100|カレンダーで選択可能な分類の上限値を指定。|
|DefaultCalendarType|2|カレンダータイプの既定値を指定。1:標準、2:FullCalendar|
|CrosstabBegin|-120|クロス集計で選択可能な月の最小値を現在からの相対的な月数で指定。|
|CrosstabEnd|120|クロス集計で選択可能な月の最大値を現在からの相対的な月数で指定。|
|CrosstabXLimit|50|クロス集計で表示可能な列数の最大値を指定。|
|CrosstabYLimit|1000|クロス集計で表示可能な行数の最大値を指定。|
|GanttLimit|1000|ガントチャートに表示可能なレコード数の最大値を指定。|
|GanttPeriodMin|7|ガントチャートで表示する期間の最小値を日数で指定。|
|GanttPeriodMax|7|ガントチャートで表示する期間の最大値を日数で指定。|
|BurnDownLimit|1000|バーンダウンチャートに表示可能なレコード数の最大値を指定。|
|TimeSeriesLimit|1000|時系列チャートに表示可能なレコード数の最大値を指定。|
|AnalyPartPeriodValueMin| 0|[分析チャート](../../users-guide/table/record-authoring/data-visualize/table-analy-chart.md)の分析パーツダイアログ画面にて、「値」項目に数値を指定する場合の最小値を指定。|
|AnalyPartPeriodValueMax| 99999|[分析チャート](../../users-guide/table/record-authoring/data-visualize/table-analy-chart.md)の分析パーツダイアログ画面にて、「値」項目に数値を指定する場合の最大値を指定。|
|KambanLimit|1000|カンバンに表示可能なレコード数の最大値を指定。|
|KambanXLimit|50|カンバンで表示可能な列数の最大値を指定。|
|KambanYLimit|300|カンバンで表示可能な行数の最大値を指定。|
|KambanMinColumns|3|カンバンの列数の最小値を指定。|
|KambanMaxColumns|50|カンバンの列数の最大値を指定。|
|KambanColumns|10|カンバンの列数の既定値を指定。|
|ImageLibPageSize|20|画像ライブラリのページ当たりの表示件数の既定値を指定。|
|ImageLibPageSizeMin|10|画像ライブラリのページ当たりの表示件数の最小値を指定。|
|ImageLibPageSizeMax|200|画像ライブラリのページ当たりの表示件数の最大値を指定。|
|ImageSizeRegular|460|サイト画像の標準サイズを指定。|
|ImageSizeThumbnail|460|サイト画像のサムネイルのサイズを指定。|
|ImageSizeIcon|460|サイト画像のアイコンのサイズを指定。|
|ImageSizeLogo|460|ロゴ画像のサイズを指定。|
|DropDownSearchPageSize|500|ドロップダウンリストの検索機能で1度に取得するレコードの上限を指定。|
|SwitchTargetsLimit|500|レコード編集画面で前ボタンおよび次ボタンを使用可能にするレコードの上限を指定。レコード数が上限値を越えた場合、レコード移動ボタンが非表示となります。また、0を指定した場合も同様にレコード移動ボタンは表示されません。|
|SeparateMin|2|分割機能で分割できるレコードの最小数を指定。|
|SeparateMax|10|分割機能で分割できるレコードの最大数を指定。|
|FirstDayOfWeek|1|カレンダーで最初に表示する曜日を指定。**本パラメータは変更不可**|
|FirstMonth|4|日付項目のフィルタで四半期を利用する際の初月を指定。|
|DateFilterMinSpan|-1|日付項目のフィルタで候補に指定する過去の日付範囲を年単位で指定。|
|DateFilterMaxSpan|1|日付項目のフィルタで候補に指定する未来の日付範囲を年単位で指定。|
|MinTime|"1900/1/1"|Pleasanterで扱うことができる日付の最小値を指定。|
|MaxTime|"2100/1/1"|Pleasanterで扱うことができる日付の最大値を指定。|
|DateTimeStep|10|カレンダーコントロールから入力する時刻の間隔の既定値を指定。|
|UseOldDatepicker|false|日時入力で旧DatePickerを利用したい場合はtrueを指定。|
|HideCurrentTimeIcon|false|「現在日時を設定する日付項目の時計ボタン」を非表示にする場合はtrueを指定。|
|HideCurrentUserIcon|false|[ログインユーザ設定ボタン](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-own-user.md)を非表示にする場合はtrueを指定。|
|HideCurrentDeptIcon|false|[所属組織設定ボタン](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-own-dept.md)を非表示にする場合はtrueを指定。|
|EnableLightBox|true|「テーブル機能：レコードに画像を登録」で登録した画像の表示にLightBoxを利用する場合はtrueを指定。|
|EnableCodeEditor|true|[スタイル](../../developers-guide/style/index.md)／[スクリプト](../../managers-guide/manage-table/scripts/index.md)／[HTML](../../managers-guide/manage-table/html/index.md)／[サーバスクリプト](../../developers-guide/server-script/index.md)のコード入力欄でコードエディタ機能を利用する場合はtrueを指定。|
|GroupsDepthMax|10|グループの子グループの階層について深さの最大値を指定。|
|BulkUpsertMax|10000|BulkUpsertのレコード数の上限を指定。0の場合には制限無し。|
|EnableExpandLinkPath|false|テーブルの管理の[一覧](../../managers-guide/manage-table/grid/index.md)タブで「リンクの経路が異なる同一サイトを含める」機能を有効にする場合にtrueを指定。この機能は、一覧項目の選択肢に"異なるリンク経路を持つ同一のサイト"を含めたい場合に利用します。|
|BlockSiteTaskWhileRunning|false|一括処理を同一テーブルに同時投入でエラーを返す場合はtrueを指定。|
|LinkPageSizeMin|0|「テーブルの管理：リンク」の「表示件数」で設定可能な範囲の最小値を指定。|
|LinkPageSizeMax|100|「テーブルの管理：リンク」の「表示件数」で設定可能な範囲の最大値を指定。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.1.12.0 以降|ViewerSwitchingTypeを追加|
|1.1.26.0 以降|DateTimeStepを追加|
|1.2.2.1 以降|AllowCopyを追加<br>AllowReferenceCopyを追加|
|1.2.6.0 以降|CharToAddWhenCopyingを追加|
|1.3.6.0 以降|AnchorTargetBlankを追加|
|1.3.7.0 以降|HideCurrentTimeIconを追加<br>HideCurrentUserIconを追加<br>HideCurrentDeptIconを追加|
|1.3.11.0 以降|AllowStandardExportを追加|
|1.3.21.0 以降|UseNegativeFiltersを追加|
|1.4.1.0 以降|EnableLightBoxを追加|
|1.4.6.0 以降|BulkUpsertMaxを追加|
|1.4.9.0 以降|EnableCodeEditorを追加|
|1.4.12.0 以降|BlockSiteTaskWhileRunningを追加|
|1.4.12.0 以降|EnableExpandLinkPathを追加|
|1.4.15.0 以降|HtmlTrialLicenseUrlを追加|
|1.4.18.0 以降| LinkPageSizeMinを追加<br>LinkPageSizeMaxを追加<br>UseOldDatepickerを追加|
|1.5.2.0以降|StandardExportTypeを追加<br>HtmlApplicationBuildingGuideUrlを削除<br>HtmlUserManualUrlを削除<br>HtmlSupportUrlを削除|
