---
title: 格納先
category: エディタ
order: '6905'
status: ''
parts: ''
urlstring: table-management-binary-storage-provider
translationKey: table-management-binary-storage-provider
shortname: 格納先
created: 2021-05-23
updated: 2024-06-13
---

## 概要

[添付ファイル項目](../../columns/table-management-attachments.md)に登録するファイルの格納先を設定します。

## 制限事項

1. [添付ファイル項目](../../columns/table-management-attachments.md)でのみ設定できます。

## 前提条件

1. 本設定を行うには「サイトの管理権限」が必要です。
1. 本設定を行うには[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「UseStorageSelect」がtrueに設定されている必要があります。falseの場合、項目が表示されません。

## 設定内容

|No|選択肢|説明|
|:----|:----|:----|
|1|データベース|アップロードされたファイルを「データベース」内のBLOBデータとして保存します。|
|2|ローカルフォルダ (※1)|アップロードされたファイルを「ローカルディスク」のフォルダに保存します。保存先のディレクトリは、[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「Path」で指定します。|
|3|自動 (データベースまたはローカルフォルダ)|アップロードされたファイルのサイズにより格納先が自動的に切り替わります。[容量制限](table-management-limit-size.md)に指定したサイズ以下のファイルは「データベース」内のBLOBデータとして保存します。それより大きなファイルは「ローカルディスク」のフォルダに保存します。「ローカルディスク」のフォルダには1ファイルにつき[ローカルフォルダ容量制限](table-management-local-folder-limit-size.md)に指定した容量までのファイルを保存できます。|

(※1)  
ファイルの格納先がローカルフォルダの場合、下記の通りファイルを保存します。
ローカルフォルダからファイルを直接削除すると、プリザンターからファイルの参照ができなくなりますのでご注意ください。

|分類|フォルダ名|例 ※[BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)の「Path」を「C:\\\\Data」と指定する場合|
|:--|:--|:--|  
|添付項目|Attachments|C:\\Data\Attachments\\{GUID}|
|説明項目|Images|C:\\Data\Images\\{GUID}|  
|サイト画像|SiteImage|C:\\Data\SiteImage\\{FileName}|
|テナント画像|TenantImage|C:\\Data\TenantImage\\{FileName}| 

## 関連情報

-   [テーブルの管理：項目：添付ファイル](../../columns/table-management-attachments.md)
-   [パラメータ設定：BinaryStorage.json](../../../../../../setup/parameters/binary-storage-json.md)
-   [テーブルの管理：エディタ：項目の詳細設定：容量制限(MB)](table-management-limit-size.md)
-   [テーブルの管理：エディタ：項目の詳細設定：ローカルフォルダ容量制限(MB)](table-management-local-folder-limit-size.md)