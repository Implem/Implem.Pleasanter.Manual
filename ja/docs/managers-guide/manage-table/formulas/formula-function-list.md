---
title: 計算式（拡張）の関数
category: 計算式
order: '50'
status: ''
parts: ''
urlstring: formula-function-list
translationKey: formula-function-list
shortname: 計算式（拡張）の関数
created: 2023-12-05
updated: 2026-09-08
---

## 概要

[計算式（拡張）](table-management-formula-extended.md)で利用できる関数です。

## 注意事項

1. 本ページに記載の関数は [計算式](index.md)タブで計算方法に［拡張］を選択した場合に利用できます。詳細な設定手順は「[テーブルの管理：計算式（拡張）](table-management-formula-extended.md)」を参照してください。
1. 数値項目の[小数点以下桁数](../editor/editor-settings/advanced-settings/general/table-management-decimal-places.md)設定により、入力・表示できる小数桁に制限がある場合があります。必要に応じて、該当項目の詳細設定を確認してください。
1. [計算式（拡張）](table-management-formula-extended.md)で行う数値計算では、一般的な浮動小数点数計算の性質に起因する小さな誤差が生じることがあります。これは、十進小数の一部（例：0.1、0.2 など）が二進小数で表現できないため、近似値で計算されることに伴うものです。類似の現象は多くのソフトウェア環境でも確認できます。金額や数量など、整数を期待する計算や、誤差により条件分岐の結果が変わり得る処理では、比較・保存の前に丸め処理（$ROUNDなど）を行うことを推奨します。  
   たとえば、数値項目Aに32.8を、数値項目Bに3095を、数値項目Cに両者を掛け算して、小数点以下を切り捨てた結果を入れるとします。数値項目Cには101516が入って欲しいのですが、実際は誤差により101515が入ります。

   |項目|設定|内容|
   |:--|:--|:--|
   |数値A|小数点以下桁数：1|32.8|
   |数値B|小数点以下桁数：0|3095|
   |数値C|$ROUNDDOWN(数値A * 数値B, 0)|期待される結果：101516<br>実際の結果：101515|

   Webブラウザの開発者ツールで、簡易に確認できます。[F12]キーを押下してコンソールを開きます。

   ```csv
   > 32.8*3095
   101515.99999999999   // 101516ではなく、誤差が発生
   > Math.floor(32.8*3095,0)  // 0.99999999999が切り捨てられる
   101515
   ```
   このような誤差を回避するには、$ROUNDで誤差を吸収し、整数化した後に$ROUNDDOWNで切り捨てします。

   |項目|設定|内容|
   |:--|:--|:--|
   |数値C|$ROUNDDOWN($ROUND(数値A * 数値B, 0), 0)|期待される結果：101516<br>実際の結果：101516|

## 計算式の関数一覧

### 日付/時刻

|No|関数名|説明|
|:--:|:---|:---|
|1|[$DATE](formula-function-date.md)|日付を生成します。|
|2|[$DATEDIF](formula-function-datedif.md)|2つの日付の間の日数、月数、または年数を計算します。|
|3|[$DATETIME](formula-function-datetime.md)|日時を生成します。|
|4|[$DAY](formula-function-day.md)|日付の日数を取得します。|
|5|[$DAYS](formula-function-days.md)|2つの日付間の日数を求めます。|
|6|[$EOMONTH](formula-function-eomonth.md)|開始日から起算して指定された月数の前または後の月の最終日を求めます。|
|7|[$HOUR](formula-function-hour.md)|日付の時間を取得します。|
|8|[$MINUTE](formula-function-minute.md)|日付の分を取得します。|
|9|[$MONTH](formula-function-month.md)|日付の月を取得します。|
|10|[$NOW](formula-function-now.md)|現在の日時を取得します。|
|11|[$SECOND](formula-function-second.md)|日付の秒を取得します。|
|12|[$TODAY](formula-function-today.md)|現在の日付を取得します。|
|13|[$WEEKDAY](formula-function-weekday.md)|日付に対応する曜日を返します。|
|14|[$YEAR](formula-function-year.md)|日付の年を取得します。|

### 文字列操作

