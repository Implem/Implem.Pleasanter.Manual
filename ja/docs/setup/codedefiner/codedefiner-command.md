---
title: CodeDefinerのコマンド一覧
category: その他
order: '0'
status: ''
parts: ''
urlstring: codedefiner-command
translationKey: codedefiner-command
shortname: CodeDefiner
created: 2024-08-30
updated: 2025-07-08
---

## 概要

[CodeDefiner](../../FAQ/system-requirements-and-setup/faq-codedefiner-about.md)のコマンドおよび引数の一覧です。

## コマンド一覧

### 1. _rdsコマンド

#### 概要

DBの作成時に使用します。

|引数|値|説明|
|:--|:--|:--|
|/y|なし|実行確認画面をスキップします|
|/f|なし|項目の縮小を許容します |  
|/p|例:/p C:\home\site\wwwroot|Implem.Pleasanterの絶対パス  <br>主にAzure App Serviceのインストールおよびバージョンアップで使用|  
|/l|ja|Service.jsonのDefaultLanguageの値を書き換えます(※1)|
|/z|Asia/Tokyo|Service.jsonのTimeZoneDefaultの値を書き換えます(※1) |  
|/c|なし|構成に変更があるテーブル名一覧を出力します。実際のテーブル構成は変更されません。|  

※1 「/l」、「/z」は初回インストール時にのみ実行します。

使用例

```
dotnet Implem.CodeDefiner.dll _rds /y
```

### 2. mergeコマンド

#### 概要

バージョンアップ時のパラメータのマージ処理で使用します。

|引数|値|説明|
|:--|:--|:--|
|/b|例:C:\web\pleasanter_bk|プリザンターのバックアップフォルダの絶対パス|
|/i|例:C:\web\pleasanter|最新バージョンのプリザンターの絶対パス |  

使用例

```
dotnet Implem.CodeDefiner.dll merge /b C:\web\pleasanter_bk /i C:\web\pleasanter
```

### 3. migrateコマンド

#### 概要

異なる種類のDBにプリザンターのデータを移行します。  
詳細な使用方法は「異なる種類のDBにプリザンターのデータを移行する手順」を確認してください。

コマンド内部で_rdsコマンドの処理を実行するため、同じ引数の指定が可能です。

|引数|値|説明|
|:--|:--|:--|
|/y|なし|実行確認画面をスキップします|
|/f|なし|項目の縮小を許容します |  
|/p|例:/p C:\home\site\wwwroot|Implem.Pleasanterの絶対パス  <br>主にAzure App Serviceのインストールおよびバージョンアップで使用|  
|/l|ja|Service.jsonのDefaultLanguageの値を書き換えます(※1)|
|/z|Asia/Tokyo|Service.jsonのTimeZoneDefaultの値を書き換えます(※1) |  

※1 「/l」、「/z」は初回インストール時にのみ実行します。

使用例

```
dotnet Implem.CodeDefiner.dll migrate
```

### 4. trialコマンド

#### 概要

商用ライセンスの機能を期間限定で利用できるようにします。
詳細な使用方法は 「Pleasanter Extensionsのトライアル」を確認してください。

|引数|値|説明|
|:--|:--|:--|
|/y|なし|実行確認画面をスキップします|
|/e|なし|カラム拡張の指定をjsonファイルより読み込みます|  

使用例

```
dotnet Implem.CodeDefiner.dll trial
```

### 5. ConvertTimeコマンド

#### 概要

データベースに格納されている日付項目に対し、指定した時間を加算または減算します。コメント項目内の更新日時も変換対象に含まれます。
主に、タイムゾーンの異なる環境へデータベースを移行する際など、日付データを一括で変換したい場合に利用できます。

|引数|値|説明|
|:--|:--|:--|
|/h|例: -9 |加算する時間（マイナス値を指定すると減算）を指定します。省略した場合は「-9」が使用されます。|

使用例

```
dotnet Implem.CodeDefiner.dll ConvertTime /h 10
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.6.0 以降|_rdsコマンドに引数「/l」、「/z」を追加|
|1.4.8.0 以降|mergeコマンド新規追加。_rdsコマンドに引数「/y」、「/f」を追加|
|1.4.15.0 以降|trialコマンド新規追加|
|1.4.16.0 以降|_rdsコマンドに引数「/c」を追加|
|1.4.18.0 以降|ConvertTimeコマンドに引数「/h」を追加|

## 関連項目

[FAQ：CodeDefinerとは](../../FAQ/system-requirements-and-setup/faq-codedefiner-about.md)
