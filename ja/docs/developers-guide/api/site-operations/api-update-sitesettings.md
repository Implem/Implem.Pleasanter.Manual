---
title: サイト設定の更新（部分追加/更新/削除）
category: API
order: '10000'
status: ''
parts: ''
urlstring: api-update-sitesettings
translationKey: api-update-sitesettings
shortname: updatesitesettings
created: 2023-12-07
updated: 2026-08-12
---

## 概要

APIでスタイル、スクリプト、HTML、サーバスクリプト、プロセス、状況による制御の追加、更新、削除を行うことができます。

## 事前準備

APIの操作を行うユーザの[APIキーの作成](../basics/api-key.md)を実施してください。

## リクエスト

下記のリクエスト形式でJSONデータを送信します。

|設定項目|値|
|:--|:--|  
|HTTPメソッド|POST|  
|Content-Type |application/json|  
|文字コード|UTF-8|
|URL|http://{サーバー名}/api/items/{サイトID}/updatesitesettings(※1)| 
|Body|下記の **パラメータ**、 **JSON** を参照してください。|

(※1){サーバー名}、{サイトID}の部分は、適宜、環境に合わせて編集してください。

### パラメータ

リクエストで指定するパラメータについては以下の通りです。

|パラメータ|データ型|説明|
|:--|:--|:--|
|ApiVersion|数値|APIバージョンを指定します。|
|ApiKey|文字列|APIキーを指定します。|
|Styles|オブジェクト配列|スタイルのオブジェクトを指定します。詳細については下記の **Stylesのパラメータ** を参照してください。|
|Scripts|オブジェクト配列|スクリプトのオブジェクトを指定します。詳細については下記の **Scriptsのパラメータ** を参照してください。|
|Htmls|オブジェクト配列|HTMLのオブジェクトを指定します。詳細については下記の **Htmlsのパラメータ** を参照してください。|
|ServerScripts|オブジェクト配列|サーバスクリプトのオブジェクトを指定します。詳細については下記の **ServerScriptsのパラメータ** を参照してください。|
|Processes|オブジェクト配列|プロセスのオブジェクトを指定します。詳細については下記の **Processesのパラメータ** を参照してください。|
|StatusControls|オブジェクト配列|状況による制御のオブジェクトを指定します。詳細については下記の **StatusControlsのパラメータ** を参照してください。|

### Stylesのパラメータ

<details markdown="1">
<summary>Stylesのパラメータ一覧</summary>

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Title|文字列|○|サンプルスタイル|タイトルを指定します。|
|Disabled|真偽値|-|false|無効を指定します。|
|Body|文字列|-|header#Header {background-color: blue;}|スタイルを指定します。|
|StyleAll|真偽値|-|true|出力先の 全て の有効/無効を指定します。|
|StyleNew|真偽値|-|false|出力先の 新規作成 の有効/無効を指定します。|
|StyleEdit|真偽値|-|false|出力先の 編集 の有効/無効を指定します。|
|StyleIndex|真偽値|-|false|出力先の 一覧 の有効/無効を指定します。|
|StyleCalendar|真偽値|-|false|出力先の カレンダー の有効/無効を指定します。|
|StyleCrosstab|真偽値|-|false|出力先の クロス集計 の有効/無効を指定します。|
|StyleGantt|真偽値|-|false|出力先の ガントチャート の有効/無効を指定します。|
|StyleBurnDown|真偽値|-|false|出力先の バーンダウンチャート の有効/無効を指定します。|
|StyleTimeSeries|真偽値|-|false|出力先の 時系列チャート の有効/無効を指定します。|
|StyleKamban|真偽値|-|false|出力先の カンバン の有効/無効を指定します。|
|StyleImageLib|真偽値|-|false|出力先の 画像ライブラリ の有効/無効を指定します。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したスタイルを削除します。|

</details>

### Scriptsのパラメータ

