---
title: 拡張SQL
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-sql
translationKey: extended-sql
shortname: 拡張SQL
created: 2019-04-30
updated: 2024-09-13
---

## 概要

拡張SQLは、プリザンターがデータベースに対して発行するSQL処理を、プログラミングによってカスタマイズする機能です。

1. **レコードの作成前、更新後などのデータ反映時のタイミングで任意のSQLを追加、実行することができる**
   ```csv
   ［例］レコードの新規作成のタイミングで、別テーブルのレコードを更新
   ```
1. **リンクサーバ（SQL Server）またはDBリンク（PostgreSQL）を利用することで、別システムのデータベースに対してSQLを実行できる**<br>

1. **プリザンター内で発生するイベントに対して、対象をWhere句やOrderBy句で制御できる**  
   ```csv
   ［例］レコードのアクセス制御を利用せず、より細かい条件でレコード単位のアクセス制御を実現  
   ［例］特定グループのメンバーのみ二段階認証をスキップ
   ```
1. **APIから呼び出して実行できる**  
   ```csv
   ［例］スクリプト、サーバスクリプトからデータベース内のデータを直接取得・更新する処理を実装
   ```

#### 拡張SQLの実行

拡張SQLは、SQLにプリザンターへの登録に必要な情報を添え、JSON形式のパラメータファイルとして専用のフォルダへ配置することで登録できます。

登録した任意の拡張SQLを実行する方法は2つに大別できます。

1. プリザンター内で発生するイベントに紐付けして実行する方法
1. 任意のタイミングで、サーバスクリプトまたはAPIから呼び出して実行する方法

このページでは前者の実行方法について説明します。後者の方法の詳細は、以下の各ページを確認してください。

#### サーバスクリプト

1. [開発者ガイド：サーバスクリプト：extendedSql](../../server-script/extended-sql/index.md)
1. [開発者ガイド：サーバスクリプト：view](../../server-script/view/index.md)
1. [開発者ガイド：サーバスクリプト：view.OnSelectingWhere](../../server-script/view/server-script-view-on-selecting-where.md)

#### API

1. [開発者ガイド：拡張機能：拡張SQL：APIから拡張SQLを実行する](extended-sql-api.md)

## 注意事項

1. 本機能を誤って使用するとプリザンターを利用できなくなったり、プリザンター内のデータを壊してしまったりする可能性があります。
1. 十分な検証、テストを経たうえで利用してください。
1. APIキーやセッションによるログイン確認は行いますが、テーブルの権限確認は行いません。SQL内で確認が必要です。

## 制限事項

1. 拡張SQLで使用するJSONファイル、SQLファイルの更新は、プリザンターの再起動後に反映されます。
1. セキュリティ上の理由により、拡張SQLはWeb画面からは設定できません。

## 拡張SQLの設定方法

本マニュアルに従ってプリザンターをセットアップしている場合、以下の手順で設定できます。

1. C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters\ExtendedSqls配下に以下の内容を含むJSONファイルを作成し、プリザンターを再起動してください。
1. ファイルの拡張子は必ず「.json」としてください。
1. ExtendedSqls\配下はフォルダで階層化できます。この場合、配下のすべてのJSONファイルが設定ファイルとして読み込まれます。

## JSONファイルのパラメータ

#### 基本設定

