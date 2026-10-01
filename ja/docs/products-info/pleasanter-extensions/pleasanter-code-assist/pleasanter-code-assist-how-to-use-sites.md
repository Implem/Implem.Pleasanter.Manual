---
title: サイト
category: Pleasanter Code Assist
order: '3000'
status: ''
parts: ''
urlstring: pleasanter-code-assist-how-to-use-sites
translationKey: pleasanter-code-assist-how-to-use-sites
shortname: Pleasanter Code Assist
created: 2025-02-17
updated: 2026-03-12
---

## 概要

[Pleasanter Code Assist](pleasanter-code-assist-create-workfolder.md)のサイトへのソースコード登録・更新機能について説明します。Visual Studio Codeで作成、編集したスクリプトやサーバスクリプト、スタイル、HTMLをテーブルやフォルダに登録・更新します。

## 操作手順

<div class="steps" markdown>

1.  Visual Studio Codeにて「フォルダーを開く」より[セットアップ手順](pleasanter-code-assist-setup.md)で作成した基準フォルダを開きます。
2.  sitesフォルダ配下の各フォルダでファイルを作成します。ファイル名は任意です。拡張子は下表を参照してください。また拡張子は[設定項目](pleasanter-code-assist-feature.md)で変更可能です。Pleasanter Code Assist 1.3.0以降では、sitesフォルダ配下の各フォルダにサブフォルダを作成できます。

    | 種類             | フォルダ      | 拡張子 | 備考                                                                                                             |
    | ---------------- | ------------- | ------ | ---------------------------------------------------------------------------------------------------------------- |
    | HTML             | htmls         | .html  | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.htmlで変更可能 |
    | スクリプト       | scripts       | .js    | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.jsで変更可能   |
    | サーバスクリプト | serverscripts | .js    | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.jsで変更可能   |
    | スタイル         | styles        | .css   | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.cssで変更可能  |

    ![sitesフォルダ配下の各フォルダにファイルを作成した例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/1cee265151c44a5bbe8a7213bf601ed7.png)

3.  作成したファイルにメタ情報を記載します。メタ情報は先頭行からコメントとして記載してください。++ctrl+alt+i++ キーでメタ情報テンプレートを挿入できます。

    ### 設定値

    | パラメータ名      | 必須      | 設定例                   | 説明                                                                                                                              |
    | ----------------- | --------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
    | @config           | ○         | server.json              | [セットアップ手順](pleasanter-code-assist-setup.md)で作成したサーバ接続情報ファイルを設定します                                   |
    | @filename         |           | samplescript.js          | ファイル名を指定します。専用変数※で自ファイルのファイル名を設定することができます                                                 |
    | @title            | ○         | サンプルスクリプト       | スクリプト、サーバスクリプト、スタイル、HTMLのタイトルを設定します。テーブルの管理上でのタイトルとして登録されます                |
    | @name             |           | サンプルサーバスクリプト | サーバスクリプトのみ有効。サーバスクリプトの名称を設定します。テーブルの管理上での名称として登録されます                          |
    | @siteIds          | ○         | 1234,5678                | このソースコードの登録・更新先のサイトIDを設定します。複数設定する場合はカンマ区切りで設定します                                  |
    | @siteTitles       | ○         | WBS,課題管理             | siteIdsで設定したサイトのタイトルを設定します。siteIdsを複数設定した場合は本パラメータも複数設定します                            |
    | @htmlPositionType | HTMLのみ○ | BodyScriptTop            | HTMLの挿入位置を指定します。本パラメータの値には**HeadTop / HeadBottom / BodyScriptTop / BodyScriptBottom**のいずれかを指定します |
    | @disabled         |           | false                    | 無効にする場合はtrueを設定します                                                                                                  |

    #### ファイル名の専用変数について

    @filenameの指定では以下の変数を使用することができます。変数を設定すると設定内容の文字列に変換してプリザンターへ登録・更新します。ソースコードファイル上では変換されません。

    | パラメータ名           | 説明                       |
    | ---------------------- | -------------------------- |
    | ${psFileBasename}      | 自ファイル名               |
    | ${psFileBasenameNoExt} | 自ファイル名（拡張子なし） |
    | ${psFileExtname}       | 自ファイル名の拡張子       |

    ### メタ情報記載例

    以下はスクリプトの場合のメタ情報記載例です。

    ``` js
    /*
       @config : connectionSetting.json
       @filename : autocalc.js
       @title : 工数計算自動算出
       @siteIds : 123456   
       @siteTitles : 業務改善テーブル
    */
    ```

4. ファイルを保存します。保存と同時にメタ情報の設定内容に基づき、指定したサイトにソースコードの内容を登録・更新します。

</div>

## 登録更新仕様

本機能によるデータ登録更新の仕様は以下の通りです。

| 処理 | 説明                                                                                                                                                                                                                                                  |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 参照 | Pleasanterからデータをダウンロードすることはできません                                                                                                                                                                                                |
| 登録 | メタ情報の@siteIds（サイトID）と@siteTitles（サイトタイトル）で特定したサイトに対して@title（タイトル）をキーとして同名のタイトルのデータがなければ新規登録します。出力先・条件は本機能からは設定できません。テーブルの管理から適宜設定してください。 |
| 更新 | メタ情報の@siteIds（サイトID）と@siteTitles（サイトタイトル）で特定したサイトに対して@title（タイトル）をキーとして同名のタイトルのデータがあれば更新します。出力先・条件は本機能では変更されません。変更する場合はテーブルの管理から行ってください。 |
| 削除 | データの削除はできません。メタ情報の@disabledをtrue（無効）で更新するか、テーブルの管理から削除してください                                                                                                                                           |

## 関連情報

-   [Pleasanter Code Assist：コマンドによる作業フォルダ作成](pleasanter-code-assist-create-workfolder.md)
-   [Pleasanter Code Assist：セットアップ、事前準備](pleasanter-code-assist-setup.md)
-   [Pleasanter Code Assist：コマンドおよび設定項目](pleasanter-code-assist-feature.md)