<details markdown="1">
<summary>Scriptsのパラメータ一覧</summary>

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Title|文字列|○|サンプルスクリプト|タイトルを指定します。|
|Disabled|真偽値|-|false|無効を指定します。|
|Body|文字列|-|console.log('sample script');|スクリプトを指定します。|
|ScriptAll|真偽値|-|true|出力先の 全て の有効/無効を指定します。|
|ScriptNew|真偽値|-|false|出力先の 新規作成 の有効/無効を指定します。|
|ScriptEdit|真偽値|-|false|出力先の 編集 の有効/無効を指定します。|
|ScriptIndex|真偽値|-|false|出力先の 一覧 の有効/無効を指定します。|
|ScriptCalendar|真偽値|-|false|出力先の カレンダー の有効/無効を指定します。|
|ScriptCrosstab|真偽値|-|false|出力先の クロス集計 の有効/無効を指定します。|
|ScriptGantt|真偽値|-|false|出力先の ガントチャート の有効/無効を指定します。|
|ScriptBurnDown|真偽値|-|false|出力先の バーンダウンチャート の有効/無効を指定します。|
|ScriptTimeSeries|真偽値|-|false|出力先の 時系列チャート の有効/無効を指定します。|
|ScriptKamban|真偽値|-|false|出力先の カンバン の有効/無効を指定します。|
|ScriptImageLib|真偽値|-|false|出力先の 画像ライブラリ の有効/無効を指定します。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したスクリプトを削除します。|

</details>

### Htmlsのパラメータ

<details markdown="1">
<summary>Htmlsのパラメータ一覧</summary>

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Title|文字列|○|サンプルHTML|タイトルを指定します。|
|HtmlPositionType|文字列|○|Headtop|HTMLの挿入位置を指定します。本パラメータの値には **HeadTop** / **HeadBottom** / **BodyScriptTop** / **BodyScriptBottom** のいずれかを指定します。|
|Disabled|真偽値|-|false|無効を指定します。|
|Body|文字列|-|\<div>sample html\</div>|HTMLを指定します。|
|HtmlAll|真偽値|-|true|出力先の 全て の有効/無効を指定します。|
|HtmlNew|真偽値|-|false|出力先の 新規作成 の有効/無効を指定します。|
|HtmlEdit|真偽値|-|false|出力先の 編集 の有効/無効を指定します。|
|HtmlIndex|真偽値|-|false|出力先の 一覧 の有効/無効を指定します。|
|HtmlCalendar|真偽値|-|false|出力先の カレンダー の有効/無効を指定します。|
|HtmlCrosstab|真偽値|-|false|出力先の クロス集計 の有効/無効を指定します。|
|HtmlGantt|真偽値|-|false|出力先の ガントチャート の有効/無効を指定します。|
|HtmlBurnDown|真偽値|-|false|出力先の バーンダウンチャート の有効/無効を指定します。|
|HtmlTimeSeries|真偽値|-|false|出力先の 時系列チャート の有効/無効を指定します。|
|HtmlKamban|真偽値|-|false|出力先の カンバン の有効/無効を指定します。|
|HtmlImageLib|真偽値|-|false|出力先の 画像ライブラリ の有効/無効を指定します。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したHTMLを削除します。|

</details>

### ServerScriptsのパラメータ

<details markdown="1">
<summary>ServerScriptsのパラメータ一覧</summary>

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Title|文字列|○|サンプルサーバスクリプト|タイトルを指定します。|
|Name|文字列|○|SampleServerScript|名称を指定します。|
|Body|文字列|-|context.Log('sample server script');|サーバスクリプトを指定します。|
|ServerScriptWhenloadingSiteSettings|真偽値|-|true|[条件](../../server-script/basics/server-script-conditions.md)の サイト設定読み込み時 の有効/無効を指定します。|
|ServerScriptWhenViewProcessing|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の ビュー処理時 の有効/無効を指定します。|
|ServerScriptWhenloadingRecord|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の レコード読み込み時 の有効/無効を指定します。|
|ServerScriptBeforeFormula|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 計算式の前 の有効/無効を指定します。|
|ServerScriptAfterFormula|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 計算式の後 の有効/無効を指定します。|
|ServerScriptBeforeCreate|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 作成前 の有効/無効を指定します。|
|ServerScriptAfterCreate|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 作成後 の有効/無効を指定します。|
|ServerScriptBeforeUpdate|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 更新前 の有効/無効を指定します。|
|ServerScriptAfterUpdate|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 更新後 の有効/無効を指定します。|
|ServerScriptBeforeDelete|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 削除前 の有効/無効を指定します。|
|ServerScriptAfterDelete|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 削除後 の有効/無効を指定します。|
|ServerScriptBeforeBulkDelete|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 一括削除前 の有効/無効を指定します。|
|ServerScriptAfterBulkDelete|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 一括削除後 の有効/無効を指定します。|
|ServerScriptBeforeOpeningPage|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 画面表示の前 の有効/無効を指定します。|
|ServerScriptBeforeOpeningRow|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 行表示の前 の有効/無効を指定します。|
|ServerScriptShared|真偽値|-|false|[条件](../../server-script/basics/server-script-conditions.md)の 共有 の有効/無効を指定します。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したサーバスクリプトを削除します。|