| パラメータ名 | 設定例                     | 説明                                                |
| :----------- | :------------------------- | :-------------------------------------------------- |
| Name         | Sample                     | APIから実行する際の識別名です。                     |
| Description  | "このSQLは...を実行します" | 拡張SQLの説明文です。省略可。                       |
| Disabled     | false                      | trueの場合、無効化され動作しません。                |
| CommandText  | "update [Issues] set ..."  | 実行するSQLを記述します。[※詳細説明](#comtext) |

#### 実行対象の絞り込み

以下のパラメータは、いずれも省略可能です。

| パラメータ名 | 設定例  | 説明                                               |
| :----------- | :------ | :------------------------------------------------- |
| DeptIdList   | [1,2,3] | 対象とする組織IDを配列形式で指定します。           |
| GroupIdList  | [1,2,3] | 対象とするグループIDを配列形式で指定します。       |
| UserIdList   | [1,2,3] | 対象とするユーザIDを配列形式で指定します。         |
| SiteIdList   | [1,2,3] | 対象とするサイトのサイトIDを配列形式で指定します。 |
| IdList       | [1,2,3] | 対象とするレコードのIDを配列形式で指定します。     |

#### イベントトリガー

以下のパラメータは、実行タイミングを制御するイベントトリガーです。

| パラメータ名                 | 設定値 |説明                                         |
| :--------------------------- | :-- | :------------------------------------------- |
| OnCreating                   | false |trueの場合、レコード作成前に実行する。       |
| OnCreated                    | false | trueの場合、レコード作成後に実行する。       |
| OnUpdating                   | false | trueの場合、レコード更新前に実行する。       |
| OnUpdated                    | false | trueの場合、レコード更新後に実行する。       |
| OnDeleting                   | false | trueの場合、レコード削除前に実行する。       |
| OnDeleted                    | false | trueの場合、レコード削除後に実行する。       |
| OnBulkDeleting               | false | trueの場合、レコード一括削除前に実行する。   |
| OnBulkDeleted                | false | trueの場合、レコード一括削除後に実行する。   |
| OnImporting                  | false | trueの場合、レコードインポート前に実行する。 |
| OnImported                   | false | trueの場合、レコードインポート後に実行する。 |
| OnUseSecondaryAuthentication | false | trueの場合、二段階認証前に実行する。         |

#### 動的制御

| パラメータ名                      | 設定例                | 説明                                                                                                                                |
| :-------------------------------- | :-------------------- | :---------------------------------------------------------------------------------------------------------------------------------- |
| OnSelectingColumn                 | false                 | trueの場合、一覧画面および編集画面に表示する項目の内容を動的に取得するためのSQLを追加します。                                         |
| ColumnList                        | ["ClassA"]            | OnSelectingColumnを使用する際に対象となる[データベースのカラム名](../../dev-column-name.md)を指定します。                         |
| OnSelectingWhere                  | false                 | trueの場合、一覧画面および編集画面に表示するレコードを限定するためのWhere句を追加します                                               |
| OnSelectingWhereParams            | ["ExtendedFieldName"] | 指定した拡張フィールドに値が入力されたとき、OnSelectingWhereへ値をパラメータとして追加します。<br>※拡張フィールドのNameの値を指定   |
| OnSelectingWherePermissionsDepts  | false                 | trueの場合、アクセス制御の選択肢一覧に表示するDeptsテーブルのレコードを限定するWhere句を追加します。                                |
| OnSelectingWherePermissionsGroups | false                 | trueの場合、アクセス制御の選択肢一覧に表示するGroupsテーブルのレコードを限定するWhere句を追加します。                               |
| OnSelectingWherePermissionsUsers  | false                 | trueの場合、アクセス制御の選択肢一覧に表示するUsersテーブルのレコードを限定するWhere句を追加します。                                |
| OnSelectingOrderBy                | false                 | trueの場合、一覧画面に表示するレコードを並び替えるためのOrderBy句を追加します。                                                     |
| OnSelectingOrderByParams          | ["ExtendedFieldName"] | 指定した拡張フィールドに値が入力されたとき、OnSelectingOrderByへ値をパラメータとして追加します。<br>※拡張フィールドのNameの値を指定 |

#### API連携

| パラメータ名 | 設定例  | 説明                                                                                                                                                                                            |
| :----------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Api          | false   | trueの場合、[APIから拡張SQLを実行](extended-sql-api.md)できます。また、[サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)のextendedSqlオブジェクトからも実行可能となります。 |
| DbUser       | "Owner" | APIから拡張SQLを実行するDBユーザを指定します。省略時は"User"で実行します。APIから実行する場合のみ有効となります。                                                                               |
| Html         | false   | trueの場合、HTMLのinputタグにhiddenタイプとして取得した値を格納します。                                                                                                                         |

<a id="comtext"></a>

## CommandTextの詳細

CommandText内では、以下の変数とプレースホルダーを利用できます。

#### 変数

| 説明                 | SQL Server       | PostgreSQL        | OnUseSecondaryAuthentication<br>がtrueの場合の使用 |
| :------------------- | :--------------- | :---------------- | :------------------------------------------------- |
| テナントID           | @_T<br>@TenantId | @ipT<br>@TenantId | 不可<br>可                                         |
| 実行ユーザの組織ID   | @_D              | @ipD              | 不可                                               |
| 実行ユーザのユーザID | @_U<br>@UserId   | @ipU<br>@UserId   | 不可<br>可                                         |

#### プレースホルダー

イベントトリガーOnUseSecondaryAuthenticationをtrueに設定した場合は、利用できません。

| プレースホルダー | 設定例                | 説明                                                                                                                                             |
| :--------------- | :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| {{SiteId}}       | 2                     | サイトIDに置換されます。                                                                                                                         |
| {{Id}}           | 10                    | レコードのIDに置換されます。                                                                                                                     |
| {{Timestamp}}    | 20171106 09:00:00.000 | フォームから投入されたレコード更新前のタイムスタンプに置換されます。OnUpdatingの場合のみ使用できます。レコードの更新競合のチェックに利用できます。 |

#### 外部ファイル化

CommandTextの内容を外部ファイルにまとめ、インポートできます。

JSONファイルの「拡張子を含むファイル名」に「拡張子.sqlを追加」したSQLファイルを作成し、JSONファイルと同じディレクトリに配置してください。

##### 例：sample.jsonのCommandTextを外部ファイル化する場合

```text
sample.json.sql
```

## ストアドプロシージャの実行

拡張SQLからストアドプロシージャを実行する場合には「Implem.Pleasanter_User」にEXECUTE権限を付与してください。

## リンクサーバー

データベースにSQL Serverを利用している場合は、リンクサーバー機能を使用し、外部のデータベースとの入出力が可能です。

## サンプルコード

<details markdown="1">

<summary style="font-weight:bold; color:#1d3994;">➊ サイトID:2のレコードが更新された際にCommandTextのSQLを実行</summary>

以下のサンプルコードでは、サイトID:2のレコードが更新された際にCommandTextのSQLが実行されます。

##### JSON

```json
{
    "Description": "Sample",
    "SiteIdList": [2],
    "OnUpdated": true,
    "CommandText": "-- 任意のSQLを記述します"
}
```

</details>

<details markdown="1">

<summary style="font-weight:bold; color:#1d3994;">➋ Users.Bodyに"NOLIST"が設定されているユーザを選択肢一覧から除外</summary>

以下のサンプルコードでは、Users.Bodyに"NOLIST"が設定されているユーザを選択肢一覧から除外します。

##### JSON

```json
{
      : 省略
    "OnSelectingWherePermissionsUsers": true,
    "CommandText": "(\"Users\".\"Body\" is null or \"Users\".\"Body\"<>'NOLIST')"
}
```

CommandTextにはWhere句の条件式のみを記述してください（キーワードWhere自体は不要です）。

##### 実行イメージ

▼実行前の選択肢一覧  
![拡張SQLを適用する前の選択肢一覧](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/4ccf653a993e4b64b4a95c361c67e5e2.png)

▼任意のレコードにおいて[説明](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)項目（Body）にNOLISTと入力  
![説明項目（Body）にNOLISTと入力したレコード](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/08f4e52c71d44b548608d88c5c5e5952.png)

▼選択肢一覧から除外される  
![NOLISTと入力したレコードが選択肢一覧から除外された状態](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/c9eb58043d3a4c58a6a42259d5bb4c84.png)

</details>

<details markdown="1">

<summary style="font-weight:bold; color:#1d3994;">➌ 特定のグループのメンバーのみ二段階認証をスキップ</summary>

以下のサンプルコードでは、グループID:1のメンバーであるユーザに対して二段階認証をスキップします。

##### JSON

```json
{
      : 省略
    "OnUseSecondaryAuthentication": true,
    "CommandText": "select 0 from [GroupMembers] where [GroupMembers].[GroupId] = 1 and [GroupMembers].[UserId] = @UserId;"
}
```

</details>

## 関連情報

-   [開発者ガイド：サーバスクリプト：extendedSql](../../server-script/extended-sql/index.md)
-   [開発者ガイド：サーバスクリプト：view](../../server-script/view/index.md)
-   [開発者ガイド：サーバスクリプト：view.OnSelectingWhere](../../server-script/view/server-script-view-on-selecting-where.md)
-   [開発者ガイド：拡張機能：拡張SQL：APIから拡張SQLを実行する](extended-sql-api.md)
-   [テーブルの管理：エディタ：項目の詳細設定：説明](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-column-description.md)
