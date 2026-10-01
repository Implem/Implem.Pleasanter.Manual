---
title: 拡張機能
category: Pleasanter Code Assist
order: '4000'
status: ''
parts: ''
urlstring: pleasanter-code-assist-how-to-use-extensions
translationKey: pleasanter-code-assist-how-to-use-extensions
shortname: Pleasanter Code Assist,Pleasanter Code Assistの拡張機能
created: 2025-02-17
updated: 2026-08-14
---

## 概要

[Pleasanter Code Assist](pleasanter-code-assist-create-workfolder.md)の拡張機能テーブルへのソースコード登録・更新機能について説明します。Visual Studio Codeで作成、編集したスクリプトやサーバスクリプト、スタイル、SQLを拡張機能テーブルに登録・更新します。

**プリザンターのバージョン1.4.16.0から、セキュリティ強化のため利用条件が変更されています。バージョン1.4.16.0以降にアップデートのうえ、必要なときのみ「Extensions APIを許可」チェックボックスをオンにして利用してください。**

### 利用条件

拡張機能テーブル（Extensionsテーブル）を利用するには、以下の条件を満たしている必要があります。

#### バージョン1.4.16.0 以降の利用条件

1.  特権ユーザでログイン後、[テナントの管理](../../../managers-guide/tenant-administration/index.md)画面で「Extensions APIを許可する」のチェックをオンにする
1.  特権ユーザのAPIキーを使用する

#### バージョン1.4.15.0以前の利用条件

1.  テナント管理者のAPIキーを使用する

## 制限事項

1.  拡張機能テーブルへの反映後はプリザンターの再起動が必要です。

## 操作手順

<div class="steps" markdown>