</details>

### Processesのパラメータ

<details markdown="1">
<summary>Processesのパラメータ一覧</summary>

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Name|文字列|○|A1_申請(共通)|名称を指定します。|
|DisplayName|文字列|-|A1_申請(共通)|表示名を指定します。|
|ScreenType|数値|-|10|画面種別を指定します。新規作成は10、編集は20を指定してください。|
|CurrentStatus|数値|-|100|現在の状況で選択する状況のコード値を指定してください。「*」の場合は-1を指定します。|
|ChangedStatus|数値|-|200|変更後の状況で選択する状況のコード値を指定してください。「*」の場合は-1を指定します。|
|Description|文字列|-|申請を行い、課長に承認を依頼する|説明を指定します。|
|Tooltip|文字列|-|申請を行い、承認を依頼します|ツールチップを指定します。|
|Icon|文字列|-|ui-icon-mail-closed|jQueryのアイコンの名称を指定します。<br>指定がない場合、画面上のボタンには"ui-icon-disk"が設定されます。<br>・https://api.jqueryui.com/resources/icons-list.html|
|ConfirmationMessage|文字列|-|記入した内容で申請してよろしいですか|確認メッセージを指定します。|
|SuccessMessage|文字列|-|申請しました|成功メッセージを指定します。|
|OnClick|文字列|-| console.log('Processを実行しました。');|プロセス機能で追加されたボタンクリック時に実行するスクリプトを指定します。|
|ExecutionType|数値|-|10|実行種別を指定します。指定内容は以下の通りです。<br>0：追加したボタン<br>10：新規または更新|
|ActionType|数値|-|10|アクション種別を指定します。指定内容は以下の通りです。<br>0：保存<br>10：ポストバック<br>90：無し|
|AllowBulkProcessing|真偽値|-|true|一括処理を許可をチェックする場合にtrueを指定します。|
|ValidationType|数値|-|0|入力検証種別を指定します。指定内容は以下の通りです。<br>0：マージ<br>10：置換<br>90：無し|
|ValidateInputs|オブジェクト配列|-|-|プロセスの入力検証のオブジェクトを指定します。詳細については下記の **ValidateInputsのパラメータ** を参照してください。|
|View|オブジェクト|-|-|プロセスの条件のオブジェクトを指定します。詳細については下記の **Viewのパラメータ** を参照してください。|
|DataChanges|オブジェクト配列|-|-|プロセスのデータの変更のオブジェクトを指定します。詳細については下記の **DataChangesのパラメータ** を参照してください。|
|AutoNumbering|オブジェクト|-|-|プロセスの自動採番のオブジェクトを指定します。詳細については下記の **AutoNumberingのパラメータ** を参照してください。|
|Notifications|オブジェクト配列|-|-|プロセスの通知のオブジェクトを指定します。詳細については下記の **Notificationsのパラメータ** を参照してください。|
|Depts|配列|-|[1,2]|プロセスのアクセス制御で権限付与する組織を指定します。組織IDを指定します。|
|Groups|配列|-|[3,4,5]|プロセスのアクセス制御で権限付与するグループを指定します。グループIDを指定します。|
|Users|配列|-|[11,12,13,14]|プロセスのアクセス制御で権限付与するユーザを指定します。ユーザIDを指定します。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したプロセスを削除します。|