|No|関数名|説明|
|:--:|:---|:---|
|1|[$ASC](formula-function-asc.md)|全角文字を半角文字に変換します。|
|2|[$CONCAT](formula-function-concat.md)|指定した文字列を結合します。|
|3|[$FIND](formula-function-find.md)|検索文字列を対象の文字列の中で検索し、検索文字列が最初に現れる位置を左端から数えた結果を求めます。検索は大文字小文字は区別されます。|
|4|[$JIS](formula-function-jis.md)|半角文字を全角文字に変換します。|
|5|[$LEFT](formula-function-left.md)|文字列の先頭から指定された数の文字を返します。|
|6|[$LEN](formula-function-len.md)|文字列の文字数を返します。|
|7|[$LOWER](formula-function-lower.md)|文字列に含まれる英大文字を英小文字に変換します。|
|8|[$MID](formula-function-mid.md)|文字列の指定位置から指定された数の文字を返します。|
|9|[$REPLACE](formula-function-replace.md)|対象の文字列に対して指定した文字数の文字を別の文字に変換します。|
|10|[$RIGHT](formula-function-right.md)|文字列の末尾から指定された数の文字を返します。|
|11|[$SEARCH](formula-function-search.md)|検索文字列を対象の文字列の中で検索し、検索文字列が最初に現れる位置を左端から数えた結果を求めます。検索は大文字小文字は区別されません。|
|12|[$SUBSTITUTE](formula-function-substitute.md)|対象の文字列内にある特定の文字列を指定した文字列に変換します。|
|13|[$TEXT](formula-function-text.md)|表示形式を適用した文字列に変換します。|
|14|[$TRIM](formula-function-trim.md)|文字列に含まれる不要なスペースを取り除きます。|
|15|[$UPPER](formula-function-upper.md)|文字列に含まれる英小文字を英大文字に変換します。|
|16|[$VALUE](formula-function-value.md)|文字列として入力されている数字を数値に変換します。|

### 論理

|No|関数名|説明|
|:--:|:---|:---|
|1|[$AND](formula-function-and.md)|全ての引数がTRUEの場合にTRUEを返します。|
|2|[$IF](formula-function-if.md)|論理式の結果（TRUEかFALSE）に応じて、指定された値を返します。|
|3|[$IFERROR](formula-function-iferror.md)|値がエラーの場合に指定した値を返します。エラーでない場合は値を返します。|
|4|[$IFS](formula-function-ifs.md)|1つ以上の条件が満たされるかどうかを確認し、最初の真条件に対応する値を返します。|
|5|[$NOT](formula-function-not.md)|引数がFALSEの場合はTRUE、TRUEの場合はFALSEを返します。|
|6|[$OR](formula-function-or.md)|いずれかの引数がTRUEのとき、TRUEを返します。引数がすべてFALSEである場合は、FALSEを返します。|

### 情報

|No|関数名|説明|
|:--:|:---|:---|
|1|[$ISBLANK](formula-function-isblank.md)|引数が空欄の場合にtrueを返します。|
|2|[$ISERROR](formula-function-iserror.md)|引数がエラーの場合にtrueを返します。|
|3|[$ISEVEN](formula-function-iseven.md)|引数に指定した数値が偶数のときTRUEを返し、奇数のときFALSEを返します。|
|4|[$ISNUMBER](formula-function-isnumber.md)|セルの内容が数値の場合にTRUEを返します|
|5|[$ISODD](formula-function-isodd.md)|引数に指定した数値が奇数のときTRUEを返し、偶数のときFALSEを返します|
|6|[$ISTEXT](formula-function-istext.md)|セルの内容が文字列である場合にTRUEを返します|

### 数学

|No|関数名|説明|
|:--:|:---|:---|
|1|[$ABS](formula-function-abs.md)|絶対値を返します。|
|2|[$MOD](formula-function-mod.md)|数値を除算した剰余を返します。|
|3|[$POWER](formula-function-power.md)|数値のべき乗を返します。|
|4|[$RAND](formula-function-rand.md)|0以上で1より小さい実数の乱数を返します。計算するたびに新しい乱数を返します。|
|5|[$ROUND](formula-function-round.md)|数値を指定した桁数に四捨五入した値を返します。|
|6|[$ROUNDDOWN](formula-function-rounddown.md)|数値を指定した桁数で切り捨てます。|
|7|[$ROUNDUP](formula-function-roundup.md)|数値を指定した桁数で切り上げます。|
|8|[$SQRT](formula-function-sqrt.md)|正の平方根を返します。|
|9|[$TRUNC](formula-function-trunc.md)|数値の小数部を切り捨てて、整数または指定した桁数に変換します。|

### 統計

|No|関数名|説明|
|:---|:---|:---|
|1|[$AVERAGE](formula-function-average.md)|引数の平均値を返します。|
|2|[$MAX](formula-function-max.md)|引数の最大値を返します。論理値および文字列は無視されます。|
|3|[$MIN](formula-function-min.md)|引数の最小値を返します。論理値および文字列は無視されます。|
