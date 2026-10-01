---
title: バッチ処理で添付ファイルを含んだレコードを新規作成したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-create-record-with-attachment
translationKey: faq-create-record-with-attachment
shortname: ''
created: 2020-10-13
updated: 2024-04-29
---

## 回答

[レコード作成API](../../developers-guide/api/table-operations/api-record-create.md)を使用してください。

---

## 概要

バッチ処理で添付ファイルを含んだレコードを作成したい場合は、[レコード作成API](../../developers-guide/api/table-operations/api-record-create.md)を使用します。POSTするデータの「Attachments」オブジェクトに[JSONデータレイアウト：Item](../../developers-guide/json-data-layout/api-item.md)に記載の内容を設定してください。

## サンプルコード

##### PowerShell 

```
Add-Type -AssemblyName "System.Web"
$error.Clear()
$requestUrl = "http://servername/api/items/2/create"
$apiKey = "af14A56RE68ssa320..."
$file = Get-Item "C:\Work\Test.pptx"
trap [Net.WebException] { continue; }
try{
    $contentType = [System.Web.MimeMapping]::GetMimeMapping($file.FullName)
    $base64filelist = New-Object System.Collections.ArrayList
    [void]$base64filelist.Add(@{
        Name = $file.Name
        ContentType = $contentType
        Base64 = [Convert]::ToBase64String([System.IO.File]::ReadAllBytes($file.FullName))
    })
    $json = @{
        ApiKey = $apiKey
        Title = "Test"
        AttachmentsHash = @{
            AttachmentsA =  $base64filelist
        }
    }
    $requestBody = $json | ConvertTo-Json -Depth 3
    $res = Invoke-RestMethod -Uri $requestUrl -ContentType "application/json" -Method POST -Body ${requestBody}
    Write-Output $res
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

-   [開発者ガイド：API：テーブル操作：レコード作成](../../developers-guide/api/table-operations/api-record-create.md)
-   [開発者ガイド：JSONデータレイアウト：Item](../../developers-guide/json-data-layout/api-item.md)