#### ValidateInputsのパラメータ

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|ColumnName|文字列|○|Title|項目を指定します。表示名ではなく[カラム名](../../dev-column-name.md)で指定します。|
|Required|真偽値|-|true|入力必須にする場合はtrueを指定します。|
|ClientRegexValidation|文字列|-|^0[789]0\d{8}$|クライアント正規表現を指定します。ColumnNameで分類項目や説明項目などを指定した場合に有効となります。|
|ServerRegexValidation|文字列|-|^0[789]0\d{8}$|サーバ正規表現を指定します。ColumnNameで分類項目や説明項目などを指定した場合に有効となります。|
|RegexValidationMessage|文字列|-|携帯電話番号の入力に誤りがあります。|正規表現でエラーとなった場合に表示するエラーメッセージを指定します。|
|Max|数値|-|99999|入力可能な最大値を指定します。ColumnNameで数値項目などを指定した場合に有効となります。|
|Min|数値|-|0|入力可能な最小値を指定します。ColumnNameで数値項目などを指定した場合に有効となります。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したプロセスを削除します。|

#### Viewのパラメータ

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Incomplete|真偽値|-|true|未完了をチェックする場合はtrueを指定します。|
|Own|真偽値|-|true|自分をチェックする場合はtrueを指定します。|
|ColumnFilterHash|文字列|-||条件を指定します。詳細は「View」の「ColumnFilterHash」を参照してください。|
|Search|文字列|-|-インプリム|検索キーワードを指定します。|
|ErrorMessage|文字列|-|条件を満たしていません。|エラーメッセージを指定します。|

#### DataChangesのパラメータ

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Type|文字列|-|InputValue|変更種別を指定します。指定内容は下記の通りです<br>CopyValue：値のコピー<br>CopyDisplayValue：表示名のコピー<br>InputValue：値の入力<br>InputDate：日付の入力<br>InputDateTime：日時の入力<br>InputDept：組織の入力<br>InputUser：ユーザの入力|
|ColumnName|文字列|-|ClassA|項目を指定します。表示名ではなく[カラム名](../../dev-column-name.md)で指定します。|
|Value|文字列|-|ClassB<br>123<br>7,Days|コピー元または値を指定します。コピー元の場合は[カラム名](../../dev-column-name.md)で項目を指定します。値の場合は入力したい任意の文字列を指定します。変更種別が「日付の入力」または「日時の入力」の場合は『値,期間』を指定します。期間は以下の内容で指定します。<br>Days：日<br>Months：月<br>Years：年<br>Hours：時<br>Minutes：分<br>Seconds：秒|
|BaseDateTime|文字列|-|CurrentDate|変更種別が「日付の入力」または「日時の入力」の場合における基準日時を指定します。[カラム名](../../dev-column-name.md)での指定の他、以下の内容で指定できます。<br>CurrentDate：現在の日付<br>CurrentTime：現在の時刻|

#### AutoNumberingのパラメータ

「[テーブルの管理：エディタ：項目の詳細設定：自動採番](../../../managers-guide/manage-table/process/process-auto-numbering.md)」を合わせて参照ください。

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|ColumnName|文字列|-|ClassA|項目を指定します。表示名ではなく[カラム名](../../dev-column-name.md)で指定します。|
|Format|文字列|-|[yyyyMMdd]-[分類A]-[NNNN]|書式を指定します。|
|ResetType|文字列|-|Year|リセット種別を指定します。指定内容は下記の通りです<br>Year：年<br>Month：月<br>Day：日<br>String：文字列|
|Default|数値|-|1|既定値を指定します。|
|Step|数値|-|1|ステップを指定します。|

#### Notificationsのパラメータ

