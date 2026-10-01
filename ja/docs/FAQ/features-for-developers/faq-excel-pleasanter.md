---
title: ExcelからPleasanterへアクセスしたい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-excel-pleasanter
translationKey: faq-excel-pleasanter
shortname: ''
created: 2021-08-06
updated: 2025-01-30
---

## 回答

Excel VBAにてプリザンターのAPIを実行してください。

---

## 概要

Excel VBA から Pleasanter の API にアクセスする方法についてサンプルをコードつきでご紹介します。
以下では、デモサイトの「商談」テーブルのレコードを、"状況"でフィルタして取得し、シートに転記する例をご案内いたします。

## 前提条件

### VBA が利用可能であること

マクロを有効にしたブックの利用や VBA そのものの利用については、ユーザ側で対応可能であるものとします。

### VBA で利用するライブラリ

Pleasanter API では問い合わせ時のパラメータおよびレスポンスは JSON で構成します。
以下のサンプルでは VBA-JSON および VBA-Dictionary を利用してデータを解釈しますため、マクロに含めていただく必要がございます。

1. [VBA-tools/VBA-JSON: JSON conversion and parsing for VBA](https://github.com/VBA-tools/VBA-JSON)
2. [VBA-tools/VBA-Dictionary: Drop-in replacement for Scripting.Dictionary on Mac](https://github.com/VBA-tools/VBA-Dictionary)

VBA-JSON および VBA-Dictionary については、Pleasanter のプロダクトに含まれないことについてあらかじめ確認してください。

### デモ環境への登録

- [デモ環境](https://demo.pleasanter.org/)に登録済みであり、ログイン可能であること

## 手順

### ブラウザからの確認

1. [デモ環境](https://demo.pleasanter.org/)にログインします。
   ![デモ環境にログインした直後の画面](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/ecc9130e46d649c491cc77b6e360508d.png)
2. 「商談管理の例」フォルダをクリックします。
   ![サイト一覧にある「商談管理の例」フォルダ](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/44f69ba5b8d0487b8ee144c317dbe91a.png)
3. 「商談」テーブルをクリックします。
   ![「商談管理の例」フォルダの中にある「商談」テーブル](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/ed01e761b0c448e7b3c5ead714c5f406.png)
4. デモ用のサンプルデータを確認してください。
   ![「商談」テーブルの一覧画面に並ぶデモ用のサンプルデータ](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/aa65e853ac51442093251c2e3966a138.png)

### VBA でのデータ取得

以下のコードを VBA のエディタに貼り付けて SampleCode Sub プロシージャを実行します。

処理概要は以下のとおりです。

1．リクエストパラメータを作成
2．リクエストを発行
3．レスポンスをシートに転記

#### サンプルコード

```vb
Private Sub SampleCode()

''' 環境ごとに設定が必要な値
' -------- 1
' https://demo.pleasanter.org/users/editapi の API キー欄の値をコピーします。空白の場合 "作成" ボタンを押して生成します。
Const APIKEY As String = " ここに API キーを文字列として記入します "
' -------- 2
' デモサイトにて「商談管理の例」>「商談」を開き、その URL の以下の数値を 0 に置き替えます。
' https://demo.pleasanter.org/items/_ここにある数値_/index
Const SiteID As Long = 0
' -------- 3
' シート名を指定します。ここでは仮に　Sheet1 としています。
Dim SheetName As String
SheetName = "Sheet1"
'''

Dim jsonRequest As Dictionary
Dim parseResponse As Dictionary
Dim httpRequest As Object
Dim i As Integer
Dim j As Integer
Dim Sheet As Worksheet
Set Sheet = Worksheets(SheetName)
Dim Hashs As Dictionary

'---------------------------------
'　1. リクエストパラメータを生成
'    リクエストパラメータとして利用するデータを Dictionary オブジェクトとして作成します。
'---------------------------------
Set jsonRequest = New Dictionary
jsonRequest.Add "ApiVersion", "1.1"
jsonRequest.Add "ApiKey", APIKEY
jsonRequest.Add "View", New Dictionary
jsonRequest("View").Add "ColumnFilterHash", New Dictionary
' "状況"でフィルタします。ここでは"引き合い"と"提案"に対応するコード値を指定しています。
jsonRequest("View")("ColumnFilterHash").Add "Status", "[""100"",""150""]"

Set httpRequest = CreateObject("MSXML2.XMLHTTP")
httpRequest.Open "POST", "https://demo.pleasanter.org/api/items/" & SiteID & "/get", False
httpRequest.setRequestHeader "Content-Type", "application/json;charset=utf-8"

'---------------------------------
'　2. リクエストを発行
'    Dictionary を JSON 形式に変換してリクエストを実施します。
'---------------------------------
httpRequest.send JsonConverter.ConvertToJson(jsonRequest)

'---------------------------------
'　3. レスポンスをシートに転記
'    API の応答結果である JSON を辞書から読み出してシートに転記します。
'---------------------------------
Set parseResponse = JsonConverter.ParseJson(httpRequest.responseText)
Set Records = parseResponse("Response")("Data")

' 取得件数が 0 件のときは中断
If Records.Count <= 0 Then
    Exit Sub
End If

' シートに転記
Sheet.Cells.Clear
i = 2
For Each Record In Records
    j = 1
    With Sheet
        For Each ColumnName In Record.Keys()
            If ColumnName = "ApiVersion" Or ColumnName = "Comments" Or ColumnName = "AttachmentsHash" Then
                GoTo ContinueTarget:
            ElseIf Right(ColumnName, 4) = "Hash" Then
                For Each HashColumn In Record(ColumnName).Keys()
                    Set Hashs = Record(ColumnName)
                    .Cells(1, j).Value = HashColumn
                    .Cells(i, j).Value = Hashs(HashColumn)
                    j = j + 1
                Next
            Else
                .Cells(1, j).Value = ColumnName
                .Cells(i, j).Value = Record(ColumnName)
                j = j + 1
            End If
ContinueTarget:
         Next
     End With
     i = i + 1
Next

End Sub
```

#### 実行例

![VBAを実行してデータを取得した結果の例](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/5031deb75d4d48c99bf854dc3db1b2f7.png)

## 応用

ここでは読み取りの例をご紹介いたしました。
こちらをご参考にしていただき、[APIレコード作成](../../developers-guide/api/table-operations/api-record-create.md)や[APIレコード更新](../../developers-guide/api/table-operations/api-record-update.md)の仕様に対応するリクエストパラメータを構築していただくことで Excel から Pleasanter へデータを登録したり、更新したりすることも可能です。

