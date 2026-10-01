---
title: バッチ処理で添付ファイルをダウンロードしたい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-download-attachment
translationKey: faq-download-attachment
shortname: ''
created: 2020-10-14
updated: 2024-07-12
---

## 回答

[添付ファイル取得API](../../developers-guide/api/table-operations/api-attachment-get.md)を使用してください。

--- 

## 概要

バッチ処理で添付ファイルをダウンロードしたい場合は、[添付ファイル取得API](../../developers-guide/api/table-operations/api-attachment-get.md)を使用します。
PowerShellを使って、任意レコードの添付ファイルをダウンロードします。

## 操作手順

1. テーブルを作成し、レコードにファイルを添付してください。
1. Windows PowerShellを開き、以下のスクリプト内容を記載してください。  
1. 下記の[servername]、[Guid]、[apiキー]の値を環境に合わせて書き換え、サンプルコードの3～4行目と入れ替えてください。

```
$requestUrl = "http://[servername]/api/binaries/[Guid]/get"
$apiKey = "[apiキー]"
```

レコードのGuidを取得する場合は以下のリンク先に従って取得してください。  
[API機能：単一レコード取得](../../developers-guide/api/table-operations/api-record-get.md)

### 実行結果

C:\Worksに添付ファイルがダウンロードされます。
![C:\Works に添付ファイルがダウンロードされた状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/0bd9a1338d4d49a98313f5484589ddce.png)

## サンプルコード

##### PowerShell

```
Add-Type -AssemblyName "System.Web"
$error.Clear()
$requestUrl = "http://pleasanter.example.local/api/binaries/************************/get"
$apiKey = "********..."
$path = "C:\Works"
trap [Net.WebException] { continue; }
try{
    $json = @{
        ApiKey = $apiKey
    }
    $requestBody = $json | ConvertTo-Json -Depth 3
    $res = Invoke-RestMethod -Uri $requestUrl -ContentType "application/json" -Method POST -Body ${requestBody}
    Write-Output $res
    $byte = [System.Convert]::FromBase64String($res.Response.Base64)
    [System.IO.File]::WriteAllBytes($path + "\" + $res.Response.FileName, $byte)
}
catch {
    Write-Output $_.Exception
}
if ($error.Count -gt 0)
{
    Write-Output $error[0].ErrorDetails.Message | ConvertFrom-Json
}
```

## 関連情報

-   [開発者ガイド：API：テーブル操作：添付ファイル取得](../../developers-guide/api/table-operations/api-attachment-get.md)
-   [開発者ガイド：API：テーブル操作：単一レコード取得](../../developers-guide/api/table-operations/api-record-get.md)