「[テーブルの管理：通知](../../../managers-guide/manage-table/notifications/index.md)」を合わせて参照ください。

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Type|数値|○|1|通知種別を指定します。指定内容は以下の通りです。<br>1：メール<br>2：Slack<br>3：ChagWork<br>4：Line<br>5：Lineグループ<br>6：Teams<br>7：Rocket.Chat<br>8：InCircle|
|Subject|文字列|○|申請しました|件名を指定します。 "[表示名]" と記載することで項目の値を利用できます。|
|Address|文字列|○|test@example.com|任意のメールアドレス、WebHook、roomIDのURL、またはLINEのUserID、GroupIDを指定します。|
|Token|文字列|-|xxx...|取得したchatworkのトークンまたはLINEボットアカウントのアクセストークンまたはInCircleのトークンを指定します。|
|Body|文字列|○|申請内容：[内容]|内容を指定します。"[表示名]" と記載することで項目の値を利用できます。|

</details>

### StatusControlsのパラメータ

<details markdown="1">
<summary>StatusControlsのパラメータ一覧</summary>

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Name|文字列|○|01_申請待(共通)|名称を指定します。|
|Description|文字列|-|起票時は承認項目を非表示とすべき|説明を指定します。|
|Status|数値|-|100|状況のコード値を指定してください。「*」の場合は-1を指定します。|
|ReadOnly|真偽値|-|true|レコードの制御－読取専用をチェックする場合はtrueを指定します。|
|ColumnHash|オブジェクト|-|{ "Status": "ReadOnly", "Owner": "Hidden", "ClassA": "Requied" }|「"カラム名": "設定内容"」の形式で指定します。[カラム名](../../dev-column-name.md)は項目を指定します。設定内容は以下内容で指定します。<br>Requied：入力必須<br>ReadOnly：読取専用<br>Hidden：非表示|
|View|オブジェクト|-|-|状況による制御の条件のオブジェクトを指定します。詳細については下記の **Viewのパラメータ** を参照してください。|
|Depts|配列|-|[1,2]|プロセスのアクセス制御で権限付与する組織を指定します。組織IDを指定します。|
|Groups|配列|-|[3,4,5]|プロセスのアクセス制御で権限付与するグループを指定します。グループIDを指定します。|
|Users|配列|-|[11,12,13,14]|プロセスのアクセス制御で権限付与するユーザを指定します。ユーザIDを指定します。|
|Delete|数値|-|0|本パラメータの値には **0** または **1** を指定します。**1** が設定されている場合、Idで指定したプロセスを削除します。|

#### Viewのパラメータ

|パラメータ|データ型|必須|設定例|説明|
|:--|:--|:--|:--|:--|
|Id|数値|○|3|IDを指定します。存在しないIDの場合は追加、存在するIDの場合は更新として処理されます。|
|Incomplete|真偽値|○|true|未完了をチェックする場合はtrueを指定します。|
|Own|真偽値|-|true|自分をチェックする場合はtrueを指定します。|
|ColumnFilterHash|文字列|-|-|条件を指定します。詳細は「View」の「ColumnFilterHash」を参照してください。|
|Search|文字列|-||検索キーワードを指定します。|

</details>

### JSON

送信するリクエスト(JSON)のサンプルは以下の通りです。設定の変更は指定したパラメータのものが対象となります。
※ScriptsにあるId:1のスクリプトの場合、Title、Body、ScriptAllだけが設定変更の対象となります。Disabled等の指定していないパラメータの値は変更しません。

