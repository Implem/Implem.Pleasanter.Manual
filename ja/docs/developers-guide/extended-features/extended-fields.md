---
title: 拡張フィールド
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-fields
translationKey: extended-fields
shortname: 拡張フィールド
created: 2021-10-11
updated: 2024-09-13
---

## 概要

標準機能には存在しない入力フィールドを画面上に配置します。[一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)の[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)に任意の入力フィールドを追加する機能を有します。

## 制限事項

-   拡張フィールドのJSONファイルを更新した後は「アプリケーションを再起動」するまで反映しません。

## 設定方法

.\Pleasanter\App_Data\Parameters\ExtendedFields\配下に以下の内容を含むJSONファイルを作成し、「アプリケーションを再起動」してください。ファイルの拡張子は必ずjsonにしてください。ExtendedFields配下はフォルダで階層化することが可能です。この場合、配下の全てのJSONファイルが設定ファイルとして読み込まれます。

## パラメータリスト

JSONファイルに指定するパラメータは以下の通りです。

| パラメータ名           | 種類          | 設定例               | 説明                                                                                                                                                                                                              |
| :--------------------- | :------------ | :------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name                   | string        | "ExtendedField"      | 拡張機能の名称を指定します。                                                                                                                                                                                      |
| SpecifyByName          | bool          | false                | サーバスクリプトから拡張機能の名称を指定して使用する場合にtrueを指定します。                                                                                                                                      |
| Description            | string        | "Sample"             | 拡張機能の説明を記述します。                                                                                                                                                                                      |
| Disabled               | bool          | false                | 拡張機能を無効化する場合にtrueを指定します。                                                                                                                                                                      |
| DeptIdList             | List\<int>    | [ 5 ]                | 特定の組織のみ拡張機能を動作させたい場合に組織IDを指定します。                                                                                                                                                    |
| GroupIdList            | List\<int>    | [ 12 ]               | 特定のグループのみ拡張機能を動作させたい場合にグループIDを指定します。                                                                                                                                            |
| UserIdList             | List\<int>    | [ 3 ]                | 特定のユーザのみ拡張機能を動作させたい場合にユーザIDを指定します。                                                                                                                                                |
| SiteIdList             | List\<long>   | [ 115 ]              | 特定のサイトのみ拡張機能を動作させたい場合にサイトIDを指定します。                                                                                                                                                |
| IdList                 | List\<long>   | [ 87 ]               | 特定のレコードのみ拡張機能を動作させたい場合にレコードIDを指定します。                                                                                                                                            |
| Controllers            | List\<string> | [ "items" ]          | 特定のコントローラのみ拡張機能を動作させたい場合にコントローラ名を指定します。                                                                                                                                    |
| Actions                | List\<string> | [ "index" ]          | 特定のアクションのみ拡張機能を動作させたい場合にアクション名を指定します。                                                                                                                                        |
| ColumnList             | List\<string> | [ "ClassX" ]         | 特定の項目に対して拡張機能を動作させたい場合に項目名を指定します。                                                                                                                                                |
| FieldType              | string        | "Filter"             | 拡張フィールド機能で追加する項目の配置領域を指定します。指定可能な値は以下のFieldTypeリストを参照ください。                                                                                                       |
| TypeName               | string        | "nvarchar"           | 拡張フィールド機能で追加する項目の種類を指定します。指定可能な値は、bit、int、long、decimal、float、datetime、nchar、nvarcharとなります。                                                                         |
| LabelText              | string        | "sample label"       | 拡張フィールド機能で追加する項目のラベルを指定します。                                                                                                                                                            |
| ChoicesText            | string        | "A\nB\nC"            | 拡張フィールド機能で追加する分類項目の選択肢一覧を指定します。このパラメータはControlTypeでChoicesTextを設定しているときに有効になります。                                                                        |
| DefaultInput           | string        | "default value"      | 拡張フィールド機能で追加する項目の既定値を指定します。                                                                                                                                                            |
| EditorFormat           | string        | "Ymdhm"              | 拡張フィールド機能で追加する日付項目の表示形式を指定します。                                                                                                                                                      |
| ControlType            | string        | "Spinner"            | 拡張フィールド機能で追加する項目のコントロール種別を指定します。指定可能な値は以下のControlTypeリストを参照ください。指定可能な値は、TextBox、Id、Slider、Spinner、Attachments、MarkDown、ChoicesTextとなります。 |
| ValidateRequired       | bool          | false                | 拡張フィールド機能で追加する項目を入力必須にtrueを指定します。                                                                                                                                                    |
| ValidateNumber         | bool          | false                | 拡張フィールド機能で追加する項目の数値の入力検証を行う場合はtrueを指定します。入力値が数値かチェックします。                                                                                                      |
| ValidateDate           | bool          | false                | 拡張フィールド機能で追加する項目の日付の入力検証を行う場合はtrueを指定します。入力値が日付かチェックします。                                                                                                      |
| ValidateEmail          | bool          | false                | 拡張フィールド機能で追加する項目の電子メールの入力検証を行う場合はtrueを指定します。入力値がアドレスかチェックします。                                                                                            |
| MaxLength              | decimal       | 100                  | 拡張フィールド機能で追加する項目で入力できる文字列数の最大を指定します。                                                                                                                                          |
| ValidateEqualTo        | string        | "#Sample"            | 拡張フィールド機能で追加する項目と比較する対象の要素を指定します。追加した項目の値と比較対象の要素の値が等しいかチェックします。                                                                                  |
| ValidateMaxLength      | int           | 50                   | 拡張フィールド機能で追加する項目の入力文字列数の入力検証を行う場合は数値を指定します。入力値が指定した文字列数以内かチェックします。                                                                              |
| DecimalPlaces          | int           | 3                    | 拡張フィールド機能で追加する数値項目の表示する小数点以下の桁数を指定します。                                                                                                                                      |
| Nullable               | bool          | false                | 拡張フィールド機能で追加する項目のNULLを許容する場合はtrueを指定します。                                                                                                                                          |
| Unit                   | string        | "円"                 | 拡張フィールド機能で追加する項目の単位を指定します。                                                                                                                                                              |
| Min                    | decimal       | 0                    | 拡張フィールド機能で追加する数値項目の最小値を指定します。                                                                                                                                                        |
| Max                    | decimal       | 1000                 | 拡張フィールド機能で追加する数値項目の最大値を指定します。                                                                                                                                                        |
| Step                   | decimal       | 2                    | 拡張フィールド機能で追加する数値項目でControlTypeをSpinnerにしている場合のステップ数を指定します。                                                                                                                |
| AutoPostBack           | bool          | false                | 拡張フィールド機能で追加する項目で自動ポストバックを使用する場合にtrueを指定します。                                                                                                                              |
| FieldCss               | string        | "sample-field-css"   | 拡張フィールド機能で追加する項目のフィールドCSSを指定します。                                                                                                                                                     |
| CheckFilterControlType | int           | 1                    | 拡張フィールド機能で追加するチェック項目のコントロール種別を指定します。指定可能な値は以下のCheckFilterControlTypeリストを参照ください。                                                                          |
| DateTimeStep           | int           | 10                   | 拡張フィールド機能で追加する日付項目の時刻間隔(分)を指定します。                                                                                                                                                  |
| ControlCss             | string        | "sample-control-css" | 拡張フィールド機能で追加する項目のフィールドCSSを指定します。                                                                                                                                                     |
| After                  | string        | "ClassA"             | 拡張フィールド機能でフィルタ内のどの項目の後に追加するか指定します。                                                                                                                                              |
| SqlParam               | bool          | false                | 拡張フィールド機能で追加する項目の入力値を拡張SQLで使用する場合にtrueを指定します。                                                                                                                               |

### FieldTypeリスト

パラメータのFieldTypeに指定可能な値は以下の通りです。

| 値             | 説明                                 |
| :------------- | :----------------------------------- |
| Filter         | フィルタ内に項目が追加されます。     |
| ViewExtensions | フィルタ外(下)に項目が追加されます。 |

### CheckFilterControlTypeリスト

パラメータのCheckFilterControlTypeに指定可能な値は以下の通りです。

| 値  | 説明                           |
| :-- | :----------------------------- |
| 1   | オンのみの場合に指定します。   |
| 2   | オンとオフの場合に指定します。 |

## サンプルコード

下記の例では、サイトID:12345 の一覧画面のフィルタにある分類A(ClassA)の後ろへ「クライアント名」項目を追加します。

``` json linenums="1"
{
    "SiteIdList": [ 12345 ],
    "Name": "ClientName",
    "FieldType": "Filter",
    "TypeName": "nvarchar",
    "LabelText": "クライアント名",
    "After": "ClassA",
    "SqlParam": true
}
```

## 関連情報

-   [テーブル機能：レコードの一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