1.  Visual Studio Codeにて「フォルダーを開く」より[セットアップ手順](pleasanter-code-assist-setup.md)で作成した基準フォルダを開きます。
1.  extensionsフォルダ配下の各フォルダにて設定ファイルを作成します。設定ファイルは以下内容を含むJSONファイルとしてください。ファイル名は任意です。拡張子は必ず`.json`としてください。

    ![extensionsフォルダ配下に作成した設定ファイル（JSON）の例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/944a669488a040b1a2b708f5af3320ac.png)

    ++ctrl+alt+i++ キーで設定情報のテンプレートを挿入できます。

    ### 共通

    | パラメータ名 | 設定例                     | 説明                                                                               |
    | ------------ | -------------------------- | ---------------------------------------------------------------------------------- |
    | Name         | Sample                     | 拡張サーバスクリプト、拡張SQLをAPIから実行させる際の名前を設定します。             |
    | Description  | "このSQLは...を実行します" | ソースコードの説明。動作には影響しません。                                         |
    | Disabled     | false                      | trueの場合は無効化され動作しません。                                               |
    | DeptIdList   | [1,2,3]                    | 対象となる組織IDを配列形式で指定します。指定しない場合には省略可能です。           |
    | GroupIdList  | [1,2,3]                    | 対象となるグループIDを配列形式で指定します。指定しない場合には省略可能です。       |
    | UserIdList   | [1,2,3]                    | 対象となるユーザIDを配列形式で指定します。指定しない場合には省略可能です。         |
    | SiteIdList   | [1,2,3]                    | 対象となるサイトのサイトIDを配列形式で指定します。指定しない場合には省略可能です。 |
    | IdList       | [1,2,3]                    | 対象となるレコードのIDを配列形式で指定します。指定しない場合には省略可能です。     |
    | Controlles   | ["items"]                  | 対象となるコントローラを配列形式で指定します。指定しない場合には省略可能です。     |
    | Actions      | ["index","edit"]           | 対象となるアクションを配列形式で指定します。指定しない場合には省略可能です。       |

    ### 拡張サーバスクリプト専用

    ??? tip "こちらをクリックすると詳細が開閉します"

        拡張サーバスクリプトは上記の共通パラメータに加えて下表のパラメータを適宜設定します。

        | パラメータ名            | 設定例 | 説明                                                                                                     |
        | ----------------------- | ------ | -------------------------------------------------------------------------------------------------------- |
        | WhenloadingSiteSettings | false  | trueの場合、サイト設定読み込み時 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。 |
        | WhenViewProcessing      | false  | trueの場合、ビュー処理時 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。         |
        | WhenloadingRecord       | false  | trueの場合、レコード読み込み時 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。   |
        | BeforeFormula           | false  | trueの場合、計算式の前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。           |
        | AfterFormula            | false  | trueの場合、計算式の後 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。           |
        | BeforeCreate            | false  | trueの場合、作成前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。               |
        | AfterCreate             | false  | trueの場合、作成後 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。               |
        | BeforeUpdate            | false  | trueの場合、更新前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。               |
        | AfterUpdate             | false  | trueの場合、更新後 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。               |
        | BeforeDelete            | false  | trueの場合、削除前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。               |
        | AfterDelete             | false  | trueの場合、削除後 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。               |
        | BeforeBulkDelete        | false  | trueの場合、一括削除前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。           |
        | AfterBulkDelete         | false  | trueの場合、一括削除後 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。           |
        | BeforeOpeningPage       | false  | trueの場合、画面表示の前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。         |
        | BeforeOpeningRow        | false  | trueの場合、行表示の前 の[条件](../../../FAQ/editor/faq-condition-mode-range.md)で実行します。           |

    ### 拡張SQL専用

    ??? tip "こちらをクリックすると詳細が開閉します"

        拡張SQLは上記の共通パラメータに加えて下表のパラメータを適宜設定します。

        | パラメータ名                      | 設定例                | 説明                                                                                                                                                                 |
        | --------------------------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | ColumnList                        | ["ClassA"]            | OnSelectingColumnを使用する際に対象となる[データベースのカラム名](../../../developers-guide/dev-column-name.md)を配列形式で指定します。                                                        |
        | Api                               | false                 | trueの場合[APIから拡張SQLを実行](../../../developers-guide/extended-features/extended-sql/extended-sql-api.md)することが可能です。また[サーバスクリプト](../../../developers-guide/server-script/index.md)の「extendedSqlオブジェクト」から使用可能となります。 |
        | DbUser                            | "Owner"               | APIから拡張SQLを実行する際のDBユーザを指定します。指定しない場合は"User"で実行されます。APIから実行する場合のみ有効となります。                                      |
        | Html                              | false                 | trueの場合Htmlのinputタグにhiddenタイプとして取得した値を格納します。                                                                                                |
        | OnCreating                        | false                 | trueの場合レコード作成前に実行します。                                                                                                                               |
        | OnCreated                         | false                 | trueの場合レコード作成後に実行します。                                                                                                                               |
        | OnUpdating                        | false                 | trueの場合レコード更新前に実行します。                                                                                                                               |
        | OnUpdated                         | true                  | trueの場合レコード更新後に実行します。                                                                                                                               |
        | OnDeleting                        | false                 | trueの場合レコード削除前に実行します。                                                                                                                               |
        | OnDeleted                         | false                 | trueの場合レコード削除後に実行します。                                                                                                                               |
        | OnBulkDeleting                    | false                 | trueの場合レコード一括削除前に実行します。                                                                                                                           |
        | OnBulkDeleted                     | false                 | trueの場合レコード一括削除後に実行します。                                                                                                                           |
        | OnImporting                       | false                 | trueの場合レコードインポート前に実行します。                                                                                                                         |
        | OnImported                        | false                 | trueの場合レコードインポート後に実行します。                                                                                                                         |
        | OnSelectingColumn                 | false                 | trueの場合一覧画面および編集画面に表示する項目の内容を動的に取得するためのSQLを追加します。                                                                            |
        | OnSelectingWhere                  | false                 | trueの場合一覧画面および編集画面に表示するレコードを限定するためのWhere句を追加します。                                                                                |
        | OnSelectingWhereParams            | ["ExtendedFieldName"] | 指定した拡張フィールドに値が入力されたときにOnSelectingWhereへ値をパラメータとして追加します。　※値は拡張フィールドの"Name"を指定します                              |
        | OnSelectingWherePermissionsDepts  | false                 | trueの場合アクセス制御の選択肢一覧に表示するDeptsテーブルのレコードを限定するWhere句を追加します                                                                     |
        | OnSelectingWherePermissionsGroups | false                 | trueの場合アクセス制御の選択肢一覧に表示するGroupsテーブルのレコードを限定するWhere句を追加します                                                                    |
        | OnSelectingWherePermissionsUsers  | false                 | trueの場合アクセス制御の選択肢一覧に表示するUsersテーブルのレコードを限定するWhere句を追加します                                                                     |
        | OnSelectingOrderBy                | false                 | trueの場合一覧画面に表示するレコードを並び替えるためのOrderBy句を追加します。                                                                                        |
        | OnSelectingOrderByParams          | ["ExtendedFieldName"] | 指定した拡張フィールドに値が入力されたときにOnSelectingOrderByへ値をパラメータとして追加します。　※値は拡張フィールドの"Name"を指定します                            |
        | OnUseSecondaryAuthentication      | false                 | trueの場合二段階認証前に実行します。                                                                                                                                 |