```
{
    "ApiVersion": 1.1,
    "ApiKey": "xxxxx...",
    "Scripts": [
        {
            "Id": 1,
            "Title": "sample script 1",
            "Body": "console.log('script 1');",
            "ScriptAll": true
        },
        {
            "Id": 2,
            "Title": "sample script 2",
            "Body": "console.log('script 2');",
            "ScriptAll": true
        }
    ],
    "ServerScripts": [
        {
            "Id": 9,
            "Title": "sample serverscript 9",
            "Name": "SampleServerScript9",
            "Body": "context.Log('sample serverscript 9');",
            "ServerScriptWhenloadingSiteSettings": true
        },
        {
            "Id": 10,
            "Title": "test10",
            "Delete": 1
        }
    ],
    "Styles": [
        {
            "Id": 2,
            "Title": "test2",
            "StyleNew": false
        }
    ],
    "Htmls": [
        {
            "Id": 3,
            "Title": "sample html 3",
            "HtmlPositionType": "HeadTop",
            "Body": "<div>sample html 3</div>"
        }
    ],
    "Processes": [
        {
            "Id": 1,
            "Name": "A1_申請(共通)",
            "DisplayName": "申請",
            "CurrentStatus": 100,
            "ChangedStatus": 200,
            "Description": "申請を行い、課長に承認を依頼する",
            "Tooltip": "申請を行い、承認を依頼します",
            "Icon": "ui-icon-mail-closed",
            "ConfirmationMessage": "記入した内容で申請してよろしいですか",
            "SuccessMessage": "申請しました",
            "ValidateInputs": [
                {
                    "Id": 1,
                    "ColumnName": "NumA",
                    "Required": true,
                    "Min": 1.0,
                    "Max": 5000000.0
                },
                {
                    "Id": 4,
                    "Delete": 1
                }
            ],
            "View": {
                "Own": true
            },
            "DataChanges": [
                {
                    "Id": 1,
                    "Type": "InputDateTime",
                    "ColumnName": "DateA",
                    "BaseDateTime": "CurrentTime",
                    "Value": "0,Days"
                },
                {
                    "Id": 5,
                    "Delete": 1
                }
            ]
        },
        {
            "Id": 17,
            "Name": "E4_経理による差戻",
            "Delete": 1
        }
    ],
    "StatusControls": [
        {
            "Id": 1,
            "Name": "01_申請待(共通)",
            "Description": "起票時は承認項目を非表示とすべき",
            "Status": 100,
            "ColumnHash": {
                "Status": "ReadOnly",
                "Owner": "Hidden",
                "ClassA": "Hidden",
                "DateA": "Required",
               "DescriptionB": "ReadOnly",
            }
        },
        {
            "Id": 11,
            "Name": "06-4_完了γ",
            "Delete": 1
        }
    ]    
}
```

## レスポンス

下記の形式でJSONデータが返却されます。

### サイト設定の更新（部分追加/更新/削除）ができた場合

```
{
    "Id": 6714,
    "StatusCode": 200,
    "Message": "\" 記録テーブル \" を更新しました。"
}
```

### サイトの管理権限がないユーザのAPIキーを用いた場合

```
{
    "Id": 123,
    "StatusCode": 403,
    "Message": "この操作を行うための権限がありません。"
}
```

### 必須パラメータが存在しなかった場合

```
{
    "Id": 123,
    "StatusCode": 404,
    "Message": "指定された情報は見つかりませんでした。"
}
```

## サンプルコード

##### コード内の【 ... 】 は適宜修正してください。

<details markdown="1">
<summary>1. JavaScriptファイルを任意のサイトすべてに登録する</summary>

任意のフォルダに格納されたJavaScriptファイルを読み取り、コード内に指定されたサイトのサーバスクリプトにコードを追加していきます。

##### Python(api_site_update_sitesettings.py)

