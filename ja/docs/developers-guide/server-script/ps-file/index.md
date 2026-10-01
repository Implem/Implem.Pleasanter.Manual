---
title: "$ps.file"
icon: material/alpha-o-box
category: サーバスクリプト
order: '70000'
status: ''
parts: ''
urlstring: server-script-ps-file
translationKey: server-script-ps-file
shortname: $ps.file,$ps.fileオブジェクト
created: 2024-12-23
updated: 2026-06-29
---

## 概要

[サーバスクリプト](../index.md)でWEBサーバ内のファイルとディレクトリの操作を行うオブジェクトです。ファイルの書き込み・読み込み・削除・名称変更とディレクトリの作成・削除・名称変更ができます。

## 注意事項

1.  [サーバスクリプト](../index.md)でファイル・ディレクトリの操作を行うとサーバ側の処理負荷が増大することがあります。[サーバスクリプト](../index.md)の実行時間が指定した処理タイムアウト時間を超えるとタイムアウトにより処理が停止し「アプリケーションエラー」が発生します。タイムアウト時間の調整は[Script.json](../../../setup/parameters/script-json.md)の「ServerScriptTimeOut」で行います。

## 制限事項

1.  ファイル・ディレクトリに対するアクセス権はWebサーバOSに依存します。プリザンターのアクセス権は使用できません。
1.  セクション名とディレクトリ名とファイル名に使用できる文字の種類は以下の半角文字です。  
アルファベット（A-Z、a-z）  
数字（0-9）  
アンダーバー（_）  
ハイフン（-）  
ドット（.）
1.  基準ディレクトリ(Script.json の ServerScriptFilePath)には、ルートディレクトリの指定（Windowsでは"C:\\"や"D:\\"、Linuxでは"/"）や相対パスの指定はできません。

## 前提条件

1.  [Script.json](../../../setup/parameters/script-json.md)のDisableServerScriptFileをfalseに設定することが必要です。

## プロパティ

プロパティはありません。

## メソッド

| No  | Name                                                            | Description                                          |
| :-- | :-------------------------------------------------------------- | :--------------------------------------------------- |
| 1   | [readAllText](server-script-ps-file-read-all-text.md)           | テキストファイル読み込みます。                       |
| 2   | [writeAllText](server-script-ps-file-write-all-text.md)         | テキストファイル書き込みます。                       |
| 3   | [removeFile](server-script-ps-file-remove-file.md)              | ファイルを削除します。                               |
| 4   | [moveFile](server-script-ps-file-move-file.md)                  | ファイル名を変更またはファイルを移動します。         |
| 5   | [getFileList](server-script-ps-file-get-file-list.md)           | 指定ディレクトリ内のファイル名一覧を取得します。     |
| 6   | [getDirectoryList](server-script-ps-file-get-directory-list.md) | 指定ディレクトリ内のディレクトリ名一覧を取得します。 |
| 7   | [createDirectory](server-script-ps-file-create-directory.md)    | ディレクトリを作成します。                           |
| 8   | [removeDirectory](server-script-ps-file-remove-directory.md)    | ディレクトリを削除します。                           |
| 9   | [moveDirectory](server-script-ps-file-move-directory.md)        | ディレクトリ名を変更またはディレクトリを移動します。 |
| 10  | [createSection](server-script-ps-file-create-section.md)        | セクションを作成します。                             |
| 11  | [removeSection](server-script-ps-file-remove-section.md)        | セクションを削除します。                             |
| 12  | [copyFile](server-script-ps-file-copy-file.md)                  | 指定ファイルをコピーします。                         |

## セクションとは

$ps.fileオブジェクトでは「セクション」という単位でファイルやディレクトリを用途ごとにグループ化して操作します。Webサーバ内の配置としては基準ディレクトリの直下にセクション名のディレクトリが作成され、そのディレクトリ内にファイルやディレクトが構築されます。セクション配下にはサブディレクトリを設定することができます。
基準ディレクトリおよびセクションの設定とWebサーバ上の配置についての関連は下図の通りです。

![基準ディレクトリとセクションのWebサーバ上の配置を示す図](https://pleasanter.org/files/images/ja/developers-guide/server-script/ps-file/assets/1668c42d6ba6443299321027e833b466.png)

基準ディレクトリをC:\fileshareとした場合、このパスを[Script.json](../../../setup/parameters/script-json.md)の"ServerScriptFilePath"に設定します。  
セクションは基準ディレクトリの直下のディレクトリを指しますので、上図では01_develop、02_salesが該当します。  
セクション以下のファイルを読み込むことを例にパラメータの設定内容について説明します。

#### 例1. 0101_emplist.csvを読み込む場合

0101_emplist.csvはWebサーバ上ではC:\fileshare\01_develop\0101_emplist.csvであるため、セクションは「01_develop」、ファイル名は「0101_emplist.csv」となります。  
したがって、[$ps.file.readAllText](server-script-ps-file-read-all-text.md)でファイルを読み込む場合は以下のような指定となります。

##### JavaScript

```
const section = '01_develop';
const path = '0101_emplist.csv';
$ps.file.readAllText(section, path);
```

#### 例2. saleslist_202501.csvを読み込む場合

saleslist_202501.csvはWebサーバ上ではC:\fileshare\02_sales\reports\saleslist_202501.csvであるため、セクションは「02_sales」、ファイル名はサブディレクトリの指定も含めた「reports/saleslist_202501.csv」となります。  
したがって、[$ps.file.readAllText](server-script-ps-file-read-all-text.md)でファイルを読み込む場合は以下のような指定となります。

##### JavaScript

```
const section = '02_sales';
const path = 'reports/saleslist_202501.csv';
$ps.file.readAllText(section, path);
```

## 対応バージョン

| 対応バージョン | 内容                   |
| :------------- | :--------------------- |
| 1.4.12.0 以降  | 機能追加               |
| 1.4.19.0 以降  | copyFileメソッドを追加 |

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [パラメータ設定：Script.json](../../../setup/parameters/script-json.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.readAllText](server-script-ps-file-read-all-text.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.writeAllText](server-script-ps-file-write-all-text.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.removeFile](server-script-ps-file-remove-file.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.moveFile](server-script-ps-file-move-file.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.getFileList](server-script-ps-file-get-file-list.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.getDirectoryList](server-script-ps-file-get-directory-list.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.createDirectory](server-script-ps-file-create-directory.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.removeDirectory](server-script-ps-file-remove-directory.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.moveDirectory](server-script-ps-file-move-directory.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.createSection](server-script-ps-file-create-section.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.removeSection](server-script-ps-file-remove-section.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.copyFile](server-script-ps-file-copy-file.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.export](server-script-ps-file-export.md)
-   [開発者ガイド：サーバスクリプト：$ps.file.import](server-script-ps-file-import.md)