1.  2.で作成した設定ファイルと対になるソースコードのファイルを作成します。**ファイル名は2.で作成した設定ファイルと同じ名称**にしてください。拡張子は下表を参照してください。例えば設定ファイルが**sample.json**の場合、拡張SQLのソースコードファイルは**sample.sql**となります。また拡張子は[設定項目](pleasanter-code-assist-feature.md)で変更可能です。Pleasanter Code Assist 1.3.0以降では、extensionsフォルダ配下の各フォルダにサブフォルダを作成できます。

    | 種類                 | フォルダ      | 拡張子 | 備考                                                                                                            |
    | -------------------- | ------------- | ------ | --------------------------------------------------------------------------------------------------------------- |
    | 拡張スクリプト       | scripts       | .js    | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.jsで変更可能  |
    | 拡張サーバスクリプト | serverscripts | .js    | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.jsで変更可能  |
    | 拡張SQL              | sqls          | .sql   | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.sqlで変更可能 |
    | 拡張スタイル         | styles        | .css   | 拡張子は[設定項目](pleasanter-code-assist-feature.md)pleasanter-code-assist.fileExtensionMappings.cssで変更可能 |

    ![設定ファイルと対になるソースコードファイルを作成した例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/d73656a672b349959908d123b50aa93e.png)

1.  作成したソースコードファイルにメタ情報を記載します。メタ情報は先頭行からコメントとして記載してください。++ctrl+alt+i++ キーでメタ情報テンプレートを挿入できます。

    ### 設定値

    | パラメータ名 | 必須 | 設定例                  | 説明                                                                                            |
    | ------------ | ---- | ----------------------- | ----------------------------------------------------------------------------------------------- |
    | @config      | ○    | server.json             | [セットアップ手順](pleasanter-code-assist-setup.md)で作成したサーバ接続情報ファイルを設定します |
    | @filename    |      | samplesql.json.js       | ファイル名を指定します。専用の変数で自ファイルのファイル名を設定することができます              |
    | @name        | ○    | サンプル拡張SQL         | 名称を設定します                                                                                |
    | @description |      | 拡張SQLのサンプルです。 | 説明を設定します                                                                                |
    | @disabled    |      | false                   | 無効にする場合はtrueを設定します。省略時はfalseとみなします                                     |

    !!! note "ファイル名の専用変数について"

        @filenameの指定では以下の変数を使用することができます。変数を設定すると設定内容の文字列に変換してプリザンターへ登録・更新します。ソースコードファイル上では変換されません。

        | パラメータ名           | 説明                       |
        | ---------------------- | -------------------------- |
        | ${psFileBasename}      | 自ファイル名               |
        | ${psFileBasenameNoExt} | 自ファイル名（拡張子なし） |
        | ${psFileExtname}       | 自ファイル名の拡張子       |

1.  ソースコードファイルを保存します。保存と同時にメタ情報の設定内容に基づき、Extensionsテーブルに設定ファイルの内容とソースコードの内容を登録・更新します。
1.  Extensionsテーブルの内容を反映するためにプリザンターを再起動します。

</div>

## 登録更新仕様

本機能によるデータ登録更新の仕様は以下の通りです。

| 処理 | 説明                                                                                                                      |
| ---- | ------------------------------------------------------------------------------------------------------------------------- |
| 参照 | データをダウンロードすることはできません                                                                                  |
| 登録 | メタ情報の@name（名前）をキーとして同名のデータがなければ新規登録します                                                   |
| 更新 | メタ情報の@name（名前）をキーとして同名のデータがあれば更新します                                                         |
| 削除 | データの削除はできません。メタ情報の@disabledをtrue（無効）で更新するか、Extensionsテーブルのデータを直接削除してください |

## 対応バージョン

| 対応バージョン            | 内容                                                                            |
| :------------------------ | :------------------------------------------------------------------------------ |
| プリザンター1.4.16.0 以降 | 拡張サーバスクリプト専用パラメータにBeforeBulkDeleteおよびAfterBulkDeleteを追加 |
| プリザンター1.4.16.0 以降 | 利用条件を追加                                                                  |

## 関連情報

### Pleasanter Code Assist

-   [コマンドによる作業フォルダ作成](pleasanter-code-assist-create-workfolder.md)
-   [セットアップ、事前準備](pleasanter-code-assist-setup.md)
-   [コマンドおよび設定項目](pleasanter-code-assist-feature.md)

### 開発者ガイド

-   [項目名とデータベース上のカラム名の対応](../../../developers-guide/dev-column-name.md)

-   [開発者ガイド：拡張機能：拡張SQL：APIから拡張SQLを実行する](../../../developers-guide/extended-features/extended-sql/extended-sql-api.md)
-   [開発者ガイド：サーバスクリプト](../../../developers-guide/server-script/index.md)

### FAQ：編集画面の操作・設定

-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