```
# osに関する機能を利用するためのライブラリ
import os

# jsonを扱うためのライブラリ
import json

# Path操作のためのライブラリ
from pathlib import Path

# 型ヒント用ライブラリ
from typing import List, Optional

# HTTPリクエスト送信用のライブラリ
import requests

# =========
# 設定
# =========
BASE_URL = "【URL】"
API_KEY = "【APIキー】"

# 更新対象サイトID（複数）
SITE_IDS: List[int] = [【サイトID】, 【サイトID】]

# ServerScript情報の指定
SERVER_SCRIPT_NAME = "【サーバスクリプト名】"  # 例：任意のサーバスクリプト名
SERVER_SCRIPT_ID = 【サーバスクリプトID】
# サーバスクリプトの条件を配列形式で指定
# 条件は欄外参照
SERVER_SCRIPT_CONDITIONS = [
    {
        "Type": "【サーバスクリプト条件】",
        "Enabled": True,
    },
    {
        "Type": "【サーバスクリプト条件】",
        "Enabled": True,
    },
]

# ローカルのJSファイル（Bodyに入れる内容）
JS_FILE_PATH = r"【パス名】\【javascriptファイル名】"

# タイムアウト等
TIMEOUT_SEC = 30

def read_js_file(path: str) -> str:
    p = Path(path)
    if not p.exists():
        raise FileNotFoundError(f"JS file not found: {p}")
    # Pleasanter側で改行含めてそのまま扱いたいので text で読む
    return p.read_text(encoding="utf-8")

def build_payload(
    body_js: str, script_name: str, script_id: Optional[int] = None
) -> dict:
    # ServerScripts 要素（最小限）
    script_obj = {
        "Name": script_name,
        "Title": script_name,
        "Body": body_js,
    }
    if script_id is not None:
        script_obj["Id"] = script_id

    for SERVER_SCRIPT_CONDITION in SERVER_SCRIPT_CONDITIONS:
        script_obj[SERVER_SCRIPT_CONDITION["Type"]] = SERVER_SCRIPT_CONDITION["Enabled"]

    # パターンA：直に配列
    payload = {
        "ApiVersion": 1,
        "ApiKey": API_KEY,
        "ServerScripts": [script_obj],
    }
    return payload

def update_site_settings(site_id: int, payload: dict) -> requests.Response:
    url = f"{BASE_URL.rstrip('/')}/api/items/{site_id}/updatesitesettings"
    headers = {
        "Content-Type": "application/json",
    }
    return requests.post(
        url, headers=headers, data=json.dumps(payload), timeout=TIMEOUT_SEC
    )

def main():
    body_js = read_js_file(JS_FILE_PATH)
    print(f"body_js={body_js}")

    # 例：全サイト同じ ServerScript 名を更新
    for site_id in SITE_IDS:
        payload = build_payload(
            body_js=body_js, script_name=SERVER_SCRIPT_NAME, script_id=SERVER_SCRIPT_ID
        )

        try:
            resp = update_site_settings(site_id, payload)
        except requests.RequestException as e:
            print(f"[ERROR] site_id={site_id} request failed: {e}")
            continue

        if resp.ok:
            print(f"[OK] site_id={site_id} updated. status={resp.status_code}")
        else:
            # 失敗時はレスポンス本文を出して原因を追えるように
            print(f"[NG] site_id={site_id} status={resp.status_code}")
            print(resp.text)

if __name__ == "__main__":
    main()
```

##### 条件の設定

|条件|設定値|
|:--|:--|
|サイト設定の読み込み時|ServerScriptWhenloadingSiteSettings|
|ビュー処理時|ServerScriptWhenViewProcessing|
|レコード読み込み時|ServerScriptWhenloadingRecord|
|計算式の前|ServerScriptBeforeFormula|
|計算式の後|ServerScriptAfterFormula|
|作成前|ServerScriptBeforeCreate|
|作成後|ServerScriptAfterCreate|
|更新前|ServerScriptBeforeUpdate|
|更新後|ServerScriptAfterUpdate|
|削除前|ServerScriptBeforeDelete|
|削除後|ServerScriptAfterDelete|
|一括削除前|ServerScriptBeforeBulkDelete|
|一括削除後|ServerScriptAfterBulkDelete|
|画面表示の前|ServerScriptBeforeOpeningPage|
|行表示の前|ServerScriptBeforeOpeningRow|
|共有|ServerScriptShared|

設定例
```
SERVER_SCRIPT_CONDITIONS = [
    {
        "Type": "ServerScriptBeforeOpeningPage",
        "Enabled": True,
    },
    {
        "Type": "ServerScriptBeforeOpeningRow",
        "Enabled": True,
    },
]
```

##### 実行

```
>python api_site_update_sitesettings.py
```

##### 実行結果

```
body_js=【ここに挿入されるbodyの内容が表示されます】

[OK] site_id=9001 updated. status=200
[OK] site_id=9002 updated. status=200
```
</details>

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.11.0 以降|ProcessesのパラメータにIconを追加|
|1.4.16.0 以降|ServerScriptsのパラメータにServerScriptBeforeBulkDeleteおよびServerScriptAfterBulkDeleteを追加|

## 関連情報

-   [開発者ガイド：API：APIキーの作成](../basics/api-key.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
-   [項目名とデータベース上のカラム名の対応](../../dev-column-name.md)