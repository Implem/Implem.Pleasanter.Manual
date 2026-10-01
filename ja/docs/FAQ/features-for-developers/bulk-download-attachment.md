---
title: バッチ処理で複数レコードの添付ファイルを一括ダウンロードしたい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: bulk-download-attachment
translationKey: bulk-download-attachment
shortname: ''
created: 2023-11-21
updated: 2024-07-12
---

## 回答

「[複数レコード取得API](../../developers-guide/api/table-operations/api-record-get-multi.md)」、「[添付ファイル取得API](../../developers-guide/api/table-operations/api-attachment-get.md)」を使用してください。

---

## 概要

バッチ処理であるテーブルの複数レコードに添付された添付ファイルをダウンロードしたい場合は、「[複数レコード取得API](../../developers-guide/api/table-operations/api-record-get-multi.md)」と「[添付ファイル取得API](../../developers-guide/api/table-operations/api-attachment-get.md)」を使用します。本ページではPowerShellでのバッチ処理を紹介します。

## 制限事項

1. 指定可能なテーブルは1つです。  
1. 取得可能な添付ファイル項目は1つです。  

## 操作手順

1. テーブルを作成し、レコードにファイルを添付してください。
1. Windows PowerShellを開き、以下のスクリプトを記載してください。ご利用環境に合わせて、「変数定義箇所」を修正してください。
1. 作成したPowerShellを実行してください。  

### 実行結果

C:WorksにレコードIDが記載されたフォルダが作成され、配下に添付ファイルA項目に添付されているファイルがダウンロードされています。
![C:\Works にレコードIDごとのフォルダが作成された状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/641b9aad7aed48c38cd285cb2f9bf814.png)
![フォルダの中に添付ファイルがダウンロードされている状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/54ff1f3e6e1140079014409c36724852.png)

## サンプルコード

##### PowerShell

```
<#
*****************************
変数定義箇所
ユーザは変更する必要がある
*****************************
#>

# ダウンロード先Path(「C:\work」のように指定)
$toPath = '****'
# Pleasanter上の(プロトコル+ドメイン「https://pleasanter.net/fs」のように指定)
$baseUri = '****'
# APIキー
$apiKey = '****'
# テーブルのサイトID
$siteId = '9999'
# Offsetを初期化
$offSet = 0
# ApiVersionを設定
$apiVersion = 9999
# Methodを設定
$method = '****'
# ContentTypeを設定
$contentType = '****'
# 取得したい添付ファイル項目を選択する
$attachmentItem = '****'

<#
*****************************
ロジック定義箇所
ユーザは変更する必要がない
*****************************
#>
try {
# ファイルをダウンロードする処理
do {
    # JSONの中身
    $jsonData = @{
        'ApiVersion' = $apiVersion
        'ApiKey' = $apiKey
        'Offset' = $offSet
    }
    # テキスト形式に変換
    $json = $jsonData|ConvertTo-Json
    # URIを設定
    $itemUri = $baseUri + '/api/items/' + $siteId + '/get'
    # WEBページにアクセスし応答を代入
    $responseData = Invoke-WebRequest -Uri $itemUri -ContentType $contentType -Method $method -Body $json
    # 処理で使う情報の1階層上までを代入
    $response = ($responseData.Content|ConvertFrom-Json).Response
    # 1ページあたりに保有できるレコード数を代入
    $pageSize = $response.PageSize
    # テーブルに記録されている全レコード数を代入
    $totalCount = $response.TotalCount
    # レコード情報を代入
    $records = $response.Data
    # レコード単位の反復処理
    foreach ($record in $records) {
        # レコードのResultIdを代入
        $id = $record.ResultId
        # ダウンロード先フォルダパスを代入
        $folderPath = $toPath + '\' + $id
        # フォルダが存在しない場合処理を続行
        if (-not(Test-Path $folderPath)) {
            # ダウンロード先フォルダを作成
            New-Item -Path $folderPath -Type Directory
        # フォルダが存在する場合
        } else {
            write-host 'フォルダが存在します'
        }
        # 応答のAttachmentsHashの中身を代入
        $recordLinks = $record.AttachmentsHash
        # データ単位の反復処理
        foreach ($recordLink in $recordLinks){
            # AttachmentsAの中身を代入
            $attachments = $recordLink.$attachmentItem
            # ファイル単位の反復処理
            foreach ($attachment in $attachments) {
                # ファイル名を代入
                $name = $attachment.Name
                # Guidを代入
                $guId = $attachment.Guid
                # ダウンロード元にファイルが存在していれば処理を続行
                if (-not($name -eq $null)) {
                    # GUIDをもとにダウンロード元Pathを代入
                    $uri = $baseUri + '/api/binaries/' + $guId + '/get'
                    # WEBページにアクセスし応答を代入
                    $responseData = Invoke-WebRequest -Uri $uri -ContentType $contentType -Method $method -Body $json
                    # 各ファイルのBase64を代入
                    $base64 = ($responseData.Content|ConvertFrom-Json).Response.Base64
                    # $base64をデコード
                    $byte = [System.Convert]::FromBase64String($base64)
                    # 出力先のファイル名を代入
                    $toFileName = $toPath + '\' + $id + '\' + $name
                    # ファイルが存在しない場合処理を続行
                    if (-not(Test-Path $toFileName)) {
                        # ファイルをダウンロード先に作成
                        New-Item -Path $folderPath -Name $name -Type File
                        # ダウンロード先のファイルに$srcを書き込む
                        [System.IO.File]::WriteAllBytes($folderPath + '\' + $name,$byte)
                    # ファイルが存在する場合
                    } else {
                        Write-Host 'ファイルが存在します'
                    }
                }
            }
        }
    }
    $offSet = $offSet + $pageSize
} while ($totalCount -ge $offSet)
write-host 'ダウンロードが完了いたしました'
} catch {
    $_.Exception.Response
}
```
