---
title: PowerShellを利用したAPIによるレコードのインポートで403エラーが発生する
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-api-import-error
translationKey: faq-api-import-error
shortname: ''
created: 2026-01-06
updated: 2026-01-14
---

## 回答

PowerShellのInvoke-WebRequestを利用した際にWAFでブロックされる場合があります。この場合は以下の方法で対応してください。
1. Python等の言語を利用
2. 下記のサンプルスクリプトで対応

---

## 概要

WAFが導入されている環境において、PowerShellのInvoke-WebRequestが生成するmultipart/form-dataの形式が、WAFの厳密なバリデーションルールに抵触してブロックされる場合があります。このときAPIからは403エラーが返ってきます。これを回避する場合は以下の方法で対応してください。

1. PythonなどPowerShell以外のプログラミング言語で[レコードのインポートAPI](../../developers-guide/api/table-operations/api-import.md)を実行する  
2. PowerShellを利用する場合は下記「実行例のサンプル」を実行する

## 実行例のサンプル（PowerShell version6.0 以降）

##### PowerShell

```
$uri = 'https://pleasanter.net/fs/api/items/{サイトID}/import'
$filePath = './sample.csv'

$parametersJson = @{ 
    ApiVersion     = 1.1
    ApiKey         = '{APIキー}'
    Encoding       = 'UTF-8'
} | ConvertTo-Json -Compress

$curl = Join-Path $env:SystemRoot 'System32/curl.exe'

$response = & $curl `
  -sS -f `
  --form-string "parameters=$parametersJson" `
  -F "file=@$filePath;type=text/csv" `
  "$uri"

Write-Host $response
```

## 関連情報

-   [開発者ガイド：API：テーブル操作：レコードのインポート](../../developers-guide/api/table-operations/api-import.md)