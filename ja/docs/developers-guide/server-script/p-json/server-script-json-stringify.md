---
title: "$p.JSON.stringify（非推奨）"
icon: material/alpha-m-box
category: サーバスクリプト
order: '80000'
status: deprecated
parts: ''
urlstring: server-script-json-stringify
translationKey: server-script-json-stringify
shortname: ''
created: 2024-02-22
updated: 2025-01-14
---

!!! warning "非推奨"
    このメソッドは非推奨となります。[$ps.JSON.stringify](../ps-json/server-script-ps-json-stringify.md)をご利用ください。

## 概要

[サーバスクリプト](../index.md)でmodelなどサーバスクリプトで利用可能なオブジェクトや、サーバから返却されるオブジェクトを文字列にシリアライズします。

## 構文

```
$p.JSON.stringify(value)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|value|object|○|サーバスクリプトのオブジェクト|

## 使用例

以下の例では、modelオブジェクトの内容をシリアライズしてコンソールに出力しています。

##### JavaScript

```
context.Log($p.JSON.stringify(model));
```

##### 出力例

```
{"ReadOnly":false,"SiteId":73152,"Title":"ネットワークの構築","Body":"ネットワークを構築します。\r\n　・VLANの設定\r\n　・スイッチの設定","Ver":3,"Creator":29867,"Updator":29867,"CreatedTime":"2024-01-20T16:56:00","UpdatedTime":"2024-02-05T13:02:00","ClassA":"構築","ClassB":"作業[定型]","ClassC":"ネットワーク・セキュリティ","CheckA":false,"AttachmentsA":"[]","Comments":"[]","IssueId":73209,"StartTime":"2024-02-02T00:00:00","CompletionTime":"2024-02-05T00:00:00","WorkValue":12.0000,"ProgressRate":85.0,"RemainingWorkValue":1.8000000,"Status":100,"Manager":29867,"Owner":29867,"Locked":false}
```

## 関連情報

-   [開発者ガイド：サーバスクリプト：$ps.JSON.stringify](../ps-json/server-script-ps-json-stringify.